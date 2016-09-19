#Functional Specification Document v0.1.1


## 1. Data Profiling
- *Cumulative Profiling: Null Count, Unique Count, Duplicate Count, Maximum, Minimum, Mean, Median*
- *Anomaly detection, support machine learning algorithms: History Trend, MAD, Bollinger Bands*

## 2. DQ Measurement
### Model management
- **Model definition, support 3 dimensions in this version: Completeness, Validity, Accuracy**

Considerations for a model(KPI) definition

| item   | Desc |
|-------------- | --------------- |
| Name | A meaningful name of the KPI that express what is being measured.  |
| Objective | Why do you measure this? What business processes are impacted if there data is not ok?  |
| Dimensions | What data quality dimensions (integrity, validity, etc.) are this KPI related to?  |
| Frequency of measure |How often do you wish to report on this KPI? Daily, weekly or monthly?  |
|Unit of measure|What is the unit of the KPI? Number of records, pct of records, number of bad values, etc.?|
|Lowest acceptable measure| Threshold that indicates if the data quality aspect the KPI represents is at a minimal acceptable level. The value here must be in the unit of measure of the KPI. |
|Target value|At what value is the KPI considered to represent data quality at a high level? |
|Responsible|The person responsible for the particular KPI. |
|Formula|The tables and fields that are used to analyze and calculate the KPI. This is the functional design formula that forms the basis for the technical implementation|
|Hierarchies|When reporting on a KPI it is very useful to be able to slice and dice the measure according to different dimensions or hierarchies. For a customer data KPI for instance, good hierarchies would be regions, country, company code and account group.<br/> Being able to view the KPI through a hierarchy also makes it easier to follow up with specific groups of business users. |
|Notes and assumptions|If certain assumptions are made about the KPI make sure to document it. |


Measurement types

|No. | Dimension |Type           |    Desc|
|----|-----------|---------------|--------|
| *1   | Accuracy  | Cross table   | Compare with single source of truth|
|  2  | Validity  | Column        | Value conforms to format           |
|   3 | Validity  | Column        | Value conforms to a range          |
|   *4 | Validity  | Column        | Value conforms to RegEx            |
|  *5  | Validity  | Column        | Compare values on incoming data to valid values in a defined domain (reference table, or mathematical rule)            |
|  *6  | Completeness| Dataset     | Record counts matches a defined expectation |
|  7  | Completeness| Cross table     | Record counts matches a defined expectation compared with a source table |
|  *8  | Completeness| Column      | Ensure all non-nullable fields are populated |
|  *9  | Completeness| Column/Cross table      | Confirm referential integrity between parent/child tables to identify parentless child("orphan") records and values |


### Model Engine
- Job Scheduler

  According to the model definition, it creates and schedules the jobs for running
- Model Executor, support both real-time data and batch data

  The backend executor running on Spark, to produce the metric values

## 3. DQ Scorecards

### Scorecard definition
- Model consumer could be different from creator, consumer defines his own threshold and notification email, enable Anomaly Detection for a Count(Total, Null, Unique, etc.),  subscribes the measurements to be shown in scorecard

### Heatmap
- Display the heatmap according to user's subscription

### Notification
- A notification service supports different types of notifications, such as email, information bar on web UI, twitter, etc.
- Support Email Reporting first: the scorecard can be sent through email

## 4. Issue Resolution
- Download executor report, so that we will know what kind of data fails and easy to do RCA
- Download sample data

## 5. Metadata Management
- Data Asset Registration, only support HiveTable.
- Dataset definition: how to retrieve the datasets for daily/weekly/hourly calculations
- Schema Registration
- Organization management
- Others

## 6. Security