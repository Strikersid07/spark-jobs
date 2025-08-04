# 🔧 Required JARs for Spark Jobs

This folder contains required libraries for running Spark 3.3.4 jobs that support Apache Hudi, Hive Metastore, HDFS, and JSON ingestion.

---

## 🗂️ JAR Categories & Why They're Needed

---

### 1. 🐘 Hive Integration (Apache Hive 2.3.9)

Required to access and sync Hudi tables to Hive Metastore.

- `hive-exec-2.3.9-core.jar`
- `hive-jdbc-2.3.9.jar`
- `hive-metastore-2.3.9.jar`
- `hive-serde-2.3.9.jar`
- `hive-shims-*.jar`, `hive-common-2.3.9.jar`
- `postgresql-42.7.3.jar` — for Hive Metastore backend on PostgreSQL
- `commons-dbcp-1.4.jar`, `commons-pool-1.5.4.jar` — JDBC connection pooling

---

### 2. 🔁 Apache Hudi (0.15.0)

Required to write Spark DataFrames to Hudi tables (COPY_ON_WRITE), enable Hive sync, and enable upserts.

- `hudi-spark3.3-bundle_2.12-0.15.0.jar`
- `avro-1.11.0.jar` — Hudi uses Avro schema internally
- `parquet-*`, `orc-*` — Support Parquet/ORC read/write
- `commons-compress-1.21.jar`, `xz-1.9.jar`, etc. — Required for efficient compression

---

### 3. 🧬 Spark Core & Hive Runtime (Spark 3.3.4)

Needed only if running Spark in standalone mode (not pre-packaged).

- `spark-core_2.12-3.3.4.jar`
- `spark-sql_2.12-3.3.4.jar`
- `spark-hive_2.12-3.3.4.jar`
- `spark-launcher_2.12-3.3.4.jar`
- `spark-hive-thriftserver_2.12-3.3.4.jar` (optional)
- `spark-streaming_2.12-3.3.4.jar` (optional)

---

### 4. 📦 JSON Parsing & Serialization

Required for parsing JSON input files and transforming them in Spark:

- ✅ **Jackson** (Spark internally uses this for `read.json()`):
  - `jackson-core-2.13.4.jar`
  - `jackson-databind-2.13.4.2.jar`
  - `jackson-annotations-2.13.4.jar`
  - `jackson-dataformat-yaml-2.13.4.jar` (optional)
  - `jackson-module-scala_2.12-2.13.4.jar`

- ✅ **json4s** (used internally by Spark + Hudi):
  - `json4s-core_2.12-3.5.5.jar`
  - `json4s-jackson_2.12-3.5.5.jar`
  - `json4s-ast_2.12-3.5.5.jar`

> ⚠️ *Avoid mixing conflicting versions like `3.5.5` and `3.7.0-M11` unless tested. Choose one set.*

---

### 5. 📂 HDFS & Hadoop Integration

Required for Spark to read/write to HDFS:

- `hadoop-hdfs-client-3.3.4.jar`
- `hadoop-shaded-guava-1.1.1.jar`
- `commons-io-2.11.0.jar`
- `hadoop-common-3.3.4.jar` (from `$HADOOP_HOME` if not bundled)

---

## 📝 .gitignore Recommendation

```gitignore
libs/*.jar
!README.md
