# notification-service
This is a Notification Service project built using Java, Spring Boot, and Maven as part of the intern assignment. The project provides RESTful API endpoints to send and retrieve notifications for users via Email, SMS, and In-App channels. It includes two main APIs: POST /notifications to send a notification and GET /users/{id}/notifications to retrieve a user’s notification history. The service is designed with asynchronous processing using RabbitMQ and includes a retry mechanism for failed notifications. The tech stack includes Java 17, Spring Boot 3.x, Maven, RabbitMQ for message queuing, and H2 (or MySQL) as the database. To set up the project, first clone the repo using git clone https://github.com/your-username/notification-service.git && cd notification-service. Then configure your application.yml or application.properties in src/main/resources with the following sample:
spring:
  datasource:
    url: jdbc:h2:mem:notificationdb
    username: sa
    password:
  jpa:
    hibernate.ddl-auto: update
    show-sql: true

rabbitmq:
  host: localhost
  port: 5672
  username: guest
  password: guest
Ensure RabbitMQ is running on your local machine. You can quickly start it with Docker using: docker run -d --hostname my-rabbit --name some-rabbit -p 5672:5672 -p 15672:15672 rabbitmq:3-management. Then build the project using mvn clean install and run it using mvn spring-boot:run. The app will be accessible at http://localhost:8080. For sending a notification, use the endpoint POST /notifications with a JSON body like:
{
  "userId": 1,
  "type": "EMAIL",
  "content": "Your order has been confirmed."
}
To fetch notifications, use: GET /users/1/notifications. The system assumes user data management is handled externally and accepts only userId in requests. Email and SMS sending are mocked/simulated for demo purposes, while In-App notifications are stored in the database. The retry mechanism uses RabbitMQ with logic for redelivery and dead-lettering. For development and testing, H2 is the default database, which can be swapped with MySQL by changing the JDBC URL. Future improvements can include Swagger documentation, authentication support, a frontend UI, integration tests, and monitoring tools. The project follows a clean package structure under com.example.notification with controller, service, model, repository, and config packages. This README documents the full setup and assumptions. For any contributions or enhancements, feel free to fork the repo or submit pull requests. This completes the backend notification system as required in the intern assignment using Spring Boot and Java development skills.
Project Structure
css
Copy
Edit
src/
├── main/
│   ├── java/
│   │   └── com.example.notification
│   │       ├── controller/
│   │       ├── service/
│   │       ├── model/
│   │       ├── repository/
│   │       └── config/
│   └── resources/
│       └── application.yml
 To Do (Improvements)
Add Swagger/OpenAPI documentation
Add authentication/authorization layer
UI to view in-app notifications
Integration tests with embedded RabbitMQ
Monitoring with Prometheus/Grafana

Author
Ayush Kumar
Java Backend Developer 
