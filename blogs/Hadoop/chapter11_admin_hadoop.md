# Administering Hadoop

### HDFS
* **Psersistent Data Structures**
> **Namenode directory structure**   
> **The filesystem image and edit log**   
> **Secondary namenode directory structure**   
> **Datanode directory structure**   

* **Safe Mode**
> **Entering and leaving safe mode**: `hdfs dfsadmin -safemode get`, `hdfs dfsadmin -safemode wait`, `hdfs dfsadmin -safemode enter`, `hdfs dfsadmin -safemode leave`. 

* **Audit Logging**: `export HDFS_AUDIT_LOGGER="INFO,RFAAUDIT"` to hadoop-env.sh. 
* **Tools**
> **dfsadmin**: admin operation on HDFS. `hdfs dfsadmin -help`.   
> **Filesystem check(fsck)**: checks the health of files in HDFS. `hdfs fsck /`.   
> **Finding the blocks for a file**: `hdfs fsck /path/to/file -files -blocks -racks`.   
> **Datanode block scanner**: `http://datanode:50075/blockScannerReport`.   
> **Balancer**: redistributes blocks by moving them from overutilized datanodes to underutilized datanodes. `start-balancer.sh`.   

### Monitoring
* **Logging**
> **Setting log levels**: `http://resource-manager-host:8088/logLevel`.   
> **Getting stack traces**: `http://resource-manager-host:8088/stacks`.   
* **Metrics and JMX**: metrics are information about events and measurements. All Hadoop metrics are published to JMX (Java Management Extensions). Set `com.sun.management.jmxremote.port` for remote access. ` http://namenode-host:50070/jmx`.   

### Maintenance
* **Routine Administration Procedures**
> **Metadata backups**: it is critical to make backups of namenode’s persistent metadata. `hdfs dfsadmin -fetchImage fsimage.backup`.   
> **Data backups**: key here is to prioritize your data. Backup high priority data. `distcp` is ideal.   
> **Filesystem check (fsck)**: run HDFS’s fsck tool regularly (daily).   
> **Filesystem balancer**: 
* **Commissioning and Decommissioning Nodes**: add or remove nodes. 
> **Commissioning new nodes**: `dfs.hosts` file lists all datanodes that are permiteed to connect to the namenode. `yarn.resourcemanager.nodes.include-path` is the same as `dfs.hosts` in most of time. `$HADOOP_CONF_DIR/slaves` file is a list of datanodes that are operated by Hadoop script as a cluster.   
> **Decommissioning old nodes**: use `dfs.hosts.exclude` and `yarn.resourcemanager.nodes.exclude-path` to decommission a node.  
* **Upgrades**: Backup!! Test!!
