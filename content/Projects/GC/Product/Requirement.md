The product consists of three main components:

The product consists of three core components, each designed to cater to different user needs and administrative roles. The **Web Application** serves as the main interface for the audience and players. It provides a platform for the audience to view live scores, match updates, and other event-related information. Players can also use this component to manage and update their personal profiles, offering a dynamic and engaging experience for those actively participating in the events.

The second component is the **Web Application (Admin Panel)**, which offers the Admin full control over the entire system. Through this panel, the admin can manage and configure match listings, oversee user accounts, and handle other critical system operations such as session management and security settings. This ensures that the system runs smoothly and allows the admin to make real-time adjustments as necessary.

Lastly, the **Admin Application / Webview** is designed for administrators responsible for updating match scores in real-time. This interface enables admins to input, modify, and track scores as the matches progress, ensuring that all data remains accurate and up-to-date. The Admin Application plays a crucial role in maintaining the integrity and flow of live events, ensuring that users and players have access to the latest match information.

Roles in the applications are: 

| **Role**   | **Description**                                                                                                                                                                         |
| ---------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **USER**   | Represents general users of the application, including roles such as Audience, Captains, and Umpires. Users can browse various components of the platform based on their specific role. |
| **ADMIN**  | Holds complete control over the system, including managing user accounts, overseeing match listings, configuring teams and squads, and terminating live user sessions when necessary.   |
| **SYSTEM** | Refers to programmatic actions and automated processes performed by the application, such as data updates, scheduled tasks, or system-generated changes.                                |
# **Player Registrations, Audience Access, and Profiles**

Players will undergo a progressive registration process, ensuring their profiles are built and updated gradually as they engage with the application. This allows for a personalized experience, where information is captured over time based on the player's interaction with the platform.

During registration, players will be required to provide the following essential details:

- **First Name**
- **Middle Name**
- **Last Name**
- **Phone Number**
- **Valid College Email ID ( ending with *@iiit-bh.ac.in)**
- **Gender**
- **Batch**
- **Branch**

Additionally, players have the option to include their social media profiles (e.g., links to their social handles), although this is not mandatory.

The **branch** field is particularly sensitive. In case of any changes, such as a branch transfer, players can raise an issue, which will be reviewed and resolved by `ADMIN` to ensure that all information remains accurate.

Future updates will introduce [[Form Fields]]
### After Registration

After registration, players will initially have  similar access to that of an unauthorized **AUDIENCE**. However, they will have additional capabilities that enhance their engagement and participation within the platform.
#### **Players can:**

- **Change their details**
- **Create Profiles**
- **Request to join teams**: Players can express interest in joining specific teams, which can be then approved / rejected by **Team Captains** ( more about this , later).
- **Leave a team**

### Profiles 

A **profile** is essentially a collection of information that helps to define and showcase an individual's skills, background, and specific attributes. For players, a profile serves as a personal identity card that not only provides basic details but also highlights their expertise, performance, and other relevant information. This helps both the player and the audience to better understand the player’s capabilities and strengths.

For example, consider **Saswat's Profile** in the context of a cricket player. It would include key details such as:

- **Sport**: Cricket
- **Position**: Batsman/Bowler/All-rounder
- **Batting Style**: Right-hand/Left-hand
- **Bowling Style**: Fast/Spin
- **Team**: CSE 2
- **Matches Played**: 45
- **Average Score**: 35
- **Wickets Taken**: 25
- **Best Performance**: 150 runs in a match, 5 wickets in an innings
- **Player Bio**: A brief description of the player’s cricket journey, strengths, and any notable achievements
- **Achievements**: This section typically highlights significant milestones, awards, or trophies earned throughout a player's career (However, in Saswat's case, there are currently no recorded cricket achievements, so this section will remain empty for now xD)

This profile will allow the audience to quickly identify the player’s strengths, role in the team, and notable achievements, creating a deeper connection with the audience and enhancing player visibility. For the player, it serves as a dynamic and evolving record of their skills and accomplishments, which can be updated as they progress in their sporting journey.

#future-scope
- **Self-Review**: In the future, players will have the ability to self-review their performance, gaining insights into their contributions and progress. This feature will help players evaluate their skills and growth, fostering a more self-driven approach to improvement.

#### **For the Audience**

The platform offers a public view system for Audience , allowing users to explore the application without the need for full registration. This feature enables audience members to access content such as match updates, team information, and live scores without requiring them to create a personal profile. The philosophy behind this approach is to promote open access and inclusivity, providing anyone the opportunity to casually engage with the platform. This allows users to familiarize themselves with the application and its offerings before deciding whether to create a personalized profile, making the platform accessible to all, regardless of their level of involvement.

# Admin Flows 

Admins can :
#### **Listings**

Admins have full control over [[Matches]], [[Teams]], [[Squads]] listings, allowing them to perform CRUD over them.
#### **Player Management (Enable/Disable/Remove)**

#### **Session Management (Terminate Sessions)**

For instance, if an admin notices a user violating platform rules, such as sending inappropriate messages during a live match, they can terminate the user's session immediately. This would disconnect the user in real-time, preventing further disruption and ensuring the platform remains secure and respectful for all participants.

#### **Umpire Assignment from Pool of Players**

[[Umpiring |Learn About Umpiring]]

Admins have the ability to promote players to the role of umpire from a pool of available players.

This allows them to assign umpires to matches as needed, ensuring the integrity of the game. The process of promoting players helps ensure that only qualified individuals are given umpiring responsibilities.

This functionality is important for maintaining a smooth and organized system, with the flexibility for admins to manage match operations effectively. Further details on this process will be outlined in the documentation.