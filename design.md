# DESHGUIDE.AI – System Design Document

## 1. Architecture Overview
DESHGUIDE.AI is built as a cloud-native, serverless web application using AWS services. The system provides a multilingual, voice-first tourist guidance experience powered by generative AI and speech services.

## 2. High-Level Architecture

User Device (Mobile Web App / PWA)
→ Amazon API Gateway  
→ AWS Lambda (Backend Services)  
→ Amazon Bedrock (AI content generation & Q&A)  
→ Amazon Polly (Text-to-Speech)  
→ Amazon Transcribe (Speech-to-Text)  
→ DynamoDB (User preferences, session metadata)  
→ Amazon S3 (Media content storage)  
→ CloudFront (Content delivery network)

## 3. Component Design

### 3.1 Frontend
- Progressive Web App (PWA) built using React.
- Features:
  - QR code scanning
  - Language selection
  - Video playback
  - Voice interaction (mic button)
  - Accessibility mode toggle

### 3.2 Backend
- API Gateway to expose REST APIs for:
  - Fetching location-specific content
  - Handling user queries
  - Logging engagement data
- AWS Lambda functions to:
  - Orchestrate AI calls
  - Apply business logic
  - Manage user sessions

### 3.3 AI & Voice Layer
- Amazon Bedrock:
  - Generates tourist place descriptions.
  - Answers user questions.
- Amazon Polly:
  - Converts AI-generated text into natural speech.
- Amazon Transcribe:
  - Converts user voice queries into text.

### 3.4 Data Layer
- DynamoDB:
  - Stores language preferences and session metadata.
- Amazon S3:
  - Stores curated videos and public tourism datasets.

## 4. Data Flow

1. User scans QR code at a tourist location.
2. Frontend sends location ID + language preference to API Gateway.
3. Lambda fetches curated content from S3.
4. Lambda invokes Bedrock to generate narrative.
5. Generated text is sent to Amazon Polly for voice synthesis.
6. Audio + video content is streamed to the user.
7. User asks a question using voice input.
8. Transcribe converts speech to text.
9. Bedrock generates response.
10. Polly converts response to speech and returns to user.

## 5. Scalability & Performance
- Serverless architecture allows automatic scaling.
- CloudFront caches static content to reduce latency.
- Bedrock calls are batched where possible to reduce cost.

## 6. Security Design
- All endpoints protected with HTTPS.
- IAM roles with least-privilege access for AWS services.
- Admin APIs protected using authentication and authorization layers.

## 7. Reliability & Monitoring
- CloudWatch used for logging and monitoring.
- Alerts configured for high error rates or latency spikes.

## 8. Future Enhancements
- Offline content caching for low-connectivity regions.
- Integration with government tourism portals.
- Multimodal AI (image-based queries for landmarks).
- Analytics dashboard for tourism departments.
