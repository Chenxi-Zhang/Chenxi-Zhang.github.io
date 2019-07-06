# Pseudodistributed Mode setup

1. Edit configuration files in {$HADOOP_CONF_DIR}. 
2. Configure SSH to Localhost. 
3. Format the HDFS.
```bash
hdfs namenode -format
```
4. Start the daemons. To start the HDFS, YARN, and MapReduce daemons, type. 
```bash
export HDFS_NAMENODE_USER="root"
export HDFS_DATANODE_USER="root"
export HDFS_SECONDARYNAMENODE_USER="root"
export YARN_RESOURCEMANAGER_USER="root"
export YARN_NODEMANAGER_USER="root"
echo 'JAVA_HOME=/docker-java-home' >> $HADOOP_CONF_DIR/hadoop-env.sh

start-dfs.sh
start-yarn.sh
mr-jobhistory-daemon.sh start historyserver
# mapred --daemon start historyserver

jps
```
5. Create a user directory. 
```bash
hadoop fs -mkdir -p /user/root
```