##### [Home](/)

## Software Design and Engineering 
 
 
 Everything that I have learned so far as a computer science student has culminated in my most recent personal project: a recipe-sharing web application. This project pushed the boundaries on my software engineering and design skills because of the level of user interaction, the way this interaction translates to the front end, and the way it is handled on the back end. While this is still a work in progress and there is a lot of functionality I still want to add, the enhancement I decided to make to the software design is how users search for recipes. I was using a custom-weighted search vector with results that update as you type using asynchronous JavaScript and XML (AJAX) search. While creating this feature certainly felt like an accomplishment, I believe it was a clunky design that took away from the user experience. This design also invariably made it nearly impossible to filter a specific category of recipes while being linked from another page (i.e. click “Breakfast Recipes” on home page and it brings you to the browse page showing only breakfast recipes).


  I have replaced this search with a more “classic” search bar that returns results after the user enters their query. Aside from the benefit to the user experience while searching, this new method also makes less calls to the database. This is an important improvement for when my app goes live and there are many users. The way I set up the “classic” search bar to work includes the user’s search in the URL. This has one main benefit that I am interested in and that is how this improves the way my app will interact with search engines. A search engine search for a particular type of recipe can yield my app as a result with the search already performed. While the way I have done it works, I eventually want to include canonical URLs for my database objects which will have the best effect on search engine searching and my app coming up.


![image](https://user-images.githubusercontent.com/57910664/129350622-9332142e-85ec-4a02-a81a-870d730ce96a.png)
_Figure 1: I added a new view to views.py and simplified the original view. Now, instead of real-time updates with AJAX a new page is loaded with each search._




![image](https://user-images.githubusercontent.com/57910664/129351007-247182b1-bfd2-4bc6-9b0d-d96c573d58c2.png)
_Figure 2: I had to add a new URL path (third path from the bottom) to accommodate the new search method. Each search calls the new path and the query is evaluated in the views.py file._




![image](https://user-images.githubusercontent.com/57910664/129351083-d128958a-2d26-4b9d-a78d-d684cd9bb5b1.png)
_Figure 3: I removed the partial HTML page that was required for real-time updates and instead made one HTML file. You can see the HTTP GET logic in the form near the top of the file._




![image](https://user-images.githubusercontent.com/57910664/129351146-0f38dbe0-d2d4-4049-bc3f-540b1483ae50.png)
_Figure 4: A screenshot of the new search bar._
