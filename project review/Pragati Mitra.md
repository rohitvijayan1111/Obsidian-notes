

# Problem statement

>This project was developed as part of our participation in **Smart India Hackathon 2024**, where we were proud winners under the **Ministry of AYUSH** problem statement..

This was under ministry of ayush, which has a set of medical colleges, under it, they asked to develop website that could generate anualized report for their intiution every year.


### **Context**

The Ministry of AYUSH oversees a number of medical colleges across India. They challenged us to create a web-based solution that could **automatically generate comprehensive annual reports** for their institutions.

### **Need for the Product**

Educational institutions produce large volumes of data every academic year, including:
- Academic performance statistics
- Financial and audit statements
- Research publications
- Faculty and student achievements
    
Compiling all this into a single, coherent, and visually engaging annual report is a **time-consuming and error-prone** process. Institutions often struggle with:
- Aggregating and standardizing data from multiple departments
- Presenting the data in a structured and reader-friendly format
- Meeting regulatory and compliance requirements
### **Current Pain Points**

- Manual data entry and formatting consumes excessive time
- Difficulty integrating data from varied, disconnected sources
- Lack of automation leads to human errors and inconsistencies
- Poor data visualization limits the insights that can be drawn
- Reports often fail to meet professional or compliance standards


### 1. Landing Page:

![[Pasted image 20250709182113.png]]
![[Pasted image 20250709182138.png]]
![[Pasted image 20250709182224.png]]
![[Pasted image 20250709182251.png]]
![[Pasted image 20250709182304.png]]
![[Pasted image 20250709182328.png]]
### 2. Different Roles/ users

- Student
- Teacher
- HOD
- Internal Quality assurance Coordinator (IQAC)
- academic coordinator
- principal
### 3. Architecture Diagrams

![[Pasted image 20250709183128.png]]
![[Pasted image 20250709183157.png]]
### 4. Login page
![[Pasted image 20250709183820.png]]

### 5. Student Pages

> Each student has their own secure login, allowing them to **track and manage their academic and extracurricular achievements**, as well as maintain personal and institutional details.

####  Key Features:

- **Login Portal:** Secure access via unique credentials
- **Achievements Tracker:** Add and manage academic, research, and extracurricular accomplishments
- **Profile Management:** Update personal details, course information, and contact data
- **Document Upload:** Upload certificates, project reports, and other relevant documents

![[Pasted image 20250709204024.png]]
![[Pasted image 20250709204052.png]]


### 6. Faculty Login

>Faculty members have dedicated login access to **view analytical data** of the students under their mentorship and to **upload and manage their own achievements**.

#### Key Features:

- **Secure Faculty Login:** Role-based authentication for faculty access
- **Student Insights Dashboard:** View academic performance, achievements, and activity logs of students they oversee
- **Faculty Achievements Upload:** Submit publications, certifications, awards, and other professional milestones

![[Pasted image 20250709204325.png]]



### 7. HOD (head of the department) Role

> The HOD dashboard provides a **comprehensive visual overview** of faculty performance, student progress, and placement statistics. It’s designed to support **data-driven decision-making** through customizable insights.

---
### Dashboard Overview

Upon login, the HOD is presented with an **interactive dashboard** displaying:
- Year-wise **placement statistics**
- Faculty performance summaries 
- Student achievement metrics
    
A **dropdown menu** allows filtering data by academic year, department, or other criteria.
![[Pasted image 20250709212001.png]]

To empower HODs/Principal/IQAC with deeper insights, the platform offers two intuitive methods to create custom graphs based on **Key Performance Indicators (KPIs):**

#### Method 1: **Natural Language Graph Generation**

- Users can simply **describe the graph they want** in plain English.
- An **AI-powered inbuilt graph generator** interprets the prompt and renders the requested visualization.
>Example:
>Create a multistack graph that helps us visualize the no of students who are eligible for placements and no of students who have already been placed.

