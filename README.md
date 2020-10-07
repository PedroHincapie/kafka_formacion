# kafka_formacion
Repo en que que econtraremos lo comandos necesario para la formacion en apache kafka

* ##### Correr el Zookeeper
```
sh bin/zookeeper-server-start.sh config/zookeeper.properties
```

* ##### Correr el servidor de Kafka
```
sh bin/kafka-server-start.sh config/server.properties
```

* ##### Crear un topic en kafka
```
bin/kafka-topics.sh --bootstrap-server localhost:9092 --create --topic topic-pedro --partitions 5 --replication-factor 1
```
En donde contamos con ciertos parámetros importantes
```
--bootstrap-server : Servido de kafka
--topic : Nombre del topic que se creara.
--partitions : Numero de particiones con los que contara el topic
--replication-factor: Numero de replicas por broker
```



