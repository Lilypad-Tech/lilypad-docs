---
description: Community Member Contribution
---

# DuckDB \[coming soon]

## Overview

[DuckDB](https://duckdb.org) is a fast and feature-rich in-process SQL OLAP ([online analytical processing](https://en.wikipedia.org/wiki/Online_analytical_processing)) database management system.
It supports CSV, JSON, and Parquet as input and output data formats. That allows you to easily and efficiently fill up the database, run some queries, and export the results. For example:

```sql
CREATE TABLE weather AS FROM '/inputs/weather.parquet';
CREATE TABLE cities AS FROM '/inputs/cities.csv.gz';

COPY (
 SELECT *
 FROM weather, cities
 WHERE cities.name = weather.city
) TO '/outputs/weather.json';
```

## \[CLI] Running DuckDB Module

To run some SQL, provide the input data and the query to the duckdb module like so:

```
lilypad run duckdb:v0.0.1 "{query: 'SELECT...', inputs_cid: 'Qm...'}"
```

The contents of the `inputs_cid` will be mounted to the `/inputs` folder from which you can import data in your SQL. Anything you write to `/outputs` will be available with the job results.

## Important note on determinism

[Modules must be deterministic](../lilypad-v1-examples/advanced-diy-module#requirements), therefore your queries must be too. It means that, given the same inputs, the outputs will be the same. In most of the cases, this should be achieved by simply [ordering](https://duckdb.org/docs/sql/query_syntax/orderby) the results.

## DuckDB Module Code

{% @github-files/github-code-block url="https://github.com/bacalhau-project/lilypad-modicum/blob/main/src/python/modules/duckdb.py" %}
