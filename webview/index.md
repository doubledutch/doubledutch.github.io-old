## Web View sections in a DoubleDutch event app

### Getting Started

A web view can be embedded in any DoubleDutch event app via the DoubleDutch Studio or CMS.

> Layout > Add New Section > Web View

Insert the URL of the web page to load.  HTTPS is preferred. It can be an existing web page such as a
[Twitter feed](https://twitter.com/DoubleDutch) or a custom page that your build and host.

### Custom pages

A custom page can take advantage of the DoubleDutch Javascript SDK for accessing basic user and event information
when referened as a Web View section in a DoubleDutch app.  Just include the
[DDEventsSDK.js](https://github.com/doubledutch/sdk/blob/master/DDEventsSDK.js) script, and your Javascript in the
page can query for event data.

```js
DD.Events.onReady(() => {
  DD.Events.getCurrentUserAsync(user => {
    const { ImageUrl, FirstName, LastName, Company, Title, UserIdentifierId, EmailAddress, UserName } = user
    console.log(`Hello, ${FirstName} ${LastName}`)
  })
  
  DD.Events.getCurrentEventAsync(event => {
    const { Icon, Name, Description, StartDate, EndDate } = event
    console.log(`Welcome to ${Name}`)
  })
})
```

See this [live example](http://jsbin.com/vakitax/edit?html,js,output)

### Redirect with context

Sometimes, you may want to redirect to another page, passing some event or user information as context in the query
string. The following URL can be embedded as a web view to achieve that.  User and event variables will be replaced
in the query string at runtime to redirect to the `redirect_uri` specified. Note that your `redirect_uri` must be
[URL-encoded](https://www.urlencoder.org/).

For example, to do a search for the current attendee's first and last name on Google...

1. Construct the URL with placeholders:

   ```
   https://google.com/search?q=${user.FirstName}+${user.LastName}
   ```

2. [URL-encode](https://www.urlencoder.org/) it:

   ```
   https%3A%2F%2Fgoogle.com%2Fsearch%3Fq%3D%24%7Buser.FirstName%7D%2B%24%7Buser.LastName%7D
   ```

3. Set it as the `redirect_uri` of our redirect page:

   ```
   https://ria-static.s3.amazonaws.com/pages/forward.html?redirect_uri=https%3A%2F%2Fgoogle.com%2Fsearch%3Fq%3D%24%7Buser.FirstName%7D%2B%24%7Buser.LastName%7D
   ```
   
Note that redirecting to a page with email address, username, ID, etc. in the query string is *NOT* a secure method
of authentication, as it can be easily spoofed.  For secure authentication, a current user token placeholder, `${token}`,
can be referenced in your URL if your URL is `https://`, e.g.

```
https://mysite.com?token=${token}
```

Your server can [decode and verify this token](https://github.com/doubledutch/verify-user-token) for secure authentication
to your web page.
