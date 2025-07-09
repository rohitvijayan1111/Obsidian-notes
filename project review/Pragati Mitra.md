

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

> Dashboard:
> As soon as the HOD login, they will be able to visually see the stastically data on the faculty,students and also the placement status (year wise-which could be changed in the dropdown)


![[Pasted image 20250709212001.png]]

to visualize more customizably the user can create additional graph based on the Key performance indicators in two ways :

i) Prompting an inbuilt graph generator to create graph that user asks in natural language
 ![[Pasted image 20250709215028.png]]
 ![[Pasted image 20250709215108.png]
 
 The multistacked bar graph of placement details gets added to the dashboard of that user.
ii) Create an sql query from the options given -> for computer professionals/administrators
![[Pasted image 20250709214731.png]]


