### **Give me an example of a time you had a conflict with a team member. How did you handle it?**

#### **My Response:**
>**One of the instance thaat i could think of where i had a conflict with a team member of mine, was during the development of the project that we had been developing for the smart india hackathon. a short description about the project it is an application that is designed to create annual reports for the institution. So we started with data collection etc using forms. We wanted to showcase analytical details about the data that we have got to make informed decision . so i insisted my teamate that we need to add one such feature. They told that we could statically add 3-4 graphs. I felt that an application should dynamic interaction and must allow users to create KPI of their needs. They said it would be difficult and it is a topic that is diverting from the problem statement. however i felt this was an game changer, so i concieved my teamates i would develop an module for that. using Ai (gemini) i was able to get input from the user as a text (normal but it should contain description about the table and i.e column in a high level) and on passing the prompt the graph would be added to the users dashboard**

#### **Structured Response:**

>    **Situation:**  
	**During the Smart India Hackathon, my team and I were developing an application to generate annual reports for an educational institution. One of our goals was to collect data using forms and present it effectively.**
>	
	**Task:**  
	**We needed to design the data presentation module. I proposed adding a dynamic analytics dashboard to allow users to generate custom KPIs and visualizations, while one of my teammates preferred using a few static charts, believing the dynamic feature was too complex and possibly outside the scope of the problem statement.**
>	
	**Action:**  
	**To resolve the disagreement, I acknowledged their concerns and proposed taking full responsibility for the feature as an independent module. I leveraged AI tools (specifically Gemini) to build a component that accepted natural language prompts to describe the table and graph requirements. The system then rendered corresponding charts on the user’s dashboard, enabling dynamic interaction without affecting the rest of the app's development.**
>	
	**Result:**  
	**The feature became a highlight during our final presentation and impressed the jury. It contributed significantly to our team winning the competition. The experience demonstrated the value of balancing innovation with collaboration and proactively resolving conflict with constructive solutions.**




### **Question: Tell me about a time you had to switch technical approaches mid-project.**
>
	**Situation:**  
	I was working on a project to rank students based on multiple metrics—level, age, and a few academic factors—and display this data in a tabular format with filters and mark entry functionality.
>	
	**Task:**  
	I initially chose Firebase because I wanted to explore it in a real project. I thought it would be a good opportunity to learn, especially because of its real-time data sync capabilities.
>	
	**Action:**  
	However, as we got closer to the deadline, I realized that implementing complex filtering and multi-column ranking logic in Firebase's NoSQL structure was turning out to be inefficient and time-consuming. Since I had limited experience with Firebase and the project required reliable sorting and filtering across multiple fields, my teammate and I made a joint decision to switch to SQL, a stack we were already comfortable with. That allowed us to complete the project efficiently and meet the deadline.
>	
	**Result:**  
	The final product worked smoothly with proper filters and bulk mark entry. More importantly, the experience taught me that technology decisions should be based not just on learning goals, but also feasibility and deadlines. I applied this lesson in a later project, MedCo, where we first outlined the core user needs and then selected a tech stack optimized for mobile users. That helped us avoid missteps and stay efficient from the start.
	


### **Question: Describe an occasion when you had to manage your time to complete a task. How did you do it?**

#### **My response**

>**Situation :**
>**In the month of January we had been part of a hackathon conducted by KYN - a startup , and it was on the eve of new year and I and my teamates were travelling to our hometown and we gave our best but not the fullest (It was the first round that happened during that time) . But to our surprise we were shortlist for the next round be hadn't built the website entire and we had only 1.5 days left.** 

>**Task:**
>**We first walked through the features that we gathered earlier to be implemented. And went through each one of the made priorities for each one of them.**

>**Action:**
>**We efficiently managed those implementation of those task , I took the lead and assigned tasks to my teamates that they are comfortable with to complete more tasks in the given span of time. I took care of the backend.**

>**Result:**
>**We were transformed the application to whole new level that they panel member who had gone through the Github screenshot of the older version said that "Both the versions are in two different poles." . The outcome was that with proper time and team management anything is possible**

#### **Improved Response:**

**Situation:**  
**In January, my team and I participated in a hackathon conducted by KYN, a startup. The first round took place around the New Year holidays, and we were traveling to our hometowns. As a result, we couldn’t give our full attention and submitted only a partially built website.**

