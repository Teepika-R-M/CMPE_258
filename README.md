# CMPE_258 : Assignment 2

## 



## Example


The main entry point for defining how you expect your data to look is the [VerificationSuite](src/main/scala/com/amazon/deequ/VerificationSuite.scala) from which you can add [Checks](src/main/scala/com/amazon/deequ/checks/Check.scala) that define constraints on attributes of the data. In this example, we test for the following properties of our data:

  * there are 5 rows in total
  * values of the `id` attribute are never NULL and unique
  * values of the `productName` attribute are never NULL
  * the `priority` attribute can only contain "high" or "low" as value
  * `numViews` should not contain negative values
  * at least half of the values in `description` should contain a url
  * the median of `numViews` should be less than or equal to 10

In code this looks as follows:

```scala
import com.amazon.deequ.VerificationSuite
import com.amazon.deequ.checks.{Check, CheckLevel, CheckStatus}


val verificationResult = VerificationSuite()
  .onData(data)
  .addCheck(
    Check(CheckLevel.Error, "unit testing my data")
      .hasSize(_ == 5) // we expect 5 rows
      .isComplete("id") // should never be NULL
      .isUnique("id") // should not contain duplicates
      .isComplete("productName") // should never be NULL
      // should only contain the values "high" and "low"
      .isContainedIn("priority", Array("high", "low"))
      .isNonNegative("numViews") // should not contain negative values
      // at least half of the descriptions should contain a url
      .containsURL("description", _ >= 0.5)
      // half of the items should have less than 10 views
      .hasApproxQuantile("numViews", 0.5, _ <= 10))
    .run()
```

After calling `run`, __deequ__ translates your test to a series of Spark jobs, which it executes to compute metrics on the data. Afterwards it invokes your assertion functions (e.g., `_ == 5` for the size check) on these metrics to see if the constraints hold on the data. We can inspect the [VerificationResult](src/main/scala/com/amazon/deequ/VerificationResult.scala) to see if the test found errors:

```scala
import com.amazon.deequ.constraints.ConstraintStatus


if (verificationResult.status == CheckStatus.Success) {
  println("The data passed the test, everything is fine!")
} else {
  println("We found errors in the data:\n")

  val resultsForAllConstraints = verificationResult.checkResults
    .flatMap { case (_, checkResult) => checkResult.constraintResults }

  resultsForAllConstraints
    .filter { _.status != ConstraintStatus.Success }
    .foreach { result => println(s"${result.constraint}: ${result.message.get}") }
}
```

If we run the example, we get the following output:
```
We found errors in the data:

CompletenessConstraint(Completeness(productName)): Value: 0.8 does not meet the requirement!
PatternConstraint(containsURL(description)): Value: 0.4 does not meet the requirement!
```
The test found that our assumptions are violated! Only 4 out of 5 (80%) of the values of the `productName` attribute are non-null and only 2 out of 5 (40%) values of the `description` attribute contained a url. Fortunately, we ran a test and found the errors, somebody should immediately fix the data :)

## More examples

Our library contains much more functionaliy than what we showed in the basic example. We are in the process of adding [more examples](src/main/scala/com/amazon/deequ/examples/) for its advanced features. So far, we showcase the following functionality:

 * [Persistence and querying of computed metrics of the data with a MetricsRepository](https://github.com/awslabs/deequ/blob/master/src/main/scala/com/amazon/deequ/examples/metrics_repository_example.md)
 * [Data profiling](https://github.com/awslabs/deequ/blob/master/src/main/scala/com/amazon/deequ/examples/data_profiling_example.md) of large data sets
 * [Anomaly detection](https://github.com/awslabs/deequ/blob/master/src/main/scala/com/amazon/deequ/examples/anomaly_detection_example.md) on data quality metrics over time
 * [Automatic suggestion of constraints](https://github.com/awslabs/deequ/blob/master/src/main/scala/com/amazon/deequ/examples/constraint_suggestion_example.md) for large datasets
 * [Incremental metrics computation on growing data and metric updates on partitioned data](https://github.com/awslabs/deequ/blob/master/src/main/scala/com/amazon/deequ/examples/algebraic_states_example.md) (advanced)