![[Pasted image 20250709215028.png]]![[Pasted image 20250709215455.png]]
 The **multi-stacked bar graph** is then **automatically added to the user's dashboard** for quick reference and ongoing analysis.
 
ii)For users with technical expertise—such as **administrators or computer professionals**—the platform allows custom data visualization through **SQL queries**  via these dropdowns and input boxes .
![[Pasted image 20250709214731.png]]
### 8. Email 
Users can send emails directly to other students, faculty, or the HOD within the institution using the **built-in email system**—eliminating the need to switch to external platforms like Gmail.
![[Pasted image 20250709220036.png]]

### 9. Chatting feature 

Users can engage in real-time conversations with **other HODs, faculty, and students** through the built-in chat system. This facilitates **collaborative discussions** on common topics, departmental matters, and academic updates—all within the platform.

![[Pasted image 20250709222813.png]]



### 10. Forms Management

#### **Overview**

Forms created by IQAC Coordinators are automatically assigned to all respective Heads of Departments (HODs). Each HOD is responsible for managing and maintaining the data specific to their department within these forms.

---
### 10.1 HOD Access & Responsibilities
- **Role-based Access Control**  
    HODs can perform CRUD (Create, Read, Update, Delete) operations **only within their departmental scope**.
- **Data Visibility**  
    HODs can **view and manage** data relevant to their department alone.
---
![[Pasted image 20250710113455.png]]
![[Pasted image 20250710113605.png]]
![[Pasted image 20250710121135.png]]
![[Pasted image 20250710121214.png]]
### 10.2 Faculty Assignment

- HODs can **assign individual forms to faculty members**, making them responsible for managing that specific form.
- **Authentication**  
    Faculty are not required to create new user accounts. A **Google email ID is sufficient**. They can log in using their Google account to access and manage their assigned forms.
![[Pasted image 20250710122040.png]]
- **Email Notifications**  
    Assigned users receive **email notifications** when a form is assigned. Any associated deadlines are also linked to the user.
![[Pasted image 20250710122013.png]]
- **User Management**  
    HODs can **remove faculty members** from form responsibilities if needed.

![[Pasted image 20250710122114.png]]


### 11. IQAC – Point of View

#### 11.1 Dashboard Page

The **IQAC dashboard** provides a detailed, visually engaging analysis across key metrics such as **students, faculty, and placement statistics**, organized **department-wise** for easy comparison and insight.

![[Pasted image 20250710122333.png]]

---

#### 11.2 Form Management

The IQAC Coordinator can organize and manage institutional data through **three primary methods**:

1. **Inbuilt Form Builder**
2. **Google Sheets Integration**
3. **Server-Side Database Integration**
    

![[Pasted image 20250710131355.png]]

---

##### 11.3 Inbuilt Form Feature

As an IQAC user, access to forms is **view-only**. The data visible comes from entries filled in by respective departments.

![[Pasted image 20250710123032.png]]

---

##### Additional Form Controls

The IQAC has several administrative controls over the forms:
###### ✅ Lock Forms

Once a form is locked:
- No new entries can be added
- Existing data **cannot** be edited or deleted
- Only **view access** remains
    
![[Pasted image 20250710123236.png]]

---
###### Set Deadlines
Deadlines can be assigned to each form to **ensure timely data submission** and maintain accountability.

![[Pasted image 20250710123421.png]]

---
######  Delete Form
Forms can be deleted, but to **prevent accidental deletion**, the system requires the user to manually type the form name as confirmation.

![[Pasted image 20250710123620.png]]
## 12. Report Creation Module
### Introduction

One of the core requirements from the Ministry of AYUSH was to automate the generation of **institutional annual reports**—a task that traditionally involves intensive manual effort, data collection, formatting, and approvals across departments.

Our platform offers a **collaborative, data-driven report creation system** that allows different stakeholders (IQAC, HODs, faculty, coordinators) to work together seamlessly. Each section of the report is:
- Automatically populated using SQL-driven queries
- Accompanied by AI-generated textual summaries
- Enhanced with charts, images, and embedded videos
This ensures that the final report is **insightful, visually appealing**, and meets **compliance and regulatory standards** without manual formatting efforts.

