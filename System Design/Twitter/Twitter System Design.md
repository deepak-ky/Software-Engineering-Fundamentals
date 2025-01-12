
##### 1. Background

People can follow others, which can be mutual, meaning other users can follow them back.
But naturally some people will end up with more followers than others. 

This indicates that it will be a **[[Read Heavy vs Write Heavy Systems|Read Heavy System]]** as most users only browse tweets, while a small percentage will actually create tweets.

A typical tweet can contain upto 280 characters of text and may also include images and videos.

Each tweet has interactions at the bottom, allowing users to like, comment and retweet, and follow other users.

##### 2. Functional Requirements

1. Following : Users need to be able to follow other users
2. Tweeting : Users can create tweets. Tweets can contain
			- text (upto 280 characters)
			- images
			- videos
			- not including the premium feature of extended tweet length in this design
3. News Feed : Users need to see tweets from other people that they follow. 
			- not covering algorithmic "For you" feed

##### 3. Non Functional Requirements
Scale and performance demands that this system needs to handle.

###### Scale

X MAU : 500 Million : 5 * 10^8
   DAU  : 200 Million : 2 * 10^8

The average user follows around 100 users.
On average each user creates 10 daily tweets and read 100 tweets.

**Write Volume :** 
200 Million DAU * 10 Tweets : 2000 Million Tweets per day => 2 Billion new tweets daily

**Read Volume :** 
200 Million DAU * 100 Tweets : 20000 Million Tweets read per day => 20 Billion reads daily

**Data Size :**
Each tweet size can be 1KB on average if it's text only (have added a comment on the post) #review . If it contains attachments like images and videos, it can range from 1 MB to 5 MB.

For simplification, let us assume that average tweet size is 1 MB, even though some tweets with media can be larger.

This means we are dealing with 200M * 1MB = 20 petabytes of data read daily. #review


**Key Takeaways :
1. This is clearly a **read heavy** system. Meaning we should optimize for efficient reads.
2. The **data storage requirements** are huge, so we will need to consider **scalable storage solutions.**
3. Handling the **load of popular users** with millions of followers presents a unique challenge.

##### 4. API Design

Assumption: All requests are authenticated with the auth service before reaching our API, and we have a userId in each request.

![[Pasted image 20250112130757.png|500]]

1. **Create Tweet** 

```
Endpoint : 
POST /tweets

Request Parameters : 
a. content (string) : The text content of the tweet
b. mediaIds (array of strings, optional) : An arry of media IDs (for images,videos etc)
c. (Server side) userId (string) : obtained from authentication service
d. (Server side) createdAt (timestamp) : set by the server at the time of creation

Response Payload : 
a. tweetId (string) : The Id of the created tweet.
b. createdAt (timestamp) : The timestamp when the tweet was created.
c. success (boolean) : Indicates whether the tweet was created successfully
```

2. **Get Feed

```
Endpoint : 
GET /feed

Request Parameters : 
a. cursor (string,optional) : A pagination token to fetch the next set of tweets
b. (Server side) userId (string) : obtained from the authentication service

Response Payload :
a. tweets (array of objects) : An array of tweet objects, each containing : 
	* mediaIds (array of strings, optional) : An array of mediaId's
	* createdAt (timestamp) : creation timestamp
b. nextCursor (string, optional) : A pagination token to fetch the next set of tweets
```

3. **Follow a User

```
Endpoint : 
POST /follow/:userId

Request Parameters :
a. userId : userId of the "want to follow" user

Response Payload :
	b. success : Indicates whether the follow operation was successful
```

4. **Unfollow a User**

```
Endpoint : 
DELETE /follow/:userId

Request Parameters :
a. userId : userId of the "want to unfollow" user

Response Payload :
	b. success : Indicates whether the unfollow operation was successful
```


##### 4. High Level Design

**Client/Mobile App** : This is where the users will interact with the system by creating tweets, viewing feeds and following/unfollowing others - it's either the frontend browser app or the app on the user's phone.

**Load Balancer :** All requests will go through our load balancer, which distributes them across multiple application servers. This is essentially important in handling the **read heavy traffic** of our news feed.

