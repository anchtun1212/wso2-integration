# Test ProxyService Project

1) Run the jar file with Java 8: `/usr/lib/jvm/java-8-openjdk-amd64/jre/bin/java -jar Hospital-Service-JDK11-2.0.0.jar`

2) Run: `curl -v GET "http://localhost:9090/healthcare/surgery"`

3) Run: `curl -v GET "URL_TO_RUN in Deployed APIs/mohamed" -w "\n"`

4) Example: `curl -v GET "http://localhost:8290/healthcare/querydoctor/surgery" -w "\n"`

5) Run: `curl -v POST --data @PatientExample.json "http://localhost:8290/healthcare/categories/ent/reserve" --header "Content-Type: application/json" -w "\n"`

6) To test the Data Mapper Run this: `curl -v POST --data @PatientClient.json "http://localhost:8290/healthcare/categories/ent/reserve" --header "Content-Type: application/json" -w "\n"`

7) To check Sequence Template Run: `curl -v POST --data @PatientExample.json "http://localhost:8290/healthcare/categories/ent/reserve" --header "Content-Type: application/json" -w "\n"`

# RabbitMQ

1) Go to: https://rabbitmq.com/download.html

2) Run: `sudo docker run -it --rm --name rabbitmq -p 5672:5672 -p 15672:15672 rabbitmq:3.12-management`

3) Open: http://localhost:15672/ --> default user/password: guest/guest
