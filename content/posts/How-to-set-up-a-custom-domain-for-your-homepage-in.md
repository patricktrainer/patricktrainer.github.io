
---
    title: How-to-set-up-a-custom-domain-for-your-homepage-in
    date: 2021-01-01    
    draft: true
    tags: []
---
# How-to-set-up-a-custom-domain-for-your-homepage-in# How to set up a custom domain for your homepage in Notion
Created: January 29, 2020 9:01 AM
Tags: How To
URL: https://medium.com/@TarasPyoneer/how-to-set-up-a-custom-domain-for-your-homepage-in-notion-53fa3d54f848
!
Notion itself does not provide this function yet, according to their twitter we might see it someday:
Luckily I have found this [gist](https://gist.github.com/mayneyao/b9fefc9625b76f70488e5d8c2a99315d) from [mayneyao](https://gist.github.com/mayneyao).
And this is why I decided to create a step by step guide on how to set up custom domains for Notion.
To follow this tutorial, you will need:
* Custom domain and access to the DNS settings * Page in Notion that should be your landing page * Account on [CloudFlare](https://www.cloudflare.com/)
Let’s start with the page itself.
For our use case, we will make use of the **Workers** feature that will forward incoming requests from users to the public Notion page that we have created earlier.
Modify them using your domain in *your domain* and public Notion page in *start page url*.
If everything went smoothly and the * Notion page is set to public * the nameservers on your domain provider were changed * CloufFlare successfully verified your domain
You should be able to see your public Notion page after entering your domain in the URL of your browser:
Each use-case is different.