---
### Section Assignment

Each report is broken down into **multiple subsections**. These subsections can be assigned to specific users using their email addresses.

![[Pasted image 20250710132114.png]]

- Users have access **only to the sections assigned to them**.
- A checkbox system allows users to select which subsections they wish to include in the report.
- All subsections are powered by **predefined SQL queries** that fetch the necessary data directly from the database, ensuring **accuracy and consistency**.
    
---
### AI-Powered Text Generation

Since the raw data retrieved is often tabular, the system also provides an **AI-generated textual summary** for each subsection. This includes:
- An introductory paragraph
- A basic interpretation of the data
Users can **review, modify, or replace** the generated content as needed, making it both a time-saver and a content aid.

![[Pasted image 20250710132858.png]]  
![[Pasted image 20250710132929.png]]

---
### Media & Multimedia Support

To make reports more engaging:
- **Images** (with descriptions) can be uploaded to be included in the report.    
- **YouTube video URLs** can also be embedded.

Output behavior:
- **PDF version**: YouTube links are automatically converted into **QR codes** for easy scanning.
- **HTML version**: Videos are directly embedded and playable within the page.
    

---

### Save Progress Functionality

Recognizing that report building is an iterative process, the system allows:
- **Each subsection to be saved independently**    
- Users to continue work over multiple sessions without losing progress

This enables flexibility and ensures that report building doesn’t need to be completed in one sitting.

---
### Version Control

To handle edits and revisions effectively, the system includes **version control**:
- Every update is saved as a new version
- Users can **revert to previous versions** if necessary
This prevents accidental overwrites and allows better change tracking during collaboration.

---
### Collaboration & Feedback System

Given that institutional reports are **multi-user and collaborative**, a built-in **feedback and discussion section** is available for every subsection:

- Users can raise issues, provide feedback, or ask for clarification
- All discussions stay tied to the relevant section for context
    

![[Pasted image 20250710133536.png]]

---

### Automatic Graph Generation

To supplement the textual content, **graphs and charts are auto-generated** based on the section's data. These visualizations enhance data interpretation and make the report more reader-friendly.

![[Pasted image 20250710133316.png]]  
![[Pasted image 20250710133343.png]]  
![[Pasted image 20250710133436.png]]  
![[Pasted image 20250710133457.png]]

---

### Report Output – PDF

The final PDF version is designed to be **clean, professional, and print-ready**, integrating:
- Text, data tables, images
- Graphs
- QR codes for video content
    

![[Pasted image 20250710133935.png]]  
![[Pasted image 20250710133949.png]]

---

### Report Output – HTML

The HTML version is designed for **digital sharing and interactivity**:
- Embedded videos
- Interactive charts
- Section-based navigation
    

![[Pasted image 20250710134100.png]]  
![[Pasted image 20250710134119.png]]


## 13. Inbuilt Virtual Assistant – _Pragati Bot_

Not sure where to find a feature or how to use a module?

Our platform includes **Pragati**, an **AI-powered virtual assistant** that is trained on the platform's documentation and workflows.

![[Pasted image 20250710134338.png]]

### Key Features:

- Provides **contextual help** based on user actions and queries
- Acts as a **guide for first-time users**
- Helps resolve **feature-specific doubts** quickly
- Offers **navigation tips**, **form assistance**, and **reporting help**
- Eliminates the need for external manuals or tutorials

Whether you’re a student, faculty, or administrator—**Pragati ensures you never feel lost** on the platform.

---
## 14. Infrastructure Login
An exclusive portal is provided for managing **infrastructure-related tasks**.
![[Pasted image 20250710143209.png]]
This section allows authorized personnel to:
- Manage physical infrastructure data
- Log and track asset inventories
- Oversee infrastructure updates and reports
    
This module supports **transparent infrastructure reporting** alongside academic and administrative modules.