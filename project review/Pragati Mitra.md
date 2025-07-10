

# Problem statement

>This project was developed as part of our participation in **Smart India Hackathon 2024**, where we were proud winners under the **Ministry of AYUSH** problem statement..

This was under ministry of ayush, which has a set of medical colleges, under it, they asked to develop website that could generate anualized report for their intiution every year.


### Context

The Ministry of AYUSH oversees a number of medical colleges across India. They challenged us to create a web-based solution that could **automatically generate comprehensive annual reports** for their institutions.

### Need for the Product

Educational institutions produce large volumes of data every academic year, including:
- Academic performance statistics
- Financial and audit statements
- Research publications
- Faculty and student achievements
    
Compiling all this into a single, coherent, and visually engaging annual report is a **time-consuming and error-prone** process. Institutions often struggle with:
- Aggregating and standardizing data from multiple departments
- Presenting the data in a structured and reader-friendly format
- Meeting regulatory and compliance requirements
### Current Pain Points

- Manual data entry and formatting consumes excessive time
- Difficulty integrating data from varied, disconnected sources
- Lack of automation leads to human errors and inconsistencies
- Poor data visualization limits the insights that can be drawn
- Reports often fail to meet professional or compliance standards


### LANDING PAGE:

![[Pasted image 20250709182113.png]]
![[Pasted image 20250709182138.png]]
![[Pasted image 20250709182224.png]]
![[Pasted image 20250709182251.png]]
![[Pasted image 20250709182304.png]]
![[Pasted image 20250709182328.png]]
### Different Roles/ users

- Student
- Teacher
- HOD
- Internal Quality assurance Coordinator (IQAC)
- academic coordinator
- principal
### Architecture Diagrams

![[Pasted image 20250709183128.png]]
![[Pasted image 20250709183157.png]]
### Login page
![[Pasted image 20250709183820.png]]

### Student Pages

> Each student has their own secure login, allowing them to **track and manage their academic and extracurricular achievements**, as well as maintain personal and institutional details.

####  Key Features:

- **Login Portal:** Secure access via unique credentials
- **Achievements Tracker:** Add and manage academic, research, and extracurricular accomplishments
- **Profile Management:** Update personal details, course information, and contact data
- **Document Upload:** Upload certificates, project reports, and other relevant documents

![[Pasted image 20250709204024.png]]
![[Pasted image 20250709204052.png]]


# Faculty Login

>Faculty members have dedicated login access to **view analytical data** of the students under their mentorship and to **upload and manage their own achievements**.

#### Key Features:

- **Secure Faculty Login:** Role-based authentication for faculty access
- **Student Insights Dashboard:** View academic performance, achievements, and activity logs of students they oversee
- **Faculty Achievements Upload:** Submit publications, certifications, awards, and other professional milestones

![[Pasted image 20250709204325.png]]



### HOD (head of the department) Role

> The HOD dashboard provides a **comprehensive visual overview** of faculty performance, student progress, and placement statistics. It’s designed to support **data-driven decision-making** through customizable insights.

---
#### 📊 Dashboard Overview

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
#### Email 
Users can send emails directly to other students, faculty, or the HOD within the institution using the **built-in email system**—eliminating the need to switch to external platforms like Gmail.
![[Pasted image 20250709220036.png]]

#### Chatting feature 

Users can engage in real-time conversations with **other HODs, faculty, and students** through the built-in chat system. This facilitates **collaborative discussions** on common topics, departmental matters, and academic updates—all within the platform.

![[Pasted image 20250709222813.png]]


#### Forms

The forms created by all IQAC coordinators are automatically assigned to all HOD. they are responsible for managing the data of their department in these forms.

i) The can perform CRUD operations on the forms (Role based -> only their department level)
Read/View the data departmental level ONLY
![[Pasted image 20250710113455.png]]
![[Pasted image 20250710113605.png]]
![[Pasted image 20250710121135.png]]
![[Pasted image 20250710121214.png]]
ii) assign individual forms to the faculty so that they would take responsibility of that particular form alone.

The forms are assigned in an clever way, the faculty aren't created a new user to assign these forms. rather a simple email id(google) is enough to assign these forms. So the user can login with their google account and access these forms and manage them

![[Pasted image 20250710122040.png]]

a mail notification is sent to the assigned user . so going forward any deadline assigned to them is also assigned to them.
![[Pasted image 20250710122013.png]]
iii)They can also manage those assigned users i.e remove the user if not needed.
![[Pasted image 20250710122114.png]]


# IQAC -POV

#### Dashboard page

The IQAC dashboard board page has a detailed analysis on various metric like students, faculty and placement department wise making it visually appealing to the them.

![[Pasted image 20250710122333.png]]


#### Form pages

The IQAC coordinator is capable of organizing the data in the form of  forms through 3 ways:
i) The inbuilt form feature
ii) Linking with google sheets 
iii)Integrating details from other database that exists in the server.
![[Pasted image 20250710131355.png]]
i)Inbuilt Form

Here as IQAC role they would be only be able to view the data of that other departments have filled in through form.
![[Pasted image 20250710123032.png]]

apart from these, the IQAC can :
	i)Lock Forms - if the form is locked , no can add new records, edit records, delete records. only view can be done
	![[Pasted image 20250710123236.png]]


ii) Deadline - deadlines can be assigned to these forms so that i can create an sense of urgency to fill in the data at the right time
![[Pasted image 20250710123421.png]]


iii)Delete Form - This feature is to delete the forms that were created. in order to prevent accidental deletion. user has to type in the name of the form itself to delete

![[Pasted image 20250710123620.png]]

iv) Google forms

Fetches data Realtime from the google form and renders it here
![[Pasted image 20250710131416.png]]
![[Pasted image 20250710131500.png]]
![[Pasted image 20250710131514.png]]




# report


#### Form list

![[Pasted image 20250710131905.png]]


#### create report
![[Pasted image 20250710132114.png]]
each sub section can be assigned to different user based on the mail id.

User can only see and modify sections that they are assigned only.

they are provided checkbox to select which subsections that they want in the report. the subsections have predefined SQL queries written for it to fetch the data.

Since the data is in tabular form and for the report we would textual content is needed right? a small is done by provided by giving an automatic AI generated Introduction and the content for that subsection. 

The user can further edit this content as they want.

![[Pasted image 20250710132858.png]]
![[Pasted image 20250710132929.png]]

The users can also upload images (along with description to appear in the report).  Also youtube URL could be added to the report.

IN PDF version an QR is rendered instead of the Link to simplify the user
IN HTML version the Video is embedded.


The data need to persist right? all cant be done at one moment right, hence we have give an option to save each subsection.


What if we want to revert ? no worries we have provided Versioning control to revert to previous version


