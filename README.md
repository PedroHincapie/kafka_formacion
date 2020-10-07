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
### Nota:
* Los replication-factor nos permite darle disponibilidad a nuestros mensajes, gracias a la generación de replicas de nuestro broker.

* En este punto es clave mencionar que tendremos siempre un leader y el resto son Follower.

* Por ultimo mencionar que los replicas son directamente proporcional a la cantidad de broker disponibles dentro del cluster. 

* Tener múltiples particiones permite tener más
consumidores de mensajes funcionando de forma
concurrente, esto se ve reflejado en el incremento del
throughput(tasa de transferencia).

* Mientras que el partitions, nos permite darle una mejor taza de lectura a nuestros mensajes puesto que da la posibilidad de tener mas consumidores.

* Para incrementar la disponibilidad de la información, los topics se deben replicar en múltiples brokers, esto se define en el atributo replication-factor, el cual define el
número de copias de la información.

* Cada topic tendrá asignado un líder y seguidores.

* Una replica actualizada se conocerá como (In-sync) y se mantiene actualizada con los cambios del líder. Si el líder falla una In-sync se puede convertir en líder.
En un ambiente saludable todas las replicas deben encontrarse In-sync, es aceptable que no se encuentren de ese modo después de un fallo.

* ##### Para generar la lista de tópicos
```
sh bin/kafka-topics.sh --bootstrap-server localhost:9092 --list
```
* ##### Para conocer la descripción por medio de la que fue creado un topic
```
bin/kafka-topics.sh --bootstrap-server localhost:9092 --describe 
```
o en el caso que necesites indicarle el topic
```
bin/kafka-topics.sh --bootstrap-server localhost:9092 --describe --topic topic-pedro
```

* ##### Para creación de un consumer sencillo
```
sh bin/kafka-console-consumer.sh --bootstrap-server localhost:9092 --topic topic-pedro
```

La observación de esta estrategia es que el momento de no estar ejecutándose el consumidor no pervivirá los mensajes con anterioridad a su ejecución, por esos mensajes se perdurar.

* ##### Para creación de un consumer con la captura de mensajes depositados desde antes de la ejecución de consumer
```
bin/kafka-console-consumer.sh --bootstrap-server localhost:9092 --topic topic-pedro --from-beginning
```

En este caso el detalle es que se trae todo lo que tenga desde el inicio de esta cola, para tener presente.

* ##### Para el caso en que necesitemos recibir e identificar cual es la key del mensaje que se recibeira de parte del consumer tenesmo:

```
bin/kafka-console-consumer.sh --bootstrap-server localhost:9092 --topic topic-pedro --from-beginning --property print.key=true --property key.separator="-"
```

* ##### Para creación de un producer sencillo
```
sh bin/kafka-console-producer.sh --bootstrap-server localhost:9092 --topic topic-pedro
```





