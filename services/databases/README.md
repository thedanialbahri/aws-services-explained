# Databases

A **database** stores organised data that apps can search, add to and update quickly – like customers, orders or game scores.

**Real-life comparison:** A spreadsheet is a simple database. A **relational** database is like a set of linked spreadsheets with strict columns (customers, orders, products). A **NoSQL** database is more like a giant set of labelled index cards – very fast to find one card by its label, and each card can hold different details.

## Relational vs NoSQL

| | Relational (SQL) | NoSQL |
|---|---|---|
| **Shape of data** | Tables with fixed columns | Flexible: key-value, documents, graphs |
| **Good for** | Orders, accounts, finance – things with lots of links | Huge scale, simple lookups, changing data shapes |
| **Language** | SQL | Depends on the database |
| **AWS examples** | [RDS](rds.md), [Aurora](aurora.md) | [DynamoDB](dynamodb.md), [DocumentDB](documentdb.md) |

## Services in this category

| Service | Level | What it does |
|---------|-------|--------------|
| [Amazon RDS](rds.md) | 🟢 | Managed relational databases (MySQL, PostgreSQL, SQL Server and more) |
| [Amazon DynamoDB](dynamodb.md) | 🟢 | Fast NoSQL database that scales without servers |
| [Amazon Aurora](aurora.md) | 🟡 | AWS's own MySQL- and PostgreSQL-compatible database |
| [Amazon ElastiCache](elasticache.md) | 🟡 | In-memory cache that makes apps faster |
| [Amazon Redshift](redshift.md) | 🟡 | Data warehouse for analysing large amounts of data |
| [Amazon MemoryDB](memorydb.md) | 🔴 | Durable in-memory database compatible with Redis/Valkey |
| [Amazon DocumentDB](documentdb.md) | 🔴 | Document database compatible with MongoDB |
| [Amazon Neptune](neptune.md) | 🔴 | Graph database for data about connections |
| [Amazon Keyspaces](keyspaces.md) | 🔴 | Managed database compatible with Apache Cassandra |
| [Amazon Timestream](timestream.md) | 🔴 | Database for time-stamped data, like sensor readings |

[← Back to the main index](../../README.md)
