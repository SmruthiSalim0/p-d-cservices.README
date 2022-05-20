# p-d-cservices.README

1. Create 3 microservices product-service(source), discount-service(processer) and courier-service(sink) with dependencies
                  1. Cloud stream
                  2. Lombok
                  3. Spring for Apache kafka
2. Run maven->lifecycle->install which build a 3 microservices

3. Run Zookeeper server

.\bin\windows\zookeeper-server-start.bat .\config\zookeeper.properties

4. Run Kafka server

.\bin\windows\kafka-server-start.bat .\config\server.properties

5.Run the skipper server by using java -jar, as follows:

java -jar spring-cloud-skipper-server-2.8.2.jar

6. Start the Data Flow Server

java -jar spring-cloud-dataflow-server-2.9.2.jar

7. Spring cloud server is up on localhost:9393

8. To start Spring Cloud Data Flow shell, the following command can be used:

java -jar spring-cloud-dataflow-shell-2.9.2.jar


9.Register all 3 microservices to Spring Cloud Data Flow Server using below commands

app register --name product-service --type source --uri maven://com.javatechie:product-service:jar:0.0.1-SNAPSHOT

app register --name discount-service --type processor --uri maven://com.javatechie:discount-service:jar:0.0.1-SNAPSHOT

app register --name courier-service --type sink --uri maven://com.javatechie:courier-service:jar:0.0.1-SNAPSHOT


10. Create Cloud Stream to connect between all microservices registered in spring cloud data flow server
create --name log-data --definition 'product-service | discount-service | courier-service'

11. Strat & Deploy Stream
stream deploy --name log-data
