# For 
Students who want quick help understanding course concepts
# Who
Learners who get caught up on a problem when studying alone
# The 
Peer-to-Peer Q&A web app
# That
Provides solutions and assistance from other students using the concepts that were talked about in class
# Unlike
Discord it is structured around the course's concepts making it easier to find your question

Stack Overflow the answers will always align with what is taught in the course and will not use advanced topics that have not been covered by the class
# Our Product
</Name> will provide the assistance using what has been brought up in the course to ensure, as well as being organized for the multiple courses a student may be taking.

## MVP:
- User Auth
- Create Profile
- Create Course
- Create Question (Help Request)
- Create Answer 
## Iteration:
- Searching
- User Roles (Teacher/TA)
- Analytics
- Reputation/ Rating
- Notifications
- Formatting (Markdown/Code Blocks)
## Advanced Stretch Goals:
- Images
	- Require Blob storage
- Points/XP (Gameification)
	- Achievements
- AI-assisted Support
	- Generate a Response


{courseid, name,desc} Course Table one to many
{Course ID, post ID} Course-Post Many to Many
{UserID, Password (salted), (Salt),last login} User Table
{Postid,userid (optional), content, reply id(postid), reputation, last_interact} Post Table
{tagid,name} Tags Table
{tagid, postid} Tags-Posts