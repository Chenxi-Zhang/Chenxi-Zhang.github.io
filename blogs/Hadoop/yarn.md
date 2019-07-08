# YARN

----
### YARN virtual memory limit
* [explanation](https://blog.yoodb.com/sugarliny/article/detail/1307)
* Config path: `$YARN_CONF_DIR/yarn-site.xml`.
* If (`2.1 GB of 2.1 GB virtual memory used`), it throws an error and stops the job. To solve the problem, we can:
* Change `yarn.nodemanager.vmem-pmem-ratio` from 2.1(default) to higher. 
* Or set `yarn.nodemanager.vmem-check-enabled` to false.
* Restart YARN daemon.

----
### YARN conf update
* Modify `$YARN_CONF_DIR/yarn-site.xml`.
* Restart YARN daemon.