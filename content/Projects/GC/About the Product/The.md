The product involves three components 

- a mobile application / webview  to be used for viewing scores, updates, information for audience & players to put up their details, etc. 
- a web application to be used as a superadmin panel - to list matches and control the entire application, sessions etc
- a admin application / webview to be used for updating the scores
Roles: 

| **Role**  | **Description**                                                                                                                                                                         |
| --------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **USER**  | Represents general users of the application, including roles such as Audience, Captains, and Umpires. Users can browse various components of the platform based on their specific role. |
| **ADMIN** | Holds complete control over the system, including managing user accounts, overseeing match listings, configuring teams and squads, and terminating live user sessions when necessary.   |
|           |                                                                                                                                                                                         |

### Functional Requirements
# **User Management**

### **Sign-Up and Login**

- Users will register and log in to the application using their mobile number and a One-Time Password (OTP) for authentication.

### **Profile Management**

for the audience mobile app, for people who just want to explore the application, can use a dummy-user credentials <add something more on this.. and its philosophy>

- Users will have the ability to create and update their profiles with the following details:
    - **First Name**
    - **Last Name**
    - **Phone**
    - **Email Address**
    - **Gender**
    - **Type of Interest** (e.g., Professional, Hobbies)