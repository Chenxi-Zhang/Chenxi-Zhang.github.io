# Installation

----
### 基于hadoop的安装
1. 正确安装配置Hadoop，YARN。
2. 下载Spark，[apache官网](https://spark.apache.org/downloads.html)，选择user-provided hadoop的package。安装到$SPARK_HOME
3. 必要的环境设置，比如：
```bash
export SPARK_HOME=/usr/local/spark
export SPARK_VERSION=2.4.3
export SPARK_DIST_CLASSPATH=$(hadoop classpath)
export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:"$HADOOP_HOME"/lib/native
```
4. 如果有scala，可以进行交互。端口4040是Spark Context UI。

----
### Test
```bash
spark-submit --deploy-mode client \
    --class org.apache.spark.examples.SparkPi \
    $SPARK_HOME/examples/jars/spark-examples_2.11-"$SPARK_VERSION".jar 10 > result
cat result

```
* [部分解释](https://www.ibm.com/developerworks/cn/opensource/os-cn-spark-deploy1/index.html)

----
### 遇到的问题
* `java.lang.NoClassDefFoundError: org/slf4j/Logger`。需要设置`SPARK_DIST_CLASSPATH`。
* 