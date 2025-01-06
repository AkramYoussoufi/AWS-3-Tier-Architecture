
# Multi-Tier Application on AWS

This project demonstrates a multi-tier application architecture deployed on Amazon Web Services (AWS). The architecture consists of three tiers:

- **Frontend (Nginx):** Handles incoming requests and distributes traffic to the backend.
- **Backend (Tomcat):** Hosts the application logic and serves dynamic content.
- **Database (MySQL RDS):** Stores and retrieves application data.

---

## Project Components

### 1. VPC and Networking

- **VPCs:** Two separate VPCs are created to enhance security and isolation.
- **Subnets:** Public and private subnets are defined within each VPC. Public subnets host internet-facing resources like the bastion host and Nginx. Private subnets house the backend servers and database.
- **NAT Gateway:** Enables outbound internet access for instances in the private subnets.
- **Internet Gateway:** Provides internet connectivity for the public subnet.
- **Transit Gateway:** Facilitates communication between the two VPCs.
- **Route Tables:** Define traffic routing rules within each VPC.

### 2. Bastion Host

- **Purpose:** Provides secure SSH access to instances in the private subnets.
- **Security:** Configured with restrictive security groups allowing SSH access only from specific IP addresses.

### 3. Golden AMIs

- **Nginx AMI:** A custom AMI pre-configured with Nginx, CloudWatch agent, and other necessary software.
- **Tomcat AMI:** A custom AMI pre-configured with Apache Tomcat, Java, and CloudWatch agent.
- **Maven AMI:** A custom AMI pre-configured with Maven, Git, and JDK for building and deploying the application.

### 4. Build and Deployment

- **Maven Build:** The application is built using Maven on the Maven AMI.
- **SonarCloud Integration:** Static code analysis is performed using SonarCloud to ensure code quality.
- **JFrog Artifact Repository:** Build artifacts (JAR files) are stored in a JFrog Cloud repository.
- **Deployment Scripts:** User data scripts are used to automate the deployment of application artifacts to Tomcat instances during launch.

### 5. Load Balancing and Auto Scaling

- **Network Load Balancer:** Distributes traffic across multiple Nginx and Tomcat instances for high availability and scalability.
- **Auto Scaling Groups:** Automatically adjust the number of instances based on traffic demand, ensuring optimal resource utilization.

### 6. Database

- **MySQL RDS:** A managed relational database service provides high availability, scalability, and security for the application data.

### 7. Monitoring and Logging

- **CloudWatch:** Monitors key metrics like CPU utilization, memory usage, and database connections.
- **CloudWatch Alarms:** Triggers alerts based on predefined thresholds, such as high CPU usage or low disk space.
- **Log Aggregation:** Tomcat logs are collected and stored in an S3 bucket for analysis and troubleshooting.

### 8. Security

- **Security Groups:** Restrict inbound and outbound traffic to specific ports and IP addresses, minimizing the attack surface.
- **IAM Roles:** Grant least privilege access to AWS services, reducing the risk of unauthorized access.

### 9. Validation and Testing

- **Application Testing:** Thoroughly test the application's functionality, performance, and security.
- **End-to-End Testing:** Verify that the entire system works as expected, from the frontend to the backend and database.

### 10. Continuous Integration/Continuous Delivery (CI/CD)

- **Automation:** Implement CI/CD pipelines to automate the build, test, and deployment processes, enabling faster development and deployment cycles.
