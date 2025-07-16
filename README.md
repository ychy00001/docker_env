# 常用中间件集合


# kafka
复制容器中的kafka版本到本地
```
docker-compose cp dev-kafka:/opt/bitnami/kafka/* ./kafka/opt
```

本机测试容器kafaka正常运行
```
cd kafka/opt/bin
./kafka-console-producer.sh --producer.config ../config/producer.properties --bootstrap-server 127.0.0.1:19094 --topic test
./kafka-console-consumer.sh --consumer.config ../config/consumer.properties --bootstrap-server 127.0.0.1:19094 --topic test --from-beginning
````

> 本地Java SDK可能无法启动G1垃圾收集，需要在./kafka/opt/bin/kafka-run-class.sh中最后启动java应用增加-XX:+UnlockExperimentalVMOptions

示例：nohup "$JAVA" -XX:+UnlockExperimentalVMOptions $KAFKA_HEAP_OPTS $KAFKA_JVM_PERFORMANCE_OPTS $KAFK A_GC_LOG_OPTS $KAFKA_JMX_OPTS $KAFKA_LOG4J_CMD_OPTS -cp.....


# kafka-console-ui
kafka可视化组件


# nginx-rtmp
使用nginx-http-flv模块镜像，包含nginx-rtmp模块，可以进行flv直播。
官方镜像：https://hub.docker.com/r/mugennsou/nginx-http-fl
