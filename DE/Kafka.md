# Kafka

## Need for Kafka

* Movemment of data is crux of data industry. We move data from one point to another all the time.
* When there are less sources and destinations, we can easily code our way to tranfer data.
* But as the sources and destinations scale, we need a better solution to manage the data flow, this is where Kakfa comes in.
* It is high performant, fault tolerant and distributed. It can be used for data transportation, streaming, activity tracking, messaging among many things.
* It also has integration with many data engineering technologies.
* Kafka acts as a middle man for a large number of producers and consumers.

## Kafka Topics

* **Kafka topics** are like tables in a database. Each topic is furthur divided into **partitions** which are then indexed, the index are called **offsets**.
* Kafka is designed to store a certain quantity of data and the data is removed after sometime, say 1 week. But the offsets keep increasing and dont reset.
* The producers put data into kafka and the data is consumed by consumers.
* We **cannot** query data by topics.
* We can have as many partitions as we want, data is put in round-robin fashion unless a key is provided, in which case it follows a hashing algo.
*  
