---
site: https://anypoint.mulesoft.com/apiplatform/popular/admin/#/dashboard/apis/17051/versions/18206/portal/pages/28702/edit
apiNotebookVersion: 1.1.67
title: Blogger
---

```javascript
load('https://github.com/chaijs/chai/releases/download/1.9.0/chai.js')
```

See http://chaijs.com/guide/styles/ for assertion styles

```javascript
assert = chai.assert 
```

```javascript
CLIENT_ID = prompt("Please, enter Client ID of your Google application.")
CLIENT_SECRET = prompt("Please, enter Client Secret of your Google application.")
```

```javascript
API.createClient('client', '#REF_TAG_DEFENITION');
```

```javascript
API.authenticate(client,"oauth_2_0",{
  clientId : CLIENT_ID,
  clientSecret : CLIENT_SECRET
})
```

```javascript
function getPath (post){
	var url = post.body.url
  var index = url.indexOf(".com") + ".com".length
  var path = url.substring(index)
  return path
}
```

```javascript
function selectComment(msg){
  var number = null
  var pageSize = -1
  var pagesCount = 1

  var searchResponse = client.blogs.blogId(ID_BLOG).posts.postId(ID_POST).comments.get()
  for(var i = 0 ; i < pagesCount ; i++ ){
    var comments = commentsResponse.body.items
    var message = msg
    message += "\n"
    for( var j in comments){
      message += "\n" + j + ": " + comments[j].content
    }
    var indStr = prompt(message)
    if(!indStr)
      break;

    ind = Number.parseInt(indStr)
    if(!(typeof ind === "number")||Number.isNaN(ind)||ind<0){
       break
    }
    if(ind>=0){
      return comments[ind]
    }  
  }
  return null
}
```

Retrieves a user by user ID

User ID

```javascript
ID_USER = "self"
```

```javascript
userResponse = client.users.userId(ID_USER).get()
```

```javascript
assert.equal( userResponse.status, 200 )
```

Retrieves a list of blogs 

```javascript
blogsResponse = client.users.userId(ID_USER).blogs.get()
```

```javascript
assert.equal( blogsResponse.status, 200 )
ID_BLOG = blogsResponse.body.items[0].id
```

Gets one blog and user info pair by blogId and userId

```javascript
blogResponse = client.users.userId(ID_USER).blogs.blogId(ID_BLOG).get()
```

```javascript
assert.equal( blogResponse.status, 200 )
```

Adds a post

```javascript
postsCreateResponse = client.blogs.blogId(ID_BLOG).posts.post({
  "title" : "Notebook test post" ,
  "content" : "Test content" 
})
```

```javascript
assert.equal( postsCreateResponse.status, 200 )
ID_POST = postsCreateResponse.body.id
PATH = getPath(postsCreateResponse)
```

Retrieves a post by path

```javascript
bypathResponse = client.blogs.blogId(ID_BLOG).posts.bypath.get({
  "path": PATH
})
```

```javascript
assert.equal( bypathResponse.status, 200 )
```

Retrieves a list of post and post user info pairs, possibly filtered. The post user info contains per-user information about the post, such as access rights, specific to the user

```javascript
postsResponse = client.users.userId(ID_USER).blogs.blogId(ID_BLOG).posts.get()
```

```javascript
assert.equal( postsResponse.status, 200 )
```

Gets one post and user info pair by postId and userId

```javascript
postResponse = client.users.userId(ID_USER).blogs.blogId(ID_BLOG).posts.postId(ID_POST).get()
```

```javascript
assert.equal( postResponse.status, 200 )
```

Retrieves a blog by its ID

```javascript
blogResponse = client.blogs.blogId(ID_BLOG).get()
```

```javascript
assert.equal( blogResponse.status, 200 )
```

Retrieves the comments for a blog, across all posts, possibly filtered

```javascript
commentsResponse = client.blogs.blogId(ID_BLOG).comments.get()
```

```javascript
assert.equal( commentsResponse.status, 200 )
```

Retrieves the list of pages for a blog

```javascript
pagesResponse = client.blogs.blogId(ID_BLOG).pages.get()
```

```javascript
assert.equal( pagesResponse.status, 200 )
```

Add a page

```javascript
pagesCreateResponse = client.blogs.blogId(ID_BLOG).pages.post({
  "title" : "Notebook test page" ,
  "content" : "Page content" 
})
```

```javascript
assert.equal( pagesCreateResponse.status, 200 )
ID_PAGE = pagesCreateResponse.body.id
```

Retrieves one pages resource by its page ID

```javascript
pageResponse = client.blogs.blogId(ID_BLOG).pages.pageId(ID_PAGE).get()
```

```javascript
assert.equal( pageResponse.status, 200 )
```

Update a page

```javascript
pageUpdateResponse = client.blogs.blogId(ID_BLOG).pages.pageId(ID_PAGE).put({
  "title" : "Updated notebook page" ,
  "content" : "Updated page content" 
})
```

