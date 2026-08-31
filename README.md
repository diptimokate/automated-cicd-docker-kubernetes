## **Automated CI/CD Pipeline with Docker and Kubernetes**

## **End-to-End DevOps Automation using GitHub, Jenkins, Maven, Ansible, Docker, DockerHub and Kubernetes**

# **1\. Project Overview**

This project demonstrates an end-to-end DevOps automation workflow for building, containerizing, and deploying a web application using GitHub, Jenkins, Maven, Ansible, Docker, DockerHub, and Kubernetes.

The application source code is created by the developer and pushed to GitHub. Jenkins automates the CI/CD stages, including pulling the application source code, testing and building the application using Maven, transferring required files to the Ansible server, building the Docker image, pushing the image to DockerHub, and deploying the application on Kubernetes.

Ansible is used to automate operations between the Docker and Kubernetes environments. Docker is used to containerize the application, while DockerHub stores the container image.

Finally, Kubernetes pulls the application image from DockerHub, creates the application Pods through a Deployment, exposes the application using a Service, and makes the application accessible through the configured service endpoint.

# **2\. Objectives**

- Automate application deployment using Jenkins.
- Store application source code in GitHub.
- Pull application source code automatically using Jenkins.
- Test and build the application using Maven.
- Transfer required application and deployment files to the Ansible server.
- Automate server operations using Ansible.
- Build a Docker image from the application.
- Push the Docker image to DockerHub.
- Deploy the application on Kubernetes.
- Create and manage application Pods using a Kubernetes Deployment.
- Expose the application using a Kubernetes Service.
- Verify the Kubernetes Deployment, Pods, and Service.
- Access the application through the Kubernetes Service.

# **3\. Prerequisites**

## **Accounts & Access**

- AWS account for creating and managing the Kubernetes environment.
- GitHub account for storing the application source code.
- DockerHub account with a repository created.
- Access to Developer, Jenkins, Ansible, Docker, and Kubernetes servers.
- SSH connectivity between the required servers.

## **Tools Installed**

### Developer Server

- Git
- Application source code
- Required project files

### Jenkins Server

- Jenkins
- Git
- Maven
- Required Jenkins plugins
- Docker access or connectivity to the Docker environment

### Ansible Server

- Ansible
- SSH access to Docker and Kubernetes environments
- Ansible inventory and playbooks

### Docker Server

- Docker
- DockerHub credentials
- Dockerfile and application files

### Kubernetes Environment

- Kubernetes Cluster
- kubectl
- Deployment YAML file
- Service YAML file

# **4\. Architecture**

Developer

↓

GitHub

↓

Jenkins Server

↓

+--------------------+

↓ ↓

Job 1 Job 2

Pull Code Test / Build

↓ ↓

+-------|------------+

↓

Ansible Server

↓

Docker Server

↓

DockerHub

↓

Kubernetes Cluster

↓

Deployment + Service

↓

Browser

# **5\. Technologies & Architecture Components**

| **Sr. No.** | **Component**         | **Role**                                            |
| ----------- | --------------------- | --------------------------------------------------- |
| 1           | Git                   | Version control                                     |
| 2           | GitHub                | Source code repository                              |
| 3           | Jenkins               | Automates CI/CD pipeline                            |
| 4           | Maven                 | Tests and builds the application                    |
| 5           | Ansible               | Automates server configuration and deployment tasks |
| 6           | Docker                | Containerizes the application                       |
| 7           | DockerHub             | Stores the Docker image                             |
| 8           | Kubernetes            | Container orchestration                             |
| 9           | Kubernetes Deployment | Creates and manages application Pods                |
| 10          | Kubernetes Service    | Exposes the application                             |
| 11          | Dockerfrile           | Defines the Docker images creation                  |
| 12          | Kuberenetes YAML      | Defines application deployment configuration        |
| 13          | Nginx                 | Web server / container base image                   |
| 14          | HTML                  | Web application                                     |
| 15          | Linux                 | Server operating system                             |

# **6\. Project Flow**

The complete project flow is:

Developer  
↓  
Create Application Files  
↓  
Push Files to GitHub  
↓  
Jenkins  
↓  
Pull Application Code  
↓  
Test and Build Application using Maven  
↓  
Transfer Files to Ansible Server  
↓  
Ansible Automation  
↓  
+------------------------+  
↓ ↓  
Docker Server Kubernetes Cluster  
↓  
Build Docker Image  
↓  
Push Image to DockerHub  
↓  
Kubernetes Pulls Image  
↓  
Create Deployment  
↓  
Create Application Pods  
↓  
Create Kubernetes Service  
↓  
Access Application

# **7\. Jenkins Pipeline / Jobs**

The project uses Jenkins to automate five different stages.

## **Job 1 — Pull Application Code**

Jenkins pulls the latest application source code from GitHub.

GitHub -> Jenkins -> Jenkins Workspace

The application source code is stored in the Jenkins workspace after successful execution.

## **Job 2 — Test and Build Application**

Jenkins uses Maven to test and build the application.

Example commands:

mvn clean test  
mvn clean package

Workflow:

Application Source Code -> Maven Test -> Maven Build -> Application Artifact

## **Job 3 — Transfer Files to Ansible Server**

Jenkins transfers the required files to the Ansible server.

The files may include:

- Application files
- Dockerfile
- Ansible playbooks
- Kubernetes Deployment YAML file
- Kubernetes Service YAML file

Workflow:

Jenkins -> Application / Deployment Files -> Ansible Server

## **Job 4 — Build and Push Docker Image**

Jenkins automates the Docker image build and push process.

Workflow:

