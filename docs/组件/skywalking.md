

# quick start

## docker

h2方式存储启动，这种方式启动后

Oap

```shell
docker run --name skywalking -p 1234:1234 -p 11800:11800 -p 12800:12800  -d apache/skywalking-oap-server
```

Ui

```
docker run --name skywalking-ui -d -p 8686:8080 --link skywalking:skywalking -e SW_OAP_ADDRESS=http://172.24.157.49:12800 apache/skywalking-ui
```
