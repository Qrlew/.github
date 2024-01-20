# Qrlew

## The open-source DP layer for SQL

[Qrlew](https://qrlew.github.io/) (/ˈkɝlu/) is the [open source library](https://github.com/Qrlew) that rewrites SQL queries into privacy-preserving variants using [Differential Privacy (DP)](https://en.wikipedia.org/wiki/Differential_privacy).

Use Qrlew if you want to bring privacy guarantees to your SQL pipelines. It is:
- **SQL-to-SQL**: Qrlew turns SQL queries into differentially-private SQL queries that can be executed at scale on many SQL datastore, in many SQL dialects.
- **Feature-rich**: Qrlew covers the broadest range of SQL queries, including JOIN and nested queries
- **Privacy-optimized**: Qrlew keeps track of tight bounds and ranges throughout each step, minimizing the amount of noise needed to achieve differential privacy.

The rewriting process occurs in three stages: The *data practitioners’s* query is parsed
into a Relation, which is rewritten into a DP equivalent and finally executed by the the data
owner which returns the privacy-safe result.

## [Qrlew](https://qrlew.github.io/) motivations: make differential privacy affordable for analytics use cases

[Qrlew](https://qrlew.github.io/) assumes the *central model of differential privacy*, where a trusted central organization: hospital, insurance company, utility provider, called the *data owner*, collects and stores personal data in a secure database and whishes to let untrusted *data practitioners* run SQL queries on its data.

At a high level we pursued the following requirements:

* Ease of use for the *data practitioners*. The *data practitioners* are assumed to be data experts but no privacy experts. They should be able to express their queries using the most common dialect for data analysis: SQL.
* Ease of integration for the *data owner*. SQL is a common language to express data analysis tasks supported by most datastores of all scale.
* Simplicity for the *data owner* to setup privacy protection. Differential privacy is about capping the sensitivity of a result to the addition or removal of an individual that we call *privacy unit*. [Qrlew](https://qrlew.github.io/) assumes that the *data owner* can tell if a table is public and, if it is not, that it can assign exactly one *privacy unit* to each row of data. In the case there are multiple related tables, [Qrlew](https://qrlew.github.io/) enables to define easily the *privacy units* for each table transitively.
* Simple integration with synthetic data when available. Some queries are not very suitable for DP-rewriting (e.g.: `SELECT * FROM table`), in those cases [Qrlew](https://qrlew.github.io/) can use synthetic data as a fallback if provided.

These requirements dictated the overall *query rewriting* architecture and features.

## How does [Qrlew](https://qrlew.github.io/) work?

The [Qrlew](https://qrlew.github.io/) library, solves the problem of running a SQL query with DP guarantees in three steps:
1. the SQL query submitted by the *data practitioners* is parsed and converted into an intermediate representation called [Relation](https://en.wikipedia.org/wiki/Relation_(database)), this [Relation](https://en.wikipedia.org/wiki/Relation_(database)) is designed to ease the tracking of data types ranges or possible values, to ease the tracking of the *privacy unit* in the next step. 
2. The [Relation](https://en.wikipedia.org/wiki/Relation_(database)) is rewritten into a DP variant
3. The DP variant of the [Relation](https://en.wikipedia.org/wiki/Relation_(database)) can be rendered as an SQL query string in any dialect.

At the end of this process, the query string can submitted to the data store of the *data owner*. The output can be shared with the *data practitioner* or published without worrying about privacy leakage.

# Deep Dive into [Qrlew](https://qrlew.github.io/)

To learn more about [Qrlew](https://qrlew.github.io/) read the [Qrlew white paper](https://arxiv.org/pdf/2401.06273.pdf).

You can cite us:
```bibtex
@misc{grislain2024qrlew,
  title={Qrlew: Rewriting SQL into Differentially Private SQL}, 
  author={Nicolas Grislain and Paul Roussel and Victoria de Sainte Agathe},
  year={2024},
  eprint={2401.06273},
  archivePrefix={arXiv},
  primaryClass={cs.DB},
  url={https://arxiv.org/pdf/2401.06273.pdf},
}
```
