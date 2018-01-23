# Kafka with Zookeeper Container

This is a docker container image that has both Kafka and Zookeeper running in the same container. This container can be easly executed either using a server, cloud or local for POC or demostrative purposes. Kafka client is also included so the running instance can be testing in multiple platforms.

### Notes

1- These instructions do not include the use of volumes, therefore keep in mind that the data created in kafka will be destroyed if the container is removed. Also if multiple container instances are executed they won't share topics and/or messages. 

2- if you have not set permissions to run docker engine commands you might need to precede the commands with ```sudo``` for root level execution.

### Prerequisites
1- Install Docker Enterprise or CE

2- Make sure docker engine is running by running ```docker run hello-world```

### Creating the Kafka container from the Dockerfile
1- Download the kafka folder and from the folder run ```sudo docker build -t kafka .```

2- This should create the image from scratch, otherwise you can load the image

### Loading the image in docker
1- Place the image file (kafka_zookeeper_container.tar) in a local folder and run ```docker load --input kafka_zookeeper_container.tar```

2- Check that the image is loaded by running ```docker images```

### Running Kafka and Zookeeper
1- Run the container in the background by using the command ```sudo docker run -d -p 2181:2181 -p 9092:9092 --env ADVERTISED_HOST=localhost --env ADVERTISED_PORT=9092 --name kafka kafka```

2- Check the output from the container by typing: ```docker logs kafka``` you should see the following message:  ```INFO success: kafka entered RUNNING state, process has stayed up for > than 1 seconds (startsecs)```

### Testing Kafka Running in the Container
1- Unpack the kafka_client.tar package and navigate to the bin folder

2- In the bin folder run the following command to create a test topic ```./kafka-topics.sh --create --zookeeper localhost:2181 --replication-factor 1 --partitions 1 --topic test```

3- Then you can input messages to the topic using the command line by running the console producer tool with this command  ```./kafka-console-producer.sh --broker-list localhost:9092 --topic test```

4- You can consume the messages from the topic by subscribing to the test topic with the console consumer tool ```./kafka-console-consumer.sh --bootstrap-server localhost:9092 --topic test --from-beginning```

