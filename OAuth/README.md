# OAuth


## Environment Variables

### Set
```
$ export TWITTER_KEY=<your_twitter_consumer_key>
```

### Get
```
ENV['TWITTER_KEY']
```




## OAuth 1.0

![IMGUR](http://i.imgur.com/Emfi1iU.png)




## OAuth 2.0

![IMGUR](http://i.imgur.com/t5gpQZ5.png)

### Resource Owner
- The person or application that owns the data that is to be shared.
  - e.g. a user on Facebook or Google.

### Resource Server
- The server hosting the resource owned by the resource server.
  - e.g. Facebook is, or has, a resource server.

### Client Application
- The application requesting access to the resources stored on the resource server.
  - e.g. a game requesting access to a user's Facebook account.

### Authorization Server
- The server authorizing the client app to access the resources of the resource owner.
- The authorization server and the resource server can be the same server, but it doesn't have to. The OAuth 2.0 specification does not say anything about how these two servers should communicate, if they are separate. This is an internal design decision to be made by the resource server + authorization server developers.





## Relevant Projects
- [Tweet Now! 2: Multi-User](http://socrates.devbootcamp.com/challenges/375)
  - [Repo](https://github.com/Ryan5231/tweet_now_multiUser)

## References
- [OAuth.net 2](http://oauth.net/2/)
- [Jenkov: OAuth 2.0 Roles](http://tutorials.jenkov.com/oauth2/roles.html)
