# Setup

----
### Use YARN as spark.master
* Config的位置：`$SPARK_HOME/conf/spark-defaults.conf`
* `spark.master    yarn`

----
### Mode

* Cluster mode: everything runs inside the cluster. You can start a job from your laptop and the job will continue running even if you close your computer. In this mode, the Spark Driver is encapsulated inside the YARN Application Master.
* Client mode: the Spark driver runs on a client, such as your laptop. If the client is shut down, the job fails. Spark Executors still run on the cluster, and to schedule everything, a small YARN Application Master is created.

----
### Logs
* `spark.eventLog.enabled  true`
* `spark.eventLog.dir hdfs://master/spark-logs`
* Create dir: `hadoop fs -mkdir /spark-logs`

----
### History server
* Modify `spark-defaults.conf`.
```
spark.history.provider            org.apache.spark.deploy.history.FsHistoryProvider
spark.history.fs.logDirectory     hdfs://master/spark-logs
spark.history.fs.update.interval  10s
spark.history.ui.port             18080
```
* `$SPARK_HOME/sbin/start-history-server.sh`

----
### 遇到的问题
* Native lib warning: `export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:"$HADOOP_HOME"/lib/native`
