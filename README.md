# CloudMart - Multi-Cloud E-Commerce Platform



## Overview



CloudMart is a multi-cloud e-commerce platform designed to showcase the deployment and integration of various cloud services and AI technologies. This project utilizes resources and services across **AWS, Google Cloud Platform (GCP), and Azure**, demonstrating a comprehensive approach to cloud computing.



## Key Features



*   **Multi-Cloud Deployment:**

    *   **AWS:** Serves as the primary infrastructure provider, hosting core services such as:

        *   **S3 buckets** for storage.

        *   **DynamoDB tables** for database management.

        *   **Lambda functions** for serverless computing.

        *   **CodePipeline and CodeBuild** for CI/CD.

        *   **EKS (Elastic Kubernetes Service)** for container orchestration.

    *   **Google Cloud Platform (GCP):** Leveraged for data warehousing and analytics through **BigQuery**.

    *   **Azure:** Utilized for sentiment analysis using **Text Analytics** services.



*   **AI Integration:**

    *   **Amazon Bedrock:** Integrated for product recommendations using the Claude 3 Sonnet model.

    *   **OpenAI:** Used for customer support functionalities.



*   **CI/CD Pipeline:**

    *   **AWS CodePipeline and CodeBuild** automate the build, testing, and deployment of application code changes to Kubernetes.

    *   Automated pipeline triggered by changes to the GitHub repository.



*   **Infrastructure as Code (Terraform):**

    *   **Terraform** is used to define and manage the infrastructure required for the application.

    *   Automates the creation, modification, and deletion of AWS resources, ensuring consistency and repeatability across different environments.



*   **Containerization and Orchestration:**

    *   **Docker** is used to containerize the application.

    *   **Kubernetes (EKS)** is used for orchestrating the deployment and management of the containers.



## Architecture



The CloudMart platform is designed with a microservices architecture, comprising both frontend and backend components.



*   **Frontend:**

    *   Developed using modern JavaScript frameworks.

    *   Containerized using Docker and deployed on Kubernetes.

    *   Utilizes a CI/CD pipeline for automated deployment of updates.

*   **Backend:**

    *   Developed using Node.js.

    *   Integrates with DynamoDB for data storage and retrieval.

    *   Connects to Amazon Bedrock and OpenAI for AI-driven functionalities.

    *   Includes Lambda functions for serverless computing.

    *   Uses a CI/CD pipeline for automated deployment.

*   **Data Analytics:**

    *   **BigQuery** is used for analyzing order data to gain insights into customer behavior and sales trends.

*   **Sentiment Analysis:**

    *   **Azure Text Analytics** is employed to analyze customer reviews and feedback to gauge sentiment.



## Setup and Deployment



### Prerequisites



*   AWS Account

*   Google Cloud Account

*   Azure Account

*   Terraform

*   Docker

*   Kubernetes (kubectl, eksctl)

*   GitHub Account



### Steps



1.  **AWS Setup:**

    *   Configure AWS credentials.

    *   Create an EKS cluster using `eksctl`.

    *   Set up IAM roles and policies for EC2, Lambda, and CodeBuild.

2.  **Terraform Configuration:**

    *   Initialize Terraform and apply the configuration to create AWS resources.

        ```bash

        terraform init

        terraform apply

        ```

3.  **GCP Setup:**

    *   Create a Google Cloud project.

    *   Enable the BigQuery API.

    *   Create a BigQuery dataset and table.

    *   Create a service account with the "BigQuery Data Editor" role.

4.  **Azure Setup:**

    *   Create an Azure account and set up a Text Analytics resource.

    *   Obtain the endpoint URL and API key.

5.  **CI/CD Pipeline Configuration:**

    *   Create a GitHub repository for the CloudMart application.

    *   Configure AWS CodePipeline and CodeBuild to build and deploy the application.

    *   Connect CodeBuild to the GitHub repository.

    *   Set up environment variables in CodeBuild, including ECR repository URI.

6.  **Application Deployment:**

    *   Build Docker images for the frontend and backend.

    *   Push the Docker images to ECR repositories.

    *   Deploy the application to Kubernetes using `kubectl apply`.

        ```bash

        kubectl apply -f cloudmart-backend.yaml

        kubectl apply -f cloudmart-frontend.yaml

        ```



## AI Assistant Configuration



### Amazon Bedrock Agent



1.  Enable model access for Claude 3 Sonnet in the Amazon Bedrock console.

2.  Create a new agent named "cloudmart-product-recommendation-agent".

3.  Select "Claude 3 Sonnet" as the base model.

4.  Provide instructions for the agent to recommend products.

5.  Configure the IAM role to allow the agent to invoke the Lambda function.

6.  Create an action group named "Get-Product-Recommendations".

7.  Set the action group type as "Define with API schemas".

8.  Select the Lambda function "cloudmart-list-products" as the action group executor.

9.  Define the API schema in the inline schema editor.

10. Prepare and test the agent.

11. Create an alias for the agent.



### OpenAI Assistant



1.  Access the OpenAI platform and create a new assistant.

2.  Name the assistant "CloudMart Customer Support" and select the gpt-4o model.

3.  Provide instructions for the assistant to provide customer support.

4.  Enable "Code Interpreter" if needed.

5.  Generate an API key.



## Cleaning Up



To avoid unwanted charges, delete all resources after completing the hands-on exercise:



```bash

kubectl delete service cloudmart-frontend-app-service

kubectl delete deployment cloudmart-frontend-app

kubectl delete service cloudmart-backend-app-service

kubectl delete deployment cloudmart-backend-app

eksctl delete cluster --name cloudmart --region us-east-1
