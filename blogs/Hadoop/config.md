# Config notes

----
### conf位置
* $HADOOP_CONF_DIR
* (or) $HADOOP_HOME/etc/hadoop/

----
### 属性property(变量variable)
* 在core-site.xml中，不要循环定义属性。在其他.xml中，不要引用除core-site.xml中以外的属性。
* 引用属性，可以使用其`<name></name>`属性，e.g. `<value>${hadoop.tmp.dir}</value>`。