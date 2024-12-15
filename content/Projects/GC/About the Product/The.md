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

### **Player Registrations, Audience Access, and Profiles**

Players will undergo a progressive registration process, ensuring their profiles are built and updated gradually as they engage with the application. This allows for a personalized experience, where information is captured over time based on the player's interaction with the platform.

During registration, players will be required to provide the following essential details:

- **First Name**
- **Middle Name**
- **Last Name**
- **Phone Number**
- **Valid College Email ID ( ending with *@iiit-bh.ac.in)
- **Gender**
- **Batch**
- **Branch**

Additionally, players have the option to include their social media profiles (e.g., links to their social handles), although this is not mandatory.

The **branch** field is particularly sensitive. In case of any changes, such as a branch transfer, players can raise an issue, which will be reviewed and resolved by `SUPERADMIN` to ensure that all information remains accurate.

Future updates will introduce [[Form Fields]]


#after-registration
After registration, players will initially have access similar to that of an unauthorized **Audience**. However, they will have additional capabilities that enhance their engagement and participation within the platform.

### **Players can:**

- **Change their profile**: Players can update and modify their personal details, such as their name, contact information, and other profile settings, ensuring their information is always up-to-date.
- **Request to join teams**: Players can express interest in joining specific teams, allowing for seamless integration into team-based activities and events.
- **Leave a team**: Players have the ability to request to leave a team, providing them with control over their participation and team affiliations.
- **Team Actions**: Players can take actions related to team management, such as requesting team membership or initiating team changes, all within the context of the platform’s team structure.

### **Future Scope:**

- **Self-Review**: In the future, players will have the ability to self-review their performance, gaining insights into their contributions and progress. This feature will help players evaluate their skills and growth, fostering a more self-driven approach to improvement.
superadmin POV: 

- change 



- create profile 

#### **For the Audience**

- For users who wish to explore the application without full registration, the platform provides a public view system. This allows audience members to browse content such as match updates, team information, and live scores without the need for a personal profile.
- The philosophy behind this is to foster open access and inclusivity, enabling anyone to engage with the platform casually before deciding to create a more personalized profile. This approach ensures that the application is accessible to all users, whether they are looking for quick information or seeking a more tailored experience as a player or participant.