# Setting Up a Hadoop Cluster

### Cluster Specification
* **Cluster Sizing**: start with a small cluster, and grow it as the storage and computational needs grow. 
> **Master node scenarios**: namenode has high memory requirements. The secondary namenode has a comparable memory footprint to the primary. 
* **Network Topology**: typical two-level network topoloty: 30-40 servers per rack, with a 10 Gb switch for the rack and an uplink to a core switch or router (10 Gb or better). 
> **Rack awareness**: to get maximum performance out of Hadoop, the node needs to know the topology of the network. Default configuration is to map all nodes to a single network location, calld `/default-rack`. A script (`net.topology.script.file.name`) is used to determine the mapping. 

### Cluster Setup and Installation
1. **Installing Java**
2. **Creating Unix User Accounts**
3. **Installing Hadoop**
4. **Configuring SSH**
5. **Configuring Hadoop**
6. **Formatting the HDFS Filesystem** 
7. **Starting and Stopping the Daemons**
8. **Creating User Directories**

### Hadoop Configuration
* **Environment Settings**: variables in hadoop-env.sh. Similarly, mapred-env.sh and yarn-env.sh. 
> **Java**: `JAVA_HOME` in hadoop-env.sh or ENV var. 
> **Memory heap**: 1GB by default. `HADOOP_HEAPSIZE` in hadoop-env.sh.
> **System logfiles**: `export HADOOP_LOG_DIR=/var/log/hadoop` in hadoop-env.sh.
> **SSH settings**: `ConnectTimeout`, `StrictHostKeyChecking`, `HADOOP_SSH_OPTS` in hadoop-env.sh.
* **Important Hadoop Daemon Properties**: core-site.xml, hdfs-site.xml, and yarn-site.xml. 
> **HDFS**: `fs.defaultFS` resolves the URI path like (hdfs://namenode/a/b). `dfs.namenode.name.dir` specifies a list of directories where the namenode stores persistent filesystem metadata. `dfs.datanode.data.dir` specifies a list of directories for a datanode to store its blocks in. `dfs.namenode.checkpoint.dir` specifies a list of directories where the checkpoints are kept. `hadoop.tmp.dir` specifies the HDFS tmp storage directory in local filesystem. 
> **YARN**: designate one machine (`yarn.resourcemanager.hostname`) as a resource manager. `yarn.nodemanager.local-dirs` controls the location of local tmp storage for YARN container. `yarn.nodemanager.aux-services` property, `mapreduce_shuffle` by default, is used to serve map outputs to reduce tasks. 
> **Memory settings in YARN and MapReduce**: `yarn.nodemanager.resource.memory-mb`, 8192MB in default, is the total memory allocation. For each individual jobs, memory is set by (1) size of the container allocated by YARN, or (2) heap size of the Java process run in the container `mapred.child.java.opts`. 
> **CPU settings in YARN and MapReduce**: `yarn.nodemanager.resource.cpu-vcores` controls number of cores that a node manager can allocate to containers. `mapreduce.map.cpu.vcores` and `mapreduce.reduce.cpu.vcores` are default to 1, which is appropriate for normal single-threaded MapReduce tasks. 
* **Hadoop Daemon Addresses and Ports**: RPC server VS HTTP server. In general, RPC server should be a resolvable hostname or IP addr, and HTTP should be 0.0.0.0 which binds all network interfaces. 
* **Other Hadoop Properties**
> **Cluster membership**: a list of authorized machines. `dfs.hosts` and `yarn.resourcemanager.nodes.include-path`.   
> **Buffer size**: 4 KB `io.file.buffer.size` property in core-site.xml.  
> **HDFS block size**: 128 MB `dfs.blocksize property` in hdfs-site.xml.  
> **Reserved storage space**: `dfs.datanode.du.reserved`.  
> **Trash**: `fs.trash.interval`  property in core-site.xml.   
> **Job scheduler**
> **Reduce slow start**: `mapreduce.job.reduce.slowstart.completedmaps`
> **Short-circuit local reads**

### Security
* **Kerberos and Hadoop**: 
* **Delegation Tokens**:

### Benchmarking a Hadoop Cluster:
* **Hadoop Benchmarks**: `hadoop jar $HADOOP_HOME/share/hadoop/mapreduce/hadoop-mapreduce-*-tests.jar`.
> **Benchmarking MapReduce with TeraSort**: (1) `hadoop jar $HADOOP_HOME/share/hadoop/mapreduce/hadoop-mapreduce-examples-*.jar teragen -Dmapreduce.job.maps=1000 10t random-data`. (2) `hadoop jar $HADOOP_HOME/share/hadoop/mapreduce/hadoop-mapreduce-examples-*.jar terasort random-data sorted-data`
> **Other benchmarks**: TestDFSIO, MRBench, NNBench, Gridmix, SWIM, TPCx-HS. 
* **User Jobs**: 
