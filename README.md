<img width="1918" height="907" alt="Screenshot 2026-04-20 175906" src="https://github.com/user-attachments/assets/b1449cba-9671-49b1-8887-9fc62caa287c" /><img width="1918" height="907" alt="Screenshot 2026-04-20 175906" src="https://github.com/user-attachments/assets/aff73794-3abb-4b87-8f20-289857607fc9" /><img width="1446" height="832" alt="Screenshot 2026-04-20 175617" src="https://github.com/user-attachments/assets/decd2fdc-67f4-47fe-858b-5f53c14af45e" /># 🚀 Serverless Orders API (AWS)

A fully serverless REST API for managing orders using AWS services. This project implements complete CRUD operations using API Gateway, Lambda, and DynamoDB.

---

## 🧠 Architecture

Client → Amazon API Gateway → AWS Lambda → Amazon DynamoDB

---

## ⚙️ Services Used

* Amazon API Gateway (REST API)
* AWS Lambda (Python)
* Amazon DynamoDB (NoSQL Database)
* AWS IAM (Permissions)
* Amazon CloudWatch (Logs & Debugging)

---

## 📂 API Endpoints

| Method | Endpoint | Description        |
| ------ | -------- | ------------------ |
| GET    | /orders  | Get all orders     |
| POST   | /orders  | Create a new order |
| PUT    | /orders  | Update an order    |
| DELETE | /orders  | Delete an order    |

---

## 🗄️ DynamoDB Table Design

Table Name: Orders

* Partition Key: orderId (String)
* Sort Key: timestamp (String)

This allows efficient querying and sorting.

---

## 🔧 Step-by-Step Implementation

### 1. Create DynamoDB Table

* Go to AWS Console → DynamoDB
* Create table:

  * Table name: Orders
  * Partition key: orderId
  * Sort key: timestamp
 
    <img width="1919" height="906" alt="Screenshot 2026-04-20 164054" src="https://github.com/user-attachments/assets/213bf7c1-350a-446e-892a-407cf0403f32" />


<img width="1918" height="907" alt="Screenshot 2026-04-20 164111" src="https://github.com/user-attachments/assets/7137410e-eea1-46d4-94d0-cd79ce1ec895" />

---

### 2. Create IAM Role

* Go to IAM → Roles → Create Role
* Select Lambda service
* Attach policies:

  * AmazonDynamoDBFullAccess
  * AWSLambdaBasicExecutionRole
 
    <img width="1918" height="910" alt="Screenshot 2026-04-20 164417" src="https://github.com/user-attachments/assets/55afdb66-adc1-45b1-a32b-0776340862a3" />


---

### 3. Create Lambda Functions

Create 4 Lambda functions:

* createOrder
* getOrders
* updateOrder
* deleteOrder

Runtime: Python 3.x
Attach IAM role created earlier

---

### 4. Implement Lambda Functions

#### createOrder

* Accepts JSON input
* Generates UUID and timestamp
* Stores data in DynamoDB

<img width="1917" height="902" alt="Screenshot 2026-04-20 164525" src="https://github.com/user-attachments/assets/33f6111c-cfd8-41be-8fe7-37c05cef1c3a" />
  

#### getOrders

* Fetches all items using scan()

<img width="1919" height="883" alt="Screenshot 2026-04-20 164851" src="https://github.com/user-attachments/assets/52347548-7dcf-424f-bc70-d8e4bfeb108d" />
  

#### updateOrder

* Updates item using update_item()
* Uses ExpressionAttributeNames to avoid reserved keywords

#### deleteOrder

* Deletes item using orderId + timestamp

  <img width="1907" height="919" alt="Screenshot 2026-04-20 165029" src="https://github.com/user-attachments/assets/7fe31964-b074-4d7b-8366-39edf788da3e" />


---

### 5. Create API Gateway

* Create REST API
* Endpoint type: Regional

  <img width="1919" height="910" alt="Screenshot 2026-04-20 165330" src="https://github.com/user-attachments/assets/a8e6ac01-88ac-4783-8ef0-739ee9e4e2e8" />


---

### 6. Create Resource

* Create resource: `/orders`

<img width="1916" height="905" alt="Screenshot 2026-04-20 165553" src="https://github.com/user-attachments/assets/890627b3-62b4-483f-8320-dddbfd067f9d" />

---

### 7. Add Methods

| Method | Lambda Function |
| ------ | --------------- |
| GET    | getOrders       |
| POST   | createOrder     |
| PUT    | updateOrder     |
| DELETE | deleteOrder     |

Enable Lambda Proxy Integration for all methods.

<img width="1919" height="881" alt="Screenshot 2026-04-20 173454" src="https://github.com/user-attachments/assets/9299a5cf-243d-4c04-8e0b-2bccbf1b7406" />


---

### 8. Enable CORS

* Select `/orders`
* Enable CORS for all methods

---

### 9. Deploy API

* Create stage: `dev`
* Deploy API

<img width="1915" height="919" alt="Screenshot 2026-04-20 173511" src="https://github.com/user-attachments/assets/743666d4-ca56-4ce2-a0d7-3158e7ad1fad" />

---

## 🧪 Testing (Postman)

### Create Order (POST)

```json
{
  "item": "Laptop"
}
```

<img width="1446" height="832" alt="Screenshot 2026-04-20 175617" src="https://github.com/user-attachments/assets/e70ab476-a6b0-4806-8942-8eef5e3e330b" />

###  Get Orders (GET)

GET /orders

👉 Returns all orders from the database.

<img width="1417" height="851" alt="Screenshot 2026-04-20 175802" src="https://github.com/user-attachments/assets/0acaffef-0244-42bd-8e07-7f885711a48c" />


### Update Order (PUT)

```json
{
  "orderId": "your-id",
  "timestamp": "your-timestamp",
  "item": "Mobile"
}
```

<img width="1918" height="907" alt="Screenshot 2026-04-20 175906" src="https://github.com/user-attachments/assets/861ddb9e-8be7-4d75-a8d8-1c5d9f8ab84e" />



### Delete Order (DELETE)

```json
{
  "orderId": "your-id",
  "timestamp": "your-timestamp"
}
```

<img width="1394" height="763" alt="Screenshot 2026-04-20 180235" src="https://github.com/user-attachments/assets/4158745e-b6a6-4d4d-8f9b-7275343f00b3" />

<img width="1918" height="921" alt="Screenshot 2026-04-20 180257" src="https://github.com/user-attachments/assets/c9cb20d9-8463-4f66-80e8-f956b36d7427" />

---


## 📌 Conclusion

This project demonstrates how to build a scalable, cost-effective serverless backend using AWS services with proper API design and error handling.

---

### Author : Suyash Dahitule
