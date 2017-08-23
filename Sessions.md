# Sessions
## What are session? 


A sessions is the unique identification of a user which is sent to the users browser as a cookie or as a GET request. Sessions end when the user closes the browser, or when the web server deletes the session information, or when the programmer explicitly destroys the session.


## How are sessions used?


A session is a place to store data that you want access to across requests. Each user that visits your website has a unique session.  You can use sessions to store and access user data as they browse your application. A use case example would be ad relevancy when browsing websites.


## How are sessions stored? 


Sessions can store their information in different ways. The popular ways to store session data is:

In a cookie
In application memory
In a memory cache
In a database


## Cookie Session:


![Image](https://i2.wp.com/nodewebapps.com/wp-content/uploads/2017/06/sessions-1.png?w=750)


## Application Memory Session:


Storing session data in application memory essentially means that the data is stored for the lifetime of your application runtime. If your web application server crashes or is stopped, all session data is removed. An applicaton memory example would be storing items in a shopping cart while visiting an ecommerce website. 


## Memory Cache Session:


The memory cache is a temporary storage location on your computer for files downloaded by your browser to display websites. A usecase example:


![Image](https://i2.wp.com/nodewebapps.com/wp-content/uploads/2017/06/sessions-2.png?w=855)




## Database Session: 


Lastly, let’s talk about storing session data in a traditional database, like MySQL or PostgreSQL. For most cases, this works in a very similar way to storing session data in a memory store.

The session cookie still contains a sessionId, however In this case, it will map to the primary key of the Session table on the database.



```javascript
var express = require('express');
var session = require('express-session') // require express session

var app = express();

// Use the session middleware
app.use(session({ secret: 'keyboard cat', cookie: { maxAge: 5000 }}))

// Access the session as req.session
app.get('/', function(req, res, next) {
  if (req.session.views) {
    req.session.views++
    res.setHeader('Content-Type', 'text/html')
    res.write('<p>views: ' + req.session.views + '</p>')
    res.write('<p>expires in: ' + (req.session.cookie.maxAge / 1000) + 's</p>')
    res.end()
  } else {
    req.session.views = 1
    res.end('welcome to the session demo. refresh!')
  }
})


app.listen(3000, function(err) {
   if (err) throw err;
   console.log("Server is Running");
});

```








