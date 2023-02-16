---
                title: Developing-a-Single-Page-App-with-Flask-and-Vue-js
                date: 2021-01-01    
                draft: true
                tags: []
               ---


            # Developing-a-Single-Page-App-with-Flask-and-Vue-js

>
Install:
Enable the Bootstrap Vue library in *client/src/main.js*:
## POST Route
### Server
Update the existing route handler to handle POST requests for adding a new book:
Update the imports:
With the Flask server running, you can test the POST route in a new terminal tab:
You should see:
You should also see the new book in the response from the [http://localhost:5000/books](http://localhost:5000/books) endpoint.[Developing%20a%20Single%20Page%20App%20with%20Flask%20and%20Vue%20js%20900a7939c8244b579780a034209512c4/add-new-book.gif](Developing%20a%20Single%20Page%20App%20with%20Flask%20and%20Vue%20js%20900a7939c8244b579780a034209512c4/add-new-book.gif)
## Alert Component
Next, let's add an [Alert](https://bootstrap-vue.js.org/docs/components/alert/) component to display a message to the end user after a new book is added.[Developing%20a%20Single%20Page%20App%20with%20Flask%20and%20Vue%20js%20900a7939c8244b579780a034209512c4/alert-2.png](Developing%20a%20Single%20Page%20App%20with%20Flask%20and%20Vue%20js%20900a7939c8244b579780a034209512c4/alert-2.png)
To make it dynamic, so that a custom message is passed down, use a [binding expression](https://vuejs.org/v2/guide/syntax.html#v-bind-Shorthand) in *Books.vue*:
Add the `message` to the `data` options, in *Books.vue* as well:
Then, within `addBook`, update the message:
Finally, add a `v-if`, so the alert is only displayed if `showMessage` is true:
Add `showMessage` to the `data`:
Update `addBook` again, setting `showMessage` to `true`:
Test it out!Handle cancel button click
### (1) Add modal and form
First, add a new modal to the template, just below the first modal:
Add the form state to the `data` part of the `script` section:
> Challenge: Instead of using a new modal, try using the same modal for handling both POST and PUT requests.>
### (2) Handle update button click
Update the "update" button in the table:
Add a new method to update the values in `editForm`:
Then, add a method to handle the form submit:
### (3) Wire up AJAX request
### (4) Alert user
Update `updateBook`:
### (5) Handle cancel button click
Add method:
Update `initForm`:
Make sure to review the code before moving on.[Developing%20a%20Single%20Page%20App%20with%20Flask%20and%20Vue%20js%20900a7939c8244b579780a034209512c4/update-book.gif](Developing%20a%20Single%20Page%20App%20with%20Flask%20and%20Vue%20js%20900a7939c8244b579780a034209512c4/update-book.gif)
## DELETE Route
### Server
Update the route handler:
### Client
Update the "delete" button like so:
Add the methods to handle the button click and then remove the book:
Now, when the user clicks the delete button, the `onDeleteBook` method is fired, which, in turn, fires the `removeBook` method.[Developing%20a%20Single%20Page%20App%20with%20Flask%20and%20Vue%20js%20900a7939c8244b579780a034209512c4/developing_spa_flask_vue.png](Developing%20a%20Single%20Page%20App%20with%20Flask%20and%20Vue%20js%20900a7939c8244b579780a034209512c4/developing_spa_flask_vue.png)
## Developing a Single Page App with Flask and Vue.js
The following is a step-by-step walkthrough of how to set up a basic CRUD app with Vue and Flask.