# Kafka

Download

https://kafka.apache.org/downloads



go to directory where you descompact Kafka installation  

*Notice*: Your path must no have empty space

> cd  c:\tools\kafka_2.12-2.5.0



First you have to start **Zookeeper server**

> .\bin\windows\kafka-server-start.bat .\config\server.properties



Start **Kafka server** (default port 9092)

>  .\bin\windows\kafka-server-start.bat .\config\server.properties



**Create a topic** to exchange messages 

*Notice*: Your topic name shouldn't use period "." and "_"  at the same time

> .\bin\windows\kafka-topics.bat --create --bootstrap-server localhost:9092 --replication-factor 1 --partitions 1 --topic STORE_NEW_ORDER

```
PS C:\tools\kafka_2.12-2.5.0> .\bin\windows\kafka-topics.bat --create --bootstrap-server localhost:9092 --replication-factor 1 --partitions 1 --topic STORE_NEW_ORDER
WARNING: Due to limitations in metric names, topics with a period ('.') or underscore ('_') could collide. To avoid issues it is best to use either, but not both.
Created topic STORE_NEW_ORDER.
```

**Check your topic**:

> .\bin\windows\kafka-topics.bat --list --bootstrap-server localhost:9002

```
PS C:\tools\kafka_2.12-2.5.0> .\bin\windows\kafka-topics.bat --list --bootstrap-server localhost:9092
STORE_NEW_ORDER
PS C:\tools\kafka_2.12-2.5.0>
```

**Producing messages** 

> .\bin\windows\kafka-console-producer.bat --broker-list localhost:9092 --topic STORE_NEW_ORDER

```
PS C:\tools\kafka_2.12-2.5.0> .\bin\windows\kafka-console-producer.bat --broker-list localhost:9092 --topic STORE_NEW_ORDER
>order0,100
>order1,101
>order2,102
>
```

**Consuming a message** 

> .\bin\windows\kafka-console-consumer.bat --bootstrap-server localhost:9092 --topic STORE_NEW_ORDER

Notice: In this example you don't see any message because you didn't define the "from" parameter (since when you can consume the message)

```
PS C:\tools\kafka_2.12-2.5.0> .\bin\windows\kafka-console-consumer.bat --bootstrap-server localhost:9092 --topic STORE_NEW_ORDER


```

Setting parameter *<u>from</u>*

> .\bin\windows\kafka-console-consumer.bat --bootstrap-server localhost:9092 --topic STORE_NEW_ORDER --from-beginning



```
PS C:\tools\kafka_2.12-2.5.0> .\bin\windows\kafka-console-consumer.bat --bootstrap-server localhost:9092 --topic STORE_NEW_ORDER --from-beginning
order0,100
order1,101
order2,102

```



If you produce another message you will see it in **both** consumers (with and without *<u>from</u>* parameter)



