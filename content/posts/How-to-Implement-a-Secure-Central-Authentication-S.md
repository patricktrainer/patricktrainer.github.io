
---
    title: How-to-Implement-a-Secure-Central-Authentication-S
    date: 2021-01-01    
    draft: true
    tags: []
---
# How-to-Implement-a-Secure-Central-Authentication-S[How%20to%20Implement%20a%20Secure%20Central%20Authentication%20S%2062529fc47abc4199930b2db48f5fcd28/002_Shop_isolation_of_users_2x_e46bda9c-6859-4248-86c3-a696f7281e63.jpg](How%20to%20Implement%20a%20Secure%20Central%20Authentication%20S%2062529fc47abc4199930b2db48f5fcd28/002_Shop_isolation_of_users_2x_e46bda9c-6859-4248-86c3-a696f7281e63.jpg)
Shop isolation of users
# Modelling User Accounts Within Identity
User accounts modelled within our Identity service are two important types: Identity accounts and Legacy accounts.
can only access Shops
We ensured that new accounts are created as Identity accounts and that existing users with legacy accounts can be safely and securely upgraded to Identity accounts.
Prompt Users to Combine Their Accounts Together
Users with an email address that can sign into more than one single Shopify service are prompted to combine their accounts together into a single Identity account.
Inside a single database transaction create the complete new account, associate destinations from legacy accounts to it, and delete the old accounts
We needed to do this inside a transaction after getting all of the information from a user to prevent the potential for reducing the security of their accounts.
If a user was using 2FA before starting this process and we created the Identity account immediately after the new password was provided, there exists a small window of time when their new Identity account would be less secure than their old legacy accounts.
Some of the more complex pieces of logic for this process included finding all of the related accounts for a given email address and the information about the destinations they had access to, replacing the legacy accounts when creating the Identity account, and ensuring that the Identity account was setup correctly with all of the required data defined correctly.
# Build New Experiences for Shopify Users That Rely on SSO Identity Accounts
As of the time of this writing over 75% of active user accounts have been auto-upgraded or combined into a single Identity account.
