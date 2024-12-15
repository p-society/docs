### Journey

The match lifecycle starts with admins creating and managing match details. Key details include the teams involved, squad assignments, venue, date, and match status. Admins have full control over match creation, updates, and deletions, ensuring that matches are properly scheduled, rescheduled, or canceled as needed.
### Access Control

- **Admins:** Can create, edit, and delete matches.
- **Audience & Users:** Can only view upcoming and past matches, with no permission to modify match details.

### ERD (Entity Relationship Diagram)

| **Column** | **Type**    | **Description**                                                   |
| ---------- | ----------- | ----------------------------------------------------------------- |
| **id**     | `string`    | Primary key, unique identifier for the match                      |
| **team1**  | `string`    | Foreign key to the first team in the match                        |
| **team2**  | `string`    | Foreign key to the second team in the match                       |
| **squad1** | `string`    | Foreign key to the first squad                                    |
| **squad2** | `string`    | Foreign key to the second squad                                   |
| **umpire** | `string`    | Foreign key to the umpire assigned to the match                   |
| **venue**  | `string`    | Location of the match                                             |
| **date**   | `timestamp` | Date and time when the match takes place                          |
| **status** | `string`    | Current status of the match (e.g., Scheduled, Ongoing, Completed) |
Admins are responsible for setting the match's status and managing the overall lifecycle of the match.
