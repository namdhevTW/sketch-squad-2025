# ADR-01: Architecture-Analysis

## Date:
2025-03-13

## Status:
Recruiters currently face inefficiencies in scheduling interviews due to a manual, fragmented process that lacks centralized scheduling, real-time updates, and intelligent interviewer matching. The existing process involves multiple applications (GT, GH, JW, Leave Planner) that operate in silos, making it difficult to streamline scheduling, track interview progress, and notify stakeholders effectively.

Key challenges include:

Manual effort required for interviewer identification and scheduling.

No centralized system to manage interview schedules and availability.

Lack of real-time integration between existing applications, leading to data silos.

Difficulty in finding interviewers with the right skills.

No automated notification system for interview updates.

No AI-driven assistant to aid recruiters in interview coordination.

A new architecture is required to address these inefficiencies and provide a seamless, automated scheduling experience with improved integration, real-time updates, and AI-powered coordination.

## Context:
Recruiters currently face inefficiencies in scheduling interviews due to a manual, fragmented process that lacks centralized scheduling, real-time updates, and intelligent interviewer matching. The existing process involves multiple applications (GT, GH, JW, Leave Planner) that operate in silos, making it difficult to streamline scheduling, track interview progress, and notify stakeholders effectively.

Key challenges include:

- Manual effort required for interviewer identification and scheduling.

- No centralized system to manage interview schedules and availability.

- Lack of real-time integration between existing applications, leading to data silos.

- Difficulty in finding interviewers with the right skills.

- No automated notification system for interview updates.

- No AI-driven assistant to aid recruiters in interview coordination.


A new architecture is required to address these inefficiencies and provide a seamless, automated scheduling experience with improved integration, real-time updates, and AI-powered coordination.
## Decision:
The system will adopt a **hybrid architecture combining API Gateway and event-driven microservices** to ensure flexibility, real-time processing, and seamless integration with existing applications.

### **1. API Gateway for External Interactions**

- Centralized **API Gateway** for handling external requests from **chatbot, dashboard, and recruiters**.

- Implements **authentication (OAuth2, JWT)**, request validation, and rate limiting.

- Provides RESTful APIs for querying interviewer availability and scheduling interviews.


### **2. Event-Driven Microservices for Internal Workflows**

- **Loosely coupled microservices** handle interviewer matching, scheduling, notifications, and reporting.

- **Kafka or Google Pub/Sub** for asynchronous event-driven communication.

- Ensures **scalability and fault tolerance**, reducing dependency on synchronous API calls.


### **3. Automated Interviewer Matching & Scheduling**

- Use JW app for interviewer skills and availability.

- Integrate Leave Planner to prevent scheduling conflicts.

- Auto-match candidates and interviewers, send calendar invites, and reschedule if needed.


### **4. AI-Powered Chatbot for Interview Coordination**

- Built using **Google Dialogflow and Google Cloud Functions**.

- Supports recruiter queries via **Google Chat** to suggest top 3 interviewers.


### **5. Automated Notifications & Alerts**

- Google Chat + email notifications for interview scheduling, rescheduling, and cancellations.

- Real-time alerts for interview status updates.


### **6. Centralized Dashboard & Reporting**

- Provides recruiter workload tracking, interviewer performance analytics, and scheduling efficiency reports.

- Built using **ReactJS, Node.js, and Elasticsearch**.


## Consequences:
### **Positive Outcomes:**

- ✅ **Improved Scheduling Efficiency**: Automated interviewer matching and scheduling reduce manual effort. 
- ✅ **Real-Time Updates**: Event-driven architecture ensures up-to-date interview statuses. 
- ✅ **Better Candidate-Interviewer Matching**: AI-driven selection enhances scheduling accuracy. 
- ✅ **Seamless Integration**: API Gateway enables controlled access, while event-driven microservices ensure interoperability. 
- ✅ **Enhanced Recruiter Productivity**: AI chatbot reduces manual queries and speeds up scheduling.
- ✅ **Improved Visibility**: Dashboards provide actionable insights for recruiters.

### **Trade-offs and Risks:**

- ⚠️ **Operational Complexity**: Managing event-driven microservices requires expertise in event sourcing and distributed systems.
- ⚠️ **Infrastructure Overhead**: Requires **Kafka, API Gateway, and serverless components**, leading to maintenance costs. 
- ⚠️ **Security Considerations**: Handling sensitive interviewer and candidate data requires **OAuth2, RBAC, and encryption mechanisms**.
- ⚠️ **Training Needs**: Recruiters may need initial training to adapt to the chatbot-driven scheduling approach.