Application Source Code -> Dockerfile -> Docker Build -> Docker Image -> DockerHub

Example:

docker build -t &lt;dockerhub-username&gt;/&lt;repository-name&gt;:latest .

docker push &lt;dockerhub-username&gt;/&lt;repository-name&gt;:latest

## **Job 5 — Deploy Application on Kubernetes**

The final Jenkins job triggers the application deployment process.

Workflow:

DockerHub -> Application Image -> Jenkins -> Kubernetes -> Deployment -> Pods -> Service

Kubernetes pulls the application image from DockerHub and deploys it to the cluster.

# **8\. Ansible Automation**

The Ansible server is used to automate operations between the different environments.

Ansible connects to:

- Docker Server
- Kubernetes Control Plane
- Kubernetes Worker Nodes

Ansible automates the required remote operations, including application deployment-related tasks.

Workflow:

Ansible Server  
↓  
+-------------------------+  
↓ ↓  
Docker Server Kubernetes Cluster  
↓ ↓  
Build Docker Image Deploy Application

# **9\. Docker & DockerHub**

Docker is used to containerize the application.

Docker performs:

- Reading the Dockerfile.
- Building the Docker image.
- Tagging the Docker image.
- Pushing the image to DockerHub.

Example:

docker build -t &lt;dockerhub-username&gt;/&lt;repository-name&gt;:latest .

Push the image:

docker login  
docker push &lt;dockerhub-username&gt;/&lt;repository-name&gt;:latest

DockerHub acts as the centralized container image registry.

The Kubernetes cluster pulls the application image from DockerHub during deployment.

# **10\. Kubernetes Deployment**

The Kubernetes environment consists of:

- Control Plane / Master Node
- Worker Node(s)

The Kubernetes Deployment YAML file is used to create and manage the application Pods.

The Deployment defines:

- Application name
- Number of replicas
- Docker image
- Container configuration
- Labels

Apply the Deployment:

kubectl apply -f deployment.yml

Verify the Pods:

kubectl get pods

Verify the Deployment:

kubectl get deployment

# **11\. Kubernetes Service**

The Kubernetes Service YAML file is used to expose the application.

The Service defines:

- Service name
- Service type
- Application selector
- Port
- Target port

Apply the Service:

kubectl apply -f service.yml

Verify the Service:

kubectl get svc

# **12\. Application Deployment & Access**

The complete Kubernetes deployment flow is:

DockerHub Image  
↓  
Kubernetes Deployment  
↓  
Application Pods  
↓  
Kubernetes Service  
↓  
Browser Access

After the Deployment and Service are created successfully, the application becomes accessible through the Kubernetes Service.

For a NodePort service:

http://&lt;WORKER_PUBLIC_IP&gt;:&lt;NODEPORT&gt;

For a LoadBalancer service, access the application using the LoadBalancer endpoint and configured port.

# **13\. How to Deploy**

## **Step 1 — Clone the Repository**

git clone <https://github.com/&lt;your-username&gt;/&lt;your-repository&gt;.git>  
cd &lt;your-repository&gt;

## **Step 2 — Configure GitHub, DockerHub and Jenkins Credentials**

Configure the required credentials in Jenkins.

Example credentials:

- GitHub credentials
- DockerHub credentials
- SSH credentials for server connectivity

## **Step 3 — Run Job 1: Pull Application Code**

Jenkins pulls the latest application source code from GitHub.

GitHub -> Jenkins Workspace

## **Step 4 — Run Job 2: Test and Build Application**

Jenkins uses Maven:

mvn clean test  
mvn clean package

## **Step 5 — Run Job 3: Transfer Files to Ansible**

Jenkins transfers the required application and deployment files to the Ansible server.

## **Step 6 — Run Job 4: Build and Push Docker Image**

Build the Docker image:

docker build -t &lt;dockerhub-username&gt;/&lt;repository-name&gt;:latest .

Push the Docker image:

docker push &lt;dockerhub-username&gt;/&lt;repository-name&gt;:latest

## **Step 7 — Verify Kubernetes Cluster**

Check the Kubernetes nodes:

kubectl get nodes

The nodes should be in the Ready state.

## **Step 8 — Deploy the Application**

Apply the Kubernetes Deployment:

kubectl apply -f deployment.yml

Apply the Kubernetes Service:

kubectl apply -f service.yml

## **Step 9 — Verify Deployment**

Check the Pods:

kubectl get pods

Check the Deployment:

kubectl get deployment

Check the Service:

kubectl get svc

## **Step 10 — Access the Application**

Use the Kubernetes Service endpoint.

For NodePort:

http://&lt;WORKER_PUBLIC_IP&gt;:&lt;NODEPORT&gt;

For LoadBalancer:

http://&lt;LOADBALANCER-ENDPOINT&gt;:&lt;PORT&gt;

#

# **14\. Final Result**

The project successfully demonstrates an end-to-end automated DevOps deployment workflow.

The final workflow integrates:

Developer -> Git -> GitHub -> Jenkins -> Maven -> Ansible -> Docker -> DockerHub -> Kubernetes -> Deployment -> Pods -> Service -> Browser

The final application is containerized using Docker, stored in DockerHub, deployed on Kubernetes, and exposed through a Kubernetes Service.

This project demonstrates practical implementation of:

- Source Code Management
- Continuous Integration
- CI/CD Automation
- Application Testing and Build Automation
- Configuration Management
- Server Automation
- Containerization
- Docker Image Management
- Container Image Registry
- Kubernetes Deployment
- Kubernetes Service Management
- Container Orchestration
- Automated Application Deployment