# Entrypoint

----
### 用法
* `ENTRYPOINT ["echo", "Hello Docker!"]`
* `ENTRYPOINT ["/entrypoint.sh"]`

```bash
#!/bin/bash
# /entrypoint.sh
set -e
echo "Hello, Docker!"
exec "$@"    #只会执行一个exec
```
* 结合CMD，可以进行组合
* `CMD ["bash", "-c", "echo 'another echo'"]`
* Entrypint CMD区别：[知乎](https://zhuanlan.zhihu.com/p/30555962)