**Task:**  
**To our surprise, we were shortlisted for the next round. With only 1.5 days left, we had to complete the full application quickly and efficiently.**

**Action:**  
**We immediately reviewed the feature list we had previously compiled and prioritized each feature based on impact and feasibility. I took the lead in task delegation, assigning components to each teammate based on their strengths and comfort zones to maximize efficiency. I personally focused on building out the backend while ensuring everyone stayed aligned.**

**Result:**  
**We delivered a significantly upgraded version of the application. One of the panel members even remarked that “both versions look like they’re from completely different worlds.” This experience reinforced how proper time and team management, even under pressure, can lead to exceptional outcomes.**

**---**

**✅ What you did well:**

- **Clear scenario with a challenge**
    
- **Shows initiative, leadership, and adaptability**
    
- **Includes a positive result and feedback from judges**
    

**📌 What you can improve:**

- **Be mindful of grammar and fluency (e.g., “we were shortlist” → “we were shortlisted”, “we were transformed” → “we transformed”)**
    
- **Keep the language professional—avoid casual phrasing like "gave our best but not the fullest"**
  

### Describe an occasion when you failed at a task. What did you learn from it?

**Situation:**  
	In 10th grade, I struggled academically because I didn’t take my studies seriously. I was easily distracted and didn’t have clear goals at the time.
	**Task:**  
	As a student, my responsibility was to manage my time and focus on building a strong academic foundation. But I didn’t give it the attention it needed.
	**Action:**  
	When I received my results, it was a wake-up call. I realized that I was limiting my future opportunities. That failure pushed me to become more intentional about how I use my time. I started setting goals, creating study plans, and holding myself accountable.	
	**Result:**  
	That shift helped me improve significantly in the following years, not just academically, but also in how I approached projects, deadlines, and responsibilities. It laid the groundwork for how I now take ownership of my learning and work, including projects where I proactively research tools, plan timelines, and reflect on what’s working.


	My answer- Project wise:
	
>Situation:
One of the mistake that i made in my Smart india hackathon, is in the report generation module, In this module user are allowed to generate report of the happenings that happened departwise wise and some subcategories wise by checking on checking provided to them. This way an automated AI genrated content for the report would be generated 
>
	Task:
	The  mistake that i made for providing dummy values for the dropdown for the report module didnt provide exact data and ALSO didnt take into consideration that "Not field values could be provided also" , like for some dropdown subsections couldn't be shown". 
>
	Acion:
	So while transitioning into the actual data for the subsections , so for some subsections there werent any data sensible to display graph. But my code threw an error that an query must be give for it and also i couldnt manage to fix it in the frontend like error handling
	>
	Result:
	From then on i decided to dive deep into research into a idea and think all possible edges so that my application would be resilient such that i doesnt through error for any input that user gives (as we cant expect users to provide the correct input format )
	
	
	### **Refined Answer (Project-Based — Smart India Hackathon):**
>		
		**Situation:**  
		During the Smart India Hackathon, I worked on a report generation module that allowed users to generate department-wise reports using dropdowns to filter content and subcategories. The system was designed to generate AI-based summaries dynamically.
	>	
	Task:**  
		My task was to ensure that the dropdowns reflected real backend data and that reports were generated smoothly, even if some sections had no associated data.
	>	
	**Action:**  
		In my initial implementation, I used dummy values in the dropdowns and didn’t account for cases where certain subcategories might not have any data. When we transitioned to actual data, this caused errors in the backend queries, especially when no meaningful values were returned. I also didn’t implement proper error handling on the frontend, so users received unhelpful error messages or the app would crash.
>		
	Result:
		This experience taught me the importance of planning for edge cases and handling missing or incomplete data gracefully. Since then, I’ve adopted a mindset of building **resilient, user-friendly applications** by validating inputs thoroughly, testing against empty or malformed data, and providing fallback UI behavior. I now always ask: “What happens if the user provides nothing, or the system returns an unexpected value?”
	>	
		---
	>	
		### ✅ Why this works:
	>	
		- Shows a **real technical mistake** that’s understandable and common.
>		    
>		- Demonstrates **ownership**, **problem-solving**, and **growth**.
	> 	   
		- Has a **clear takeaway** that applies to future work (error handling, user input validation, robustness).

https://www.indeed.com/career-advice/interviewing/behavioral-interview-questions