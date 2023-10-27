# SASS Talent Assessment

The following is a simple set of questions related to Ruby on Rails and general troubleshooting skills. The answers to these questions need to be written in a Google Docs document and shared with the interviewers; you will have 30 minutes to complete the questions (believe me, they are very easy). Whenever required to provide code, you can either type the code directly into the document, attach a screenshot of your code, or provide a Github link with the requested code.

1. What’s your strongest skill (Queries, Rails, Ruby )? During our in-person interview, we will focus on your strongest skill.

2. Within Rails, we have a model named ‘User’. The User table has only 2 relevant fields: ‘name’ (string) and ‘active’ (boolean). We have two controllers with index methods where we need to find active users (SessionController and ApiController). Write simple code for all three classes (2 or 3 liner codes ) (1 model, 2 controllers ).  You don’t need to worry about security etc.

3. If we are having a production issue, how would you go about troubleshooting it? Let’s assume we are a new company, and you are the lead over this project, and nothing is set up correctly. What steps would you take to make sure we can troubleshoot any production issues going forward?

4. Let’s create another model, ‘Person’, with two fields: name and active, just like the User model. Any time a user is added, it needs to be added to Person as well.
Let's add another method to ApiController called create. We will create a User with your name and active set to true. Please add it to Person after you create a User.

5. Someone points out that even though a User is being created, a Person isn't being created. How would you go about troubleshooting it?

### Solution

[View Solution](./readme.md)