```javascript
assert.equal( pageUpdateResponse.status, 200 )
```

Update a page. This method supports patch semantics

```javascript
pagePatchResponse = client.blogs.blogId(ID_BLOG).pages.pageId(ID_PAGE).patch({
  "title" : "Notebook pachted page" ,
  "content" : "Patched page content" 
})
```

```javascript
assert.equal( pagePatchResponse.status, 200 )
```

Retrieves a list of posts

```javascript
postsResponse = client.blogs.blogId(ID_BLOG).posts.get()
```

```javascript
assert.equal( postsResponse.status, 200 )
```

Retrieves one post by post ID

```javascript
postResponse = client.blogs.blogId(ID_BLOG).posts.postId(ID_POST).get()
```

```javascript
assert.equal( postResponse.status, 200 )
```

Updates a post

```javascript
postUpdateResponse = client.blogs.blogId(ID_BLOG).posts.postId(ID_POST).put({
  "title" : "Updated notebook post" ,
  "content" : "Updated test content" 
})
```

```javascript
assert.equal( postUpdateResponse.status, 200 )
```

Updates a post. This method supports patch semantics

```javascript
postPatchResponse = client.blogs.blogId(ID_BLOG).posts.postId(ID_POST).patch({
  "title" : "Patched notebook test post" ,
  "content" : "Patched test content" 
})
```

```javascript
assert.equal( postPatchResponse.status, 200 )
```

Retrieves the list of comments for a post

```javascript
alert('Now you should visit your blog web page and leave a comment for \'Notebook test post\'. After click button \'OK\' please.')
```

```javascript
commentsResponse = client.blogs.blogId(ID_BLOG).posts.postId(ID_POST).comments.get()
```

```javascript
assert.equal( commentsResponse.status, 200 )
COMMENT = selectComment("Please, select your comment by entering its index.")
ID_COMMENT = COMMENT.id
```

Retrieves one comment resource by its commentId

```javascript
commentResponse = client.blogs.blogId(ID_BLOG).posts.postId(ID_POST).comments.commentId(ID_COMMENT).get()
```

```javascript
assert.equal( commentResponse.status, 200 )
```

Marks a comment as spam. This will set the status of the comment to spam, and hide it in the default comment rendering

```javascript
spamCreateResponse = client.blogs.blogId(ID_BLOG).posts.postId(ID_POST).comments.commentId(ID_COMMENT).spam.post()
```

```javascript
assert.equal( spamCreateResponse.status, 200 )
```

Marks a comment as not spam

```javascript
approveCreateResponse = client.blogs.blogId(ID_BLOG).posts.postId(ID_POST).comments.commentId(ID_COMMENT).approve.post()
```

```javascript
assert.equal( approveCreateResponse.status, 200 )
```

Removes the content of a comment

```javascript
removecontentCreateResponse = client.blogs.blogId(ID_BLOG).posts.postId(ID_POST).comments.commentId(ID_COMMENT).removecontent.post()
```

```javascript
assert.equal( removecontentCreateResponse.status, 200 )
```

Delete a comment by ID

```javascript
commentDeleteResponse = client.blogs.blogId(ID_BLOG).posts.postId(ID_POST).comments.commentId(ID_COMMENT).delete()
```

```javascript
assert.equal( commentDeleteResponse.status, 204 )
```

Publish a draft post

```javascript
publishCreateResponse = client.blogs.blogId(ID_BLOG).posts.postId(ID_POST).publish.post()
```

```javascript
assert.equal( publishCreateResponse.status, 200 )
```

Revert a published or scheduled post to draft state, which removes the post from the publicly viewable content

```javascript
revertCreateResponse = client.blogs.blogId(ID_BLOG).posts.postId(ID_POST).revert.post()
```

```javascript
assert.equal( revertCreateResponse.status, 200 )
```

Searches for a post that matches the given query terms

```javascript
searchResponse = client.blogs.blogId(ID_BLOG).posts.search.get({
  "q": "Notebook"
})
```

```javascript
assert.equal( searchResponse.status, 200 )
```

Retrieve pageview stats for a Blog

```javascript
pageviewsResponse = client.blogs.blogId(ID_BLOG).pageviews.get()
```

```javascript
assert.equal( pageviewsResponse.status, 200 )
```

Retrieves a blog by URL

```javascript
byurlResponse = client.blogs.byurl.get({
  "url": "http://code.blogger.com/"
})
```

```javascript
assert.equal( byurlResponse.status, 200 )
```

Delete a page by ID

```javascript
pageDeleteResponse = client.blogs.blogId(ID_BLOG).pages.pageId(ID_PAGE).delete()
```

```javascript
assert.equal( pageDeleteResponse.status, 204 )
```

Deletes a post by ID

```javascript
postDeleteResponse = client.blogs.blogId(ID_BLOG).posts.postId(ID_POST).delete()
```

```javascript
assert.equal( postDeleteResponse.status, 204 )
```