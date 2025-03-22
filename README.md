# Serverless-File-Sharing-Management
A serverless file-sharing system that enables users to upload and retrieve files using a REST API.

---

# **Serverless File Sharing Platform**  
![image](https://github.com/user-attachments/assets/2004fec9-eb8b-4ef1-b7f8-45e87ac1cc20)

## **Introduction**  

This project demonstrates a **serverless file-sharing system** that enables users to upload and retrieve files using a **REST API**. The solution is built on **AWS Lambda** for event-driven computing, **API Gateway** for managing API requests, and **Amazon S3** for secure and scalable storage. Users can interact with the API using tools like **Postman** or **cURL**, making it flexible for various use cases.  

## **Potential Use Cases**  

✔️ **File Sharing:** Users can upload and share files seamlessly via HTTP requests.  
✔️ **Content Delivery:** Creators can distribute digital assets such as documents, software, and media files.  
✔️ **Team Collaboration:** Teams can use the platform for secure, remote file access and collaboration.  

## **Architecture Overview**  




## **Implementation Steps**  

### **Step 1: Set Up an S3 Bucket**  
- Create an **S3 bucket** (e.g., `serverless-file-bucket`) for storing uploaded files.  

### **Step 2: Develop a Lambda Function for File Uploads**  
- **Function Name:** `FileUploadHandler`  
- **Runtime:** Python 3.x  
- **IAM Role:** Grant permissions to write files to S3  
- **Purpose:** Accepts file data and stores it in S3.  

### **Step 3: Develop a Lambda Function for File Retrieval**  
- **Function Name:** `FileDownloadHandler`  
- **Runtime:** Python 3.x  
- **IAM Role:** Grant permissions to read files from S3  
- **Purpose:** Fetches files based on user requests.  

### **Step 4: Configure API Gateway**  
- **API Name:** `serverless-file-api`  
- Define a **/files** resource with two methods:  
  - `POST` → Linked to `FileUploadHandler`  
  - `GET` → Linked to `FileDownloadHandler`  

### **Step 5: Modify API Request Handling**  

#### ✅ **Configuring the GET Method (Download Files)**  
- **Request Validation:** Enable query string parameter validation.  
- **Mapping Template for Input Transformation:**  

```json
{
  "queryStringParameters": {
    "fileName": "$input.params('fileName')"
  }
}
```

#### ✅ **Configuring the POST Method (Upload Files)**  
- **Request Validation:** Process request body and filename as input parameters.  
- **Mapping Template for Input Transformation:**  

```json
{
  "body": "$input.body",
  "queryStringParameters": {
    "fileName": "$input.params('fileName')"
  }
}
```

### **Step 6: Deploy API Gateway**  
- Publish the API to a designated stage (e.g., `production`).  
- Navigate to **Actions** > **Deploy API** and select the `production` stage.  

## **Testing the API**  

### **Uploading a File**  

#### **Using Postman:**  
- **Method:** `POST`  
- **URL:** `https://<api-id>.execute-api.<region>.amazonaws.com/production/files?fileName=sample.txt`  
- **Headers:** `Content-Type: text/plain`  
- **Body:** Enter text content (e.g., `Hello Serverless World!`) and send the request.  

#### **Using cURL:**  

```sh
curl --location 'https://<api-id>.execute-api.<region>.amazonaws.com/production/files?fileName=sample.txt' \
--header 'Content-Type: text/plain' \
--data 'Hello from the serverless platform!'
```

### **Downloading a File**  

#### **Using Postman:**  
- **Method:** `GET`  
- **URL:** `https://<api-id>.execute-api.<region>.amazonaws.com/production/files?fileName=sample.txt`  

#### **Using cURL:**  

```sh
curl --location 'https://<api-id>.execute-api.<region>.amazonaws.com/production/files?fileName=sample.txt'
```

## **Key Benefits of This Approach**  

🚀 **Scalability:** Automatically handles fluctuating workloads.  
💰 **Cost-Efficient:** Pay only for actual resource usage.  
🔒 **Security:** AWS IAM controls protect file access.  
⚡ **No Server Management:** Fully managed serverless setup.  

## **Final Thoughts**  

This **lightweight, cloud-native file-sharing solution** leverages AWS **Lambda, API Gateway, and S3** to provide a **secure, scalable, and cost-effective** approach to managing file uploads and downloads. By following this guide, you can set up your own **serverless file-sharing service** efficiently.  

---  
