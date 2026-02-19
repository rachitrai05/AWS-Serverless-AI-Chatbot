# 🚀 Project Setup Guide

This document explains how to set up the required AWS resources for the project.

---

# 1️⃣ DynamoDB Setup

Create the required DynamoDB tables:

### 📌 Create table `conversation_data`

1. Go to **AWS Console → DynamoDB → Tables**
2. Click **Create table**
3. Configure:

   * **Table name:** `conversation_data`
   * **Partition key:** `conversationId`
4. Click **Create**

---

### 📌 Create table `user-data`

1. Go to **AWS Console → DynamoDB → Tables**
2. Click **Create table**
3. Configure:

   * **Table name:** `user-data`
   * **Partition key:** `userId`
4. Click **Create**

---

# 2️⃣ Lambda Setup

Create the following Lambda functions.

> ✅ Runtime for all functions: **Python 3.14**

For each function:

* Go to **AWS Console → Lambda → Create Function**
* Choose **Author from scratch**
* Set function name
* Select **Python 3.14**
* Click **Create Function**
* Paste the respective code file
* Click **Deploy**
* Go to **Configuration → Permissions**
* Add **least-privilege inline policy** (Refer to `inline-policies.txt`)

---

### 🔹 1. ModelInvokation

* Code file: `model-nvocation.py`

### 🔹 2. generate-conversation-id

* Code file: `generate-conversation-id.py`

### 🔹 3. get-conversation-history

* Code file: `history.py`

### 🔹 4. login

* Code file: `login.py`

### 🔹 5. register

* Code file: `register.py`

---

# 3️⃣ API Gateway Setup

You need to create **two REST APIs**:

* BedRockInvoke API
* loginRegister API

---

# 🔷 A. Create Conversation API

### Step 1: Create API

1. Go to **AWS Console → API Gateway**
2. Click **Create API**
3. Select **REST API**
4. Configure:

   * **API Name:** `BedRockInvoke`
   * **Description:** Conversation-related APIs
   * **Security Policy:** `SecurityPolicy_TLS13_1_2_2021_06`
5. Click **Create API**
6. Enable **CORS**

---

## Create Resources & Methods

### 🔹 1. `bedRockInvoke`

* Create Resource:

  * Resource name: `bedRockInvoke`
  * Enable CORS
* Create Method:

  * Method: `POST`
  * Integration type: `Lambda Function`
  * Select `model-invocation`

---

### 🔹 2. `history`

* Create Resource:

  * Resource name: `history`
  * Enable CORS
* Create Method:

  * Method: `POST`
  * Integration type: `Lambda Function`
  * Select `history`

---

## Deploy Conversation API

1. Select `/` and all created resources
2. Enable **CORS** (Allow all checkboxes)
3. Click **Deploy API**
4. Note the **Invoke URL**

---

# 🔷 B. Create loginRegister API

### Step 1: Create API

1. Go to **AWS Console → API Gateway**
2. Click **Create API**
3. Select **REST API**
4. Configure:

   * **API Name:** `loginRegister`
   * **Description:** Authentication-related APIs
   * **Security Policy:** `SecurityPolicy_TLS13_1_2_2021_06`
5. Click **Create**
6. Enable **CORS**

---

## Create Resources & Methods

### 🔹 1. `login`

* Create Resource:

  * Resource name: `login`
  * Enable CORS
* Create Method:

  * Method: `POST`
  * Integration type: `Lambda Function`
  * Select `login`

---

### 🔹 2. `register`

* Create Resource:

  * Resource name: `register`
  * Enable CORS
* Create Method:

  * Method: `POST`
  * Integration type: `Lambda Function`
  * Select `register`

---

### 🔹 3. `generateConvoId`

* Create Resource:

  * Resource name: `generateConvoId`
  * Enable CORS
* Create Method:

  * Method: `POST`
  * Integration type: `Lambda Function`
  * Select `generate-conversation-id`

---

## Deploy Auth API

1. Select `/` and all created resources
2. Enable **CORS** (Allow all checkboxes)
3. Click **Deploy API**
4. Note the **Invoke URL**

---

# 4️⃣ Environment 

1. Copy all **Invoke URLs** from deployed APIs.
2. Add them to your `index.html` file under `<Script> section`with the correct paths.
3. Verify endpoints are correctly mapped.

✅ Your APIs are now ready to use!