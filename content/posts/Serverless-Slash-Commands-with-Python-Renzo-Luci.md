
---
    title: Serverless-Slash-Commands-with-Python-Renzo-Luci
    date: 2021-01-01    
    draft: true
    tags: []
---
# Serverless-Slash-Commands-with-Python-Renzo-Luci# Serverless Slash Commands with Python - Renzo Lucioni
Created: February 21, 2020 12:03 PM
URL: https://renzo.lucioni.xyz/serverless-slash-commands-with-python/
Slack’s [slash commands](https://api.slack.com/slash-commands) allow you to perform actions by typing commands into Slack.
[Serverless%20Slash%20Commands%20with%20Python%20-%20Renzo%20Luci%2094a762f9efaa44ad83e6a523a512da4e/hello-there-app-credentials_hu183e95f920966d8fe95c9761fdfb32b9_29554_500x500_fit_lanczos_2.png](Serverless%20Slash%20Commands%20with%20Python%20-%20Renzo%20Luci%2094a762f9efaa44ad83e6a523a512da4e/hello-there-app-credentials_hu183e95f920966d8fe95c9761fdfb32b9_29554_500x500_fit_lanczos_2.png)
You’re going to create a command invoked with `/hello-there` which responds with [“General Kenobi!”](https://youtu.be/frszEJb0aOo) whenever the command is run.
[Serverless%20Slash%20Commands%20with%20Python%20-%20Renzo%20Luci%2094a762f9efaa44ad83e6a523a512da4e/hello-there-team-id_hu41e0fba4d4b1057f776459be142ef28a_17546_500x500_fit_lanczos_2.png](Serverless%20Slash%20Commands%20with%20Python%20-%20Renzo%20Luci%2094a762f9efaa44ad83e6a523a512da4e/hello-there-team-id_hu41e0fba4d4b1057f776459be142ef28a_17546_500x500_fit_lanczos_2.png)
See Slack’s [command validation](https://api.slack.com/slash-commands#validating_the_command) docs for more details about what’s going on in `is_request_valid()`.
Zappa creates a Lambda function containing your Flask app and sets up a wildcard API Gateway route to proxy requests from Slack to the app.
Then, just like before, navigate back to your app’s “Slash Commands” section in your browser and edit the configuration of the `/hello-there` command, replacing the ngrok forwarding URL with the API Gateway URL.
To be more faithful to the scene from Revenge of the Sith, you now want your `/hello-there` command to respond with [“General Kenobi!”](https://youtu.be/frszEJb0aOo), followed 5 seconds later by “You *are* a bold one.” Your command’s backend has to do more work now: receive a POST request, verify that the request was issued by Slack, schedule a task that will issue the second message 5 seconds in the future, and respond immediately with the first message.
### Slash Command Best Practices
Slack lists a variety of slash command [best practices](https://api.slack.com/slash-commands#best_practices) in their docs.
