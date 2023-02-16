---
                title: Hosting-Flask-servers-on-Firebase-from-scratch-F
                date: 2021-01-01    
                draft: true
                tags: []
               ---


            # Hosting-Flask-servers-on-Firebase-from-scratch-F

## Any server backend with Cloud Run
With Firebase Hosting integrating with Cloud Run, you can generate content from anything that fits within a stateless Docker container.## Cloud Run has a free tier
To use Cloud Run with Firebase Hosting you currently need billing enabled, which requires putting a credit card on file.Now it’s time to set up Firebase Hosting to serve your static files and the content generated with Cloud Run.From the root of the project run the following command:
```
./node_modules/.bin/firebase init hosting
```
This calls the locally installed Firebase CLI to set up Firebase Hosting within your project.To delete then file, run the following command from the root of the project:
```
rm static/index.html # Mac/Linux
del static/index.html # Windows
```
## Add a style.css in the static directory
To add some style to your web app, create a`static/style.css` file with the following contents:
With the project set up locally, we can hook up Cloud Run to Firebase Hosting.During this 10 minute period Firebase Hosting will skip running your server code in Cloud Run and serve the cache content directly.Run the following commands:
```
gcloud builds submit --tag gcr.io//flask-fire
gcloud beta run deploy --image gcr.io//flask-fire
```
This build the container in Cloud Build and deploy to Cloud Run.