# School Cybersecurity Incident Management System

## Overview

This project implements a **scalable and structured database model** designed to manage and analyze cybersecurity incidents in educational institutions.  
The system centralizes incident reporting, detection, response, prevention, and training data in order to **support prevention, fast decision-making, and long-term security improvement** in schools.

The database is designed to work efficiently at **large scale**, from a single school to a national-level deployment.

---

## Core Concept

At the heart of the system lies the **Incident** entity, which acts as the central point connecting all security-related information:
- where an incident occurred,
- who was involved,
- how it was detected,
- how fast it was resolved,
- and what preventive actions were taken afterward.

This design ensures **traceability, accountability, and analytical power**.

---

## Main Entities and Their Roles

### **School**
Represents an educational institution.  
Each school can contain multiple zones and can register multiple incidents.

**Purpose:**
- Enables analysis at school level
- Supports comparisons between institutions
- Allows national-level aggregation

---

### **Zone**
Represents logical or physical areas inside a school (laboratories, administrative offices, staff areas).

Each zone belongs to a single school and may be associated with multiple incidents.

**Why it matters:**
- Identifies high-risk areas
- Helps prioritize security investments
- Supports zone-based prevention strategies

---

### **Incident** (Central Entity)
Represents a cybersecurity event reported within a school.

An incident is:
- linked to a school and a zone,
- classified by attack type,
- associated with users,
- detected through one or more methods,
- resolved within a measurable response time,
- followed by preventive recommendations.

**This entity acts as the backbone of the entire database.**

---

### **Attack_Type**
Classifies incidents (e.g. phishing, unauthorized access, malware).

**Benefits:**
- Enables pattern recognition
- Supports trend analysis
- Helps prioritize training and prevention

---

### **User**
Represents individuals involved in incidents (students, teachers, administrators).

Users may participate in:
- incidents,
- training sessions,
- detection or reporting processes.

---

## Many-to-Many Relationship Tables

To model real-world complexity, the database uses **association tables**:

### **Incident_User**
Links incidents with all users involved.

**Why this is important:**
- One incident can involve multiple people
- One user can be involved in multiple incidents
- Avoids data duplication

---

### **Incident_Detection** & **Detection_Method**
Tracks how incidents were discovered (monitoring systems, reports, audits).

**Impact:**
- Measures detection effectiveness
- Identifies weak points in monitoring
- Improves early detection strategies

---

### **Incident_Prevention** & **Prevention_Measure**
Stores preventive actions taken after incidents.

**Purpose:**
- Connects incidents with security measures
- Supports continuous improvement
- Enables evaluation of prevention effectiveness

---

## Response and Improvement Components

### **Incident_Response_Time**
Stores the reported and resolved timestamps of an incident.

**Why it matters:**
- Measures operational efficiency
- Helps reduce reaction delays
- Supports performance evaluation

---

### **Incident_Recommendation**
Contains security recommendations generated after incidents.

Each recommendation includes a priority level.

**Benefits:**
- Encourages proactive security
- Supports management decision-making
- Helps prevent recurrence of incidents

---

### **Training_Session**
Represents cybersecurity training activities for users.

**Role in the system:**
- Improves awareness
- Reduces human-related vulnerabilities
- Supports long-term security culture

---

## Database Design Principles

### **Third Normal Form (3NF)**
- Eliminates redundancy
- Preserves data consistency
- Simplifies maintenance

### **Scalability by Design**
- Centralized incident model
- Modular relationships
- Ready for millions of records

### **Real-World Accuracy**
- Reflects actual security workflows
- Supports operational and strategic use cases
- Aligns with institutional needs

---

## Why This Database Matters

- Improves cybersecurity visibility in schools
- Enables data-driven prevention
- Supports fast incident response
- Helps teachers and management make informed decisions
- Can be expanded at regional or national level

---

## Conclusion

This database is not just a storage solution, but a **decision-support system**.  
It transforms raw security events into **actionable intelligence**, helping educational institutions move from reactive to proactive cybersecurity.

The model is **robust, scalable, and future-proof**, making it suitable for real-world deployment and further development.
