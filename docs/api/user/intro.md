While all the other endpoints behave the same, this one is a bit special as we deal with private information like emails.

### Anonymous users

The following actions cannot be done:

1.  Create a new user via a POST
2.  Update an existing user via a PUT
3.  Delete an existing user via a DEL

Read action will only return username and locale for that user.

### Authenticated users

The following actions cannot be done:

1.  Create a new user via a POST
2.  Update an existing user via a PUT different than the same user
3.  Delete an existing user via a DEL

Read action will only return user name and locale for that user. If the
user access its page, then all the information will be available to
him/her.

### Admin users

The following actions cannot be done:

1.  Create a new user via a POST
2.  Delete an existing user via a DEL

Read action can be done by any user. The admins will have access to the
User IDs. This will be helpful in case that you want to give, for
example, badges, for users when using our webhooks solution. Each user
has in the info field a new field named **extra** where that information
(or anything else) could be stored.
