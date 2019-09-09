---
layout: post
title: C# - Read uploaded file
image: img/testimg-cover.jpg
author: Pranay Aryal
date: 2019-08-10T10:00:00.000Z
tags:
  - C#
---

This is how you can read uploaded files in C#.

```c
[HttpPost, Route("api/upload")]
public async Task<IHttpActionResult> Upload()
{
    if (!Request.Content.IsMimeMultipartContent())
        throw new HttpResponseException(HttpStatusCode.UnsupportedMediaType); 
 
    var provider = new MultipartMemoryStreamProvider();
    await Request.Content.ReadAsMultipartAsync(provider);
    foreach (var file in provider.Contents)
    {
        var filename = file.Headers.ContentDisposition.FileName.Trim('\"');
        var buffer = await file.ReadAsByteArrayAsync();
        //Do whatever you want with filename and its binary data.
    }
 
    return Ok();
}
```

This is how you can save an uploaded file

```c
public Task<HttpResponseMessage> PostFile() 
{ 
    HttpRequestMessage request = this.Request; 
    if (!request.Content.IsMimeMultipartContent()) 
    { 
        throw new HttpResponseException(HttpStatusCode.UnsupportedMediaType); 
    } 
 
    string root = System.Web.HttpContext.Current.Server.MapPath("~/App_Data/uploads"); 
    var provider = new MultipartFormDataStreamProvider(root); 
 
    var task = request.Content.ReadAsMultipartAsync(provider). 
        ContinueWith<HttpResponseMessage>(o => 
    { 
 
        string file1 = provider.BodyPartFileNames.First().Value;
        // this is the file name on the server where the file was saved 
 
        return new HttpResponseMessage() 
        { 
            Content = new StringContent("File uploaded.") 
        }; 
    } 
    ); 
    return task; 
} 
```