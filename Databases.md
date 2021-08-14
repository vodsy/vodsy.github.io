#### [Home](/)

## Databases


  The artifact that I have chosen for the databases category is my personal web application project: the recipe sharing app. With so much user interaction happening and with the recipe-sharing idea being rooted in social media the databases are fairly complex. I currently have 8 different database tables, most of which are connected to each other through many-to-many and one-to-one (similar to foreign key) relationships. These relationships allow recipes to be linked to users, users to collect recipes, users to follow users, users to have photos, photos to be linked to recipes, recipes to have tags, etc. One enhancement that I need to make is I need to perform more than a basic cleaning of the user-supplied data that is going to the database. It is a SQL database, meaning that it is relatively vulnerable to injection attacks.
  
  
  I have built this web application (and many others) using the Django framework. It is very robust and has a great object relational mapper (ORM) built in for SQL databases. During development I use an SQLite database but when I deploy, I migrate it to a PostgreSQL. Django has built-in data cleaning; however, it is fairly light cleaning and leaves some gaps that need to be filled. To fill those gaps, I created a function named “MakeFriendly” that takes a string as an input, strips all non-word characters (everything except numbers and letters) using regular expressions, and returns the altered string. There is no threat of numeric overflow or underflow in Django/Python, so I am not worried about the numeric user inputs (I have still added a limit though as this is good practice). I call my “MakeFriendly” function on all other user inputs, like the user profile bio, recipe names, etc. These are the inputs where a user could attempt a SQL injection attack. I believe this enhancement will help make my web application even more robust and will make maintaining it easier: if I need to enhance the cleaning, I can just change the “MakeFriendly” function. Please see my function and how it is called in the images below.


![image](https://user-images.githubusercontent.com/57910664/129358055-d42b9baa-1c01-4753-bc66-74758a1eb2e4.png)
_Figure 1: The "MakeFriendly" function takes a string and strips it of all non-word characters using regular expressions. This helps remove a malicious user's ability to perform a SQL injection attack_




![image](https://user-images.githubusercontent.com/57910664/129358104-746dd66c-a9d5-46bb-8eed-a86b2261b422.png)
_Figure 2: Examples of where I have used the "MakeFriendly" function to clean user-supplied data_
