
---
    title: Flask-and-Firebase-and-Pyrebase-Oh-my-upperlin
    date: 2021-01-01    
    draft: true
    tags: []
---
# Flask-and-Firebase-and-Pyrebase-Oh-my-upperlin## Connecting to your Firebase DB
To connect to your firebase database, you’ll need to set up a dictionary variable with your configuration data in your `routes.py` file.
Back to the routes.py file — once you’ve set up your config variable correctly, add the following code underneath:
This code connects to our project using our configuration data, and then creates a `db` variable to interact with the Firebase database that we created earlier.
Unfortunately that events list will not persist (save) our data, so we're going to replace this with a call to our firebase `db`variable:
To test if this worked (you won’t see anything change on the index page since we haven’t updated it yet), head to the Firebase Console and open up your project, clicking on the ‘database’ section.
You should see that the event you submitted is now a “node” in your database, under the node “events” (which was created as well since this was your first upload to that node — future submissions to `db.child("events")` will just add on to that node).
Next, inside of our `index()` method we'll create a new variabe called `db_events` that pulls in the data we want from Firebase (the "events" node), and we'll pass that in to our template for rendering:
Now reload your app and you should hopefully see data getting pulled in from your Firebase database!
- Add another field to your events form and then make sure that that content gets rendered correctly on your index page
- Build a similar app to inventory anything else you’re interested in: animals, groceries, todo items, etc.To test if this worked (you won’t see anything change on the index page since we haven’t updated it yet), head to the Firebase Console and open up your project, clicking on the ‘database’ section.
You should see that the event you submitted is now a “node” in your database, under the node “events” (which was created as well since this was your first upload to that node — future submissions to `db.child("events")` will just add on to that node).
