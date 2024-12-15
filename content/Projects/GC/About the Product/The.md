The product involves three components 

- a mobile application / webview  to be used for viewing scores, updates, information for audience & players to put up their details, etc. 
- a web application to be used as a superadmin panel - to list matches and control the entire application, sessions etc
- a admin application / webview to be used for updating the scores
Roles: 

| **Role**   | **Description**                                                                                                                                                                         |
| ---------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **USER**   | Represents general users of the application, including roles such as Audience, Captains, and Umpires. Users can browse various components of the platform based on their specific role. |
| **ADMIN**  | Holds complete control over the system, including managing user accounts, overseeing match listings, configuring teams and squads, and terminating live user sessions when necessary.   |
| **SYSTEM** | Refers to programmatic actions and automated processes performed by the application, such as data updates, scheduled tasks, or system-generated changes.                                |
### Functional Requirements
# **User Management**

### **Sign-Up and Login**

- Users will register and log in to the application using their mobile number and a One-Time Password (OTP) for authentication.

### **Profile Management**

#### **For Users (Players)**

- Players will have a personalized experience, allowing them to create and update their profiles with essential details. This helps ensure their interactions within the application are tailored to their needs and preferences. The profile can include:
- it will be progressive registration 
    - **First Name**
    - **Middle Name**
    - **Last Name**
    - **Phone Number**
    - **Email Address (only  via clg email id)** 
    - **Gender**
    - **Batch**
    - **Branch**
    - **socials:[]** ? 

branch is a sensitive issue - if any isue arrises (branch changes )can be raisede and done fixed by superadmin
- future scope involves form fields integrations


- create profile 

#### **For the Audience**

- For users who wish to explore the application without full registration, the platform provides a public view system. This allows audience members to browse content such as match updates, team information, and live scores without the need for a personal profile.
- The philosophy behind this is to foster open access and inclusivity, enabling anyone to engage with the platform casually before deciding to create a more personalized profile. This approach ensures that the application is accessible to all users, whether they are looking for quick information or seeking a more tailored experience as a player or participant.