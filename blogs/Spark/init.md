# Installation

----
### 基于hadoop的安装
1. 正确安装配置Hadoop，YARN。
2. 下载Spark，[apache官网](https://spark.apache.org/downloads.html)，选择user-provided hadoop的package。安装到$SPARK_HOME
3. 必要的环境设置，比如：
```bash
export SPARK_HOME=/usr/local/spark
export SPARK_MAJOR_VERSION=2
export SPARK_VERSION=2.4.3
export SPARK_DIST_CLASSPATH=$(hadoop classpath)
```
4. 如果有scala，可以进行交互。端口4040是Spark Context UI。

----
### Test
```bash
spark-submit --deploy-mode client \
    --class org.apache.spark.examples.SparkPi \
    $SPARK_HOME/examples/jars/spark-examples_2.11-"$SPARK_VERSION".jar 10
```