# AI-Driven Photo Search Platform

A comprehensive, end-to-end web application that enables intelligent photo album searches using natural language queries. This platform employs **AWS Rekognition** for label detection, **Amazon Elasticsearch (OpenSearch)** for indexing and retrieval, and **Amazon Lex** for natural language query processing. The entire solution is orchestrated via **AWS Lambda** and **Amazon API Gateway** and served through **Amazon S3**.

---

## Table of Contents
- [Overview](#overview)
- [Architecture](#architecture)
- [Features](#features)
- [Getting Started](#getting-started)
- [Deployment](#deployment)

---

## Overview
This project is designed to streamline the process of searching and retrieving images using **natural language**. By leveraging AWS Rekognition, images are automatically labeled, enriched with custom metadata from S3 object headers, and indexed in Amazon Elasticsearch (OpenSearch). Users can then query these images using a **natural language interface** powered by Amazon Lex or through a simple web-based interface hosted on Amazon S3.  

Key AWS Services involved:
- **Amazon S3** for storage and front-end hosting
- **AWS Lambda** for serverless compute
- **Amazon API Gateway** for RESTful endpoints
- **Amazon Rekognition** for labeling and image recognition
- **Amazon Elasticsearch (OpenSearch)** for searching and indexing
- **Amazon Lex** for conversational query processing

---

## Architecture
1. **Front End (Amazon S3 + JS/HTML/CSS/React/Vue/etc.)**  
   - Hosted on Amazon S3 (static website hosting).
   - Allows users to upload photos and input search queries.
2. **Image Upload (S3 Trigger)**
   - Photos uploaded to an S3 bucket trigger a Lambda function via an S3 event.
   - Custom metadata can be passed through S3 object headers.
3. **AWS Lambda (Indexing)**
   - Automatically invoked after new images are uploaded.
   - Uses AWS Rekognition to detect labels (e.g., “cat,” “beach,” “sunset”).
   - Integrates custom metadata from the S3 object.
   - Sends the combined label/metadata data to Amazon Elasticsearch (OpenSearch) for indexing.
4. **Amazon Elasticsearch (OpenSearch)**
   - Stores metadata and labels.
   - Allows full-text and tag-based queries for fast retrieval.
5. **Amazon Lex**
   - Provides a conversational interface for the end user.
   - Processes natural language queries and identifies search terms/intents.
6. **AWS Lambda (Search)**
   - Receives requests from Lex or the front-end.
   - Queries the Elasticsearch (OpenSearch) index to return relevant images.
7. **Amazon API Gateway**
   - Serves as the RESTful interface connecting the front-end to the back-end.
   - Integrates with Lambda functions for both indexing and search.

---

## Features
- **Natural Language Search:** Users can type queries like “Show me pictures of mountains at sunrise.”
- **Automated Labeling:** AWS Rekognition automatically tags each image (e.g., “dog,” “landscape,” “portrait”).
- **Metadata Integration:** Custom metadata from S3 object headers is indexed alongside Rekognition labels.
- **Serverless Architecture:** Runs on AWS Lambda and S3, minimizing operational overhead.
- **High Scalability:** Scales seamlessly with AWS services based on usage.
- **Full-Text Search with Elasticsearch (OpenSearch):** Enables fast and accurate search capabilities.

---

## Getting Started

### Prerequisites
- **AWS Account** with the following services enabled:
  - S3
  - Lambda
  - API Gateway
  - Amazon Rekognition
  - Amazon Elasticsearch (OpenSearch)
  - Amazon Lex
- **IAM Roles/Policies** granting permissions to:
  - Read/write from S3
  - Invoke Lambda
  - Use Rekognition
  - Access and modify Elasticsearch (OpenSearch) indices
  - Integrate with Amazon Lex
- **Node.js** or **Python** (depending on the language chosen for Lambda functions)
- **AWS CLI** (optional but recommended for easier service management)

### Local Setup
1. **Clone this Repository**  
   ```bash
   git clone https://github.com/your-username/ai-driven-photo-search.git
   cd ai-driven-photo-search
