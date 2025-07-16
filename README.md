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
推流:
ffmpeg -re -stream_loop -1 -i "/Users/rain/Downloads/ylx_test.mp4" -c copy -f rtsp -rtsp_transport tcp rtsp://127.0.0.1:11554/live/test
流转m3u8:
ffmpeg -fflags nobuffer \                                                      
 -loglevel debug \
 -rtsp_transport tcp \
 -i rtsp://127.0.0.1:11554/live/test \
 -vsync 0 \
 -copyts \
 -vcodec copy \
 -movflags frag_keyframe+empty_moov \
 -an \
 -hls_flags delete_segments+append_list \
 -f hls \
 -hls_time 1 \
 -hls_list_size 3 \
 -hls_segment_type mpegts \
/Users/rain/work_space/docker_space/docker_env/nginx-rtmp/www/hls/ylx/ylx.m3u8


# minio-old
低版本minio用于直接存储原始图片信息
