# Analytics

**Analytics** means collecting data, cleaning it up and turning it into answers – charts, reports and insights.

**Real-life comparison:** Think of making orange juice. You collect oranges (Kinesis, Data Exchange), wash and squeeze them (Glue, EMR), store the juice (S3 data lake, Lake Formation), and serve it in glasses people can enjoy (Athena queries, Quick Sight dashboards).

## Services in this category

| Service | Level | What it does |
|---------|-------|--------------|
| [Amazon Athena](athena.md) | 🟡 | Ask questions of files in S3 using SQL |
| [AWS Quick Sight](quicksight.md) (formerly QuickSight) | 🟡 | Dashboards and charts for business data |
| [Amazon Kinesis](kinesis.md) | 🟡 | Collects and processes data streams in real time |
| [AWS Glue](glue.md) | 🟡 | Finds, cleans and moves data between stores |
| [Amazon OpenSearch Service](opensearch.md) | 🟡 | Search and analyse logs and text |
| [Amazon EMR](emr.md) | 🔴 | Runs big data tools like Apache Spark |
| [AWS Lake Formation](lake-formation.md) | 🔴 | Builds and secures a data lake |
| [Amazon MSK](msk.md) | 🔴 | Managed Apache Kafka for streaming data |
| [AWS Data Exchange](data-exchange.md) | 🔴 | Find and subscribe to third-party data sets |

## A typical data pipeline

```
 Apps / devices ──► Kinesis ──► S3 (data lake) ──► Glue (catalogue + clean) ──► Athena (SQL) ──► Quick Sight (dashboards)
```

[← Back to the main index](../../README.md)
