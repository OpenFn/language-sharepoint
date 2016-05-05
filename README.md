Language SharePoint
===================

Language Pack for building expressions and operations for working with
the [SharePoint REST API](https://msdn.microsoft.com/en-us/library/office/jj164022.aspx).

Documentation
-------------
## Events API

#### Desired create expression:
```js
create("SP.List", fields(
  field("Title", "New title"),
  field(...),
  field(...)
))
```
#### Desired update expression:
```js
// url: "http://<site url>/_api/web/lists/GetByTitle('Test')",
update("SP.List", "Original Title", fields(
  field("Title", "New title"),
  field(...),
  field(...)
))
```


### From SharePoint docs:

`You can create and update SharePoint entities by constructing RESTful HTTP requests to the appropriate endpoints, just as you do when you’re reading data. One key difference, however, is that you use a POST request. When you’re updating entities, you also pass a PUT or MERGE HTTP request method by adding one of those terms to the headers of your request as the value of the X-HTTP-Method key. The MERGE method updates only the properties of the entity that you specify, while the PUT method replaces the existing entity with a new one that you supply in the body of the POST. Use the DELETE method to delete the entity. When you create or update an entity, you must provide an OData representation of the entity that you want to create or change in the body of your HTTP request.
Another important consideration when creating, updating, and deleting SharePoint entities is that if you aren’t using OAuth to authorize your requests, these operations require the server’s request form digest value as the value of the X-RequestDigest header. You can retrieve this value by making a POST request with an empty body to http://<site url>/_api/contextinfo and extracting the value of the d:FormDigestValue node in the XML that the contextinfo endpoint returns. The following example shows an HTTP request to the contextinfo endpoint in C#.`


### SharePoint docs sample code:
```js
jQuery.ajax({
        url: "http://<site url>/_api/web/lists",
        type: "POST",
        data:  JSON.stringify({ '__metadata': { 'type': 'SP.List' }, 'AllowContentTypes': true,
 'BaseTemplate': 100, 'ContentTypesEnabled': true, 'Description': 'My list description', 'Title': 'Test' }
),
        headers: {
            "accept": "application/json;odata=verbose",
            "content-type": "application/json;odata=verbose",
            "content-length": <length of post body>,
            "X-RequestDigest": $("#__REQUESTDIGEST").val()
        },
        success: doSuccess,
        error: doError
});
```



Development
-----------

Clone the repo, run `npm install`.

Run tests using `npm run test` or `npm run test:watch`

Build the project using `make`.
