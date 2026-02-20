# 🚀 AI-Powered Chatbot – Serverless AWS Architecture

![AWS](https://img.shields.io/badge/AWS-Serverless-orange?logo=amazonaws)
![Amazon Bedrock](https://img.shields.io/badge/AI-Amazon%20Bedrock-blue)
![DynamoDB](https://img.shields.io/badge/Database-DynamoDB-4053D6?logo=amazondynamodb)
![Lambda](https://img.shields.io/badge/Compute-AWS%20Lambda-FF9900?logo=awslambda)
![API Gateway](https://img.shields.io/badge/API-Gateway-6A5ACD)
![HTML](https://img.shields.io/badge/HTML-5-orange?logo=html5)
![CSS](https://img.shields.io/badge/CSS-3-blue?logo=css3)
![JavaScript](https://img.shields.io/badge/JavaScript-ES6-yellow?logo=javascript)


> A production-style, fully serverless AI chatbot built using AWS services and powered by Amazon Bedrock (Nova Micro model).
> Supports authentication, multi-session conversations, persistent history, and contextual AI responses.

---

## 🌐 Live Demo

🔗 **Frontend URL:**
[Click Here ](http://new-bucket-rach.s3-website-us-east-1.amazonaws.com)

---

## 📚 Documentation

- [Click Here](./setup.md) to see how to setup the full project.
---

# 📌 Overview

This project demonstrates a **cloud-native AI chatbot system** built with:

* 🧠 Context-aware AI responses using Amazon Bedrock – Nova Micro
* 🔐 User authentication (Register/Login)
* 💬 Multi-session conversation handling
* 💾 Persistent chat history using DynamoDB
* ⚡ Fully serverless backend using AWS Lambda
* 🌐 Responsive frontend built with HTML, CSS, JavaScript

The system is designed following **scalable serverless architecture principles** and **least-privilege IAM policies**.

---

# 🏗️ Architecture

## 🔁 Message Flow (End-to-End)

When a user sends a message:

1. **User sends a message via HTML/CSS/JavaScript frontend**  and Request is routed to **API Gateway** 

2. **API Gateway** triggers a Lambda function
3. Lambda:

   * Retrieves conversation history from DynamoDB
   * Sends history + current message to Amazon Bedrock (Nova Micro)
   * Receives AI response
   * Updates DynamoDB with new conversation entries
4. Response is returned to frontend

---

## 📊 Application Architecture Diagram

![alt text](Application_Architecture.png)

## 📊 High-Level Architecture Diagram

```
              ┌─────────────────────┐
            HTML/CSS/JavaScript frontend
              └───────────┬─────────┘
                          │
                          ▼
                  ┌───────────────┐
                  │ API Gateway   │
                  └───────┬───────┘
                          │
                          ▼
                 ┌────────────────┐
                 │ AWS Lambda     │
                 │ (Business Logic)│
                 └───────┬────────┘
          ┌──────────────┼──────────────┐
          ▼              ▼              ▼
  DynamoDB        Amazon Bedrock      Auth Logic
(user-data)       (Nova Micro)     (user-data)
(conversation_data)


```
## 📊 Workflow_Architecture_Diagram

![alt text](Workflow_Architecture_Diagram.png)
---

# 🧠 AI Layer

### 🔹 Model Used

* **Amazon Bedrock – Nova Micro**

### 🔹 Context Handling Strategy

Each model invocation includes:

* Previous conversation history
* Current user input
* Structured payload format

This enables:

* Context-aware replies
* Continuity across sessions
* Natural multi-turn conversation

---

# 🗄️ Database Design

## 🧾 `user-data`

| Attribute       | Purpose                    |
| --------------- | -------------------------- |
| userId (PK)     | Unique user identifier     |
| Credentials     | Login validation           |
| conversationIds | List of user conversations |


Used for:

* Authentication
* Tracking multiple chat sessions per user

---

## 💬 `conversation_data`

| Attribute           | Purpose                        |
| ------------------- | ------------------------------ |
| conversationId (PK) | Unique conversation identifier |
| Messages            | Full chat history (User + AI)  |

Used for:

* Fetching chat history
* Updating conversations
* Continuing previous sessions

---

# 🔐 Authentication System

### Lambda Functions:

* ✅ `register`
* ✅ `login`

Authentication flow:

1. User registers → stored in `user-data`
2. User logs in → validated against stored credentials
3. Session established on frontend

---

# 💬 Conversation Features

## ➕ Create New Chat

* Triggers `generate-conversation-id` Lambda
* Creates new entry in `conversation_data`
* Updates user’s conversation list in `user-data`

---

## 📂 View Conversation History

* Dedicated Lambda retrieves all conversation IDs
* Sidebar lists:

  * All previous chats
  * Full conversation history
* Users can resume any conversation seamlessly

---

## ✨ AI Message Processing

The `model-invocation` Lambda:

1. Fetches chat history
2. Sends structured payload to Bedrock
3. Receives AI response
4. Updates conversation history
5. Returns response to frontend

Ensures persistent, contextual dialogue.

---

# 🛠️ AWS Services Used

| Service            | Purpose                   |
| ------------------ | ------------------------- |
| Amazon API Gateway | REST API exposure         |
| AWS Lambda         | Serverless compute        |
| Amazon DynamoDB    | NoSQL data storage        |
| Amazon Bedrock     | AI model inference        |
| IAM                | Role-based access control |

---

# ⚡ Why This Architecture?

* ✅ Fully Serverless (No EC2)
* ✅ Auto-scalable
* ✅ Pay-per-use
* ✅ Decoupled components
* ✅ Secure with IAM least privilege
* ✅ Cloud-native design

---

# 🧪 API Structure (Backend)

### BedRockInvoke API (REST)

* `POST /bedRockInvoke`
* `POST /history`

Handles:
* AI model invocation
* Chat history retrieval

### loginRegister API (REST)

* `POST /login`
* `POST /register`
* `POST /generateConvoId`

Handles:
* Authentication
* Conversation creation

---

# 📦 Tech Stack

**Frontend**

Built using:

* HTML
* CSS
* JavaScript

Features:

* Responsive chatbot interface
* Real-time message rendering
* API-based backend integration
* Clean and intuitive UI design

**Backend**

* Python (AWS Lambda)
* Boto3 SDK
* Serverless Architecture

**Cloud**

* Amazon Bedrock
* AWS 
* DynamoDB
* Amazon API Gateways
* CloudWatch
---

# 🔮 Future Enhancements

* 🔐 JWT-based authentication
* 🧠 Conversation summarization
* ⚡ Streaming responses from Bedrock
* 📊 Token usage analytics
* 🛡️ Rate limiting
* 🚀 CI/CD pipeline
* 📈 Monitoring with CloudWatch dashboards

---

# 🏆 Key Learning Outcomes

* Designing production-style serverless architectures
* Managing AI inference pipelines
* Context handling in LLM applications
* DynamoDB schema planning
* IAM least-privilege policy design
* Full-stack cloud integration

---

# 👨‍💻 Author

**Rachit Rai**
Engineer - Cloud and Infra Management