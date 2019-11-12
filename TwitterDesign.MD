
# This document is meant to provide an overview of how to approach the desing of Twitter service.

## Core concepts when it comes to any desing question is to focus on:
1. Converse about a couple of features.
2. Show that you have a good grasp of the service and concepts around it.
3. You can talk about different topics concerning the several technology items within your design.
4. Identify some core features your design will cover.

Staring off: The core features (Do not talk about the whole twitter, it is practically impossible to cover all the desing concepts of the twitter service in a single session like an interview). You want to focus on some core features "of your choice" during the interview.
For this assignment you may pick out some below (These are my choices), you are free to extend them if you have more time.

## Core features:

1. Tweeting (sending a tweet).
2. Having a timeline where you see feeds from the people you follow. Here you can have two things see own tweet as a user and the people you follow and their tweets.
3. Following a person.

To start with a design flow. You can start off by giving a naive approach and later a more refined approach.

### Naive approach ( where you have two tables, a TWEETS table and USER table.)

The TWEET table will have below fields:
1. ID (Autoincrement field)
2. TWEET (Char*, could be long text)
3. USER_ID_FK (Long datatype) --  Foreign key reference to USER table, having a n to 1 relationship with ID of USER table.

USER table will have the below fields.
1. ID (Autoincrement)
2. NAME (Char*)

A common flow would be a person tweets, and the service has to update the tweets table and a push notification sent to all followers by selecting the entire followers list for each tweet. This is also bound to happen to all updates and responses. If you take a look at corner cases of this implementation, if you have a user like Jay-Z with 1 Million followers, the database will experience some latency and the maintainance is going to be hectic. You could attempt to do optimizations like sharding and vertical scaling, but there is just as miuch you can do to serve everyone. Second edge case, when there is a mor event like the infamous KOT vs SouthAfrican on tweeter, this a good corener case where the service and database hits could last days with high availability being of a very big concern.
At this point as you may have noticed. I picked up a term (Availability) and I will add another one called Consitency. For such a service 
Both need to be balanced out to provide a good user experience. 
By Consistency, we refer to Eventual consitency, meaning once data is written to a database successfully, queries that follow are able to access the data and get a consistent view of the data. Availability is pretty much self explanatory, this refers to how "available" is the service, with this the reference point being the data, a user wants to come and join a tweet and find the initial post of the person you follow and be able to read the responses of everyone.

Moving away from the naive approach.

### Precomputing the followers.




