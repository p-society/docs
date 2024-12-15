### Journey

The match lifecycle starts with admins creating and managing match details. Key details include the teams involved, squad assignments, venue, date, and match status. Admins have full control over match creation, updates, and deletions, ensuring that matches are properly scheduled, rescheduled, or canceled as needed.

**Match Model Fields:**

- **[[Teams]]:** Two teams (team1 and team2) are assigned to each match.
- [[S]]:** Each team has an associated squad (squad1 and squad2), which are required for the match.
- **Admin:** The admin responsible for the match is assigned through the `assignedAdmin` field.
- **Venue & Date:** The location and timing of the match are specified.
- **Status:** The match status (e.g., "Scheduled," "Ongoing," "Completed") is tracked.

Admins are responsible for setting the match's status and managing the overall lifecycle of the match.

### Access Control

- **Admins:** Can create, edit, and delete matches.
- **Audience & Users:** Can only view upcoming and past matches, with no permission to modify match details.

### ERD (Entity Relationship Diagram)

The database schema for the match system involves several key entities:

- **Match:** Contains details like teams, squads, venue, date, and match status.
- **Team:** Each match involves two teams.
- **Squad:** Each team has an associated squad.
- **Admin:** Admins manage the match creation and lifecycle.

The **ERD** visually represents how these entities are related, with `Match` linked to `Team`, `Squad`, and `Admin` via references (foreign keys). An SQL schema can be used to generate this ERD, which illustrates the relationships and constraints between the entities.