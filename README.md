# AWS Cloud for Web App Setup Lift & Shift
![AWS Lift Shift project](https://github.com/user-attachments/assets/0203e9d7-bd15-403e-860b-919c0a62558d)

## Overview

This project demonstrates the deployment of a Java-based web application using AWS services. The application is built locally and deployed on AWS using a Lift & Shift approach. The project infrastructure is designed for high availability, scalability, and security.

## Architecture

The architecture consists of the following components:

- **DNS (GoDaddy & Route 53):** The domain is managed by GoDaddy, pointing to the Application Load Balancer (ALB) endpoint via DNS zones. Internal DNS routing is handled by Amazon Route 53 private zones.
  
- **Application Load Balancer (ALB):** Manages incoming traffic and distributes it across multiple Tomcat instances running in an Auto Scaling group. The ALB is secured with an SSL certificate generated by AWS Certificate Manager (ACM).

- **Tomcat Instances:** Hosts the Java application, with instances managed under an Auto Scaling group for automatic scaling.

- **Amazon S3:** Stores the application build artifacts. The Tomcat servers fetch the application from S3 during deployment.

- **Security Groups:** Enforces security rules across the different components, ensuring controlled access to the application.

- **Amazon Route 53:** Manages DNS routing, including both public and private DNS zones.

- **Backend Instances:** The backend consists of Memcache, RabbitMQ, and MySQL instances, each residing in a separate security group for isolation and security.

## Deployment Workflow

1. **Build Locally:** The Java application is built locally using Maven.
   ```bash
   mvn clean install
   ```

2. **Upload to S3:** After a successful build, the application artifact (e.g., WAR or JAR file) is uploaded to an S3 bucket.
   ```bash
   aws s3 cp target/myapp.war s3://my-bucket/myapp.war
   ```

3. **Fetch from S3:** The Tomcat application servers fetch the application artifact from the S3 bucket during deployment.

4. **Deploy the Application:** The application is deployed on Tomcat instances, which are automatically scaled based on load.

## Prerequisites

- AWS Account with necessary IAM permissions.
- A domain registered with GoDaddy (or any other DNS provider).
- Java Development Kit (JDK) installed locally.
- Maven installed locally for building the project.
- SSL Certificate generated by AWS Certificate Manager (ACM).


## Security Considerations

- Ensure that the S3 bucket has the necessary policies to allow access only to the application servers.
- Use HTTPS for all external communication, secured by the ACM-generated SSL certificate.
- Regularly update security group rules to minimize exposure.

## Conclusion

This project provides a robust and scalable deployment strategy for a Java-based application using AWS services. By leveraging AWS, the application benefits from high availability, security, and automatic scaling.

## Snaps
![Screenshot 2024-08-19 201801](https://github.com/user-attachments/assets/cfe079a1-fa5c-4d22-8ee5-f9f3dbe3408a)

![Screenshot 2024-08-19 201826](https://github.com/user-attachments/assets/407fe7e6-16b2-4d3e-97bc-2a700e2b8a47)

---
