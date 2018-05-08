# e621-API-Docs

## About

**PLEASE NOTE**: This is still in development/in-depth research phase

This is a repository for a better set of documentation for the site [e621](https://e621.net). If you're here, you know what this site is for.
</br>

The official documentation is available [here](https://e621.net), but it does not go very in depth on GET/POST endpoints and how they differ. Also some information is incorrect. This documentation is derived from the official API documentation but presented in a different and more in-depth manor.

Any general information will be available on this page. if you want to get more information on any specific endpoint, look in the `docs/` folder of this repo.
</br>
</br>


## The Basics

The e621 API uses the two main HTTP REST methods, **GET** and **POST**. This is how you interact with the API, through REST URL endpoints. Any time you are retrieving data from the API you are using GET, any time your are giving the API information you are using POST.
</br>

e621 treats REST URLs as functions, so when you are GETting data, you pass your desired options after the base URL (separated by a `?`)

A basic example looks like this:
```url
https://e621.net/post/index.json?limit=10
```
[Try it in your browser](https://e621.net/post/index.json?limit=10)
</br>

### Breaking down the URL

If you've dealt with REST APIs before this should seem familiar, if not here's a breakdown: The base URL will always be `https://e621.net/`, the next part of the URL `post` indicates the base endpoint we want to access. Changing this to something like `artist` would make all `artist` endpoints available to us. 

The next part of the URL `index` is considered the 'action'. In this case the `index` action retrieves an index of posts. 

After that, the `.json` part of the URL tells e621 that we want a JSON message returned, as opposed to XML. **Both JSON and XML are available but some endpoints are only available in one or the other**. 

Lastly are your `parameters`. These change depending on the 'action' you are performing but the allow you to specify the type of data you are receiving from the API. In this case `limit=10` is our parameter. This limits the response from e621 to 10 posts being returned. 

**Note**: Parameters for GET requests must **always** use a `?` to separate the URL from the parameters. Also, any additional parameters beyond the first must be separated with an `&`.
</br>

### JSONP Support

The API does support JSONP. To use JSONP, append `&callback=mycallbackfunction` to your request. The resulting JSON will be encapsulated into a call to `mycallbackfunction`. 

#### Example

`/blip/index.json?callback=mycallbackfunction`

would return a response like:
```javascript
mycallbackfunction([{"user":"A User","response":null,"body":"Blip one","user_id":1,"id":1}])
```
</br>

### Using cURL

If you are using cURL or something similar, you may experience failurs on your HTTP requests. The API declares this to be a problem with SSL. If this is the case, you will need to point cURL to a trusted certificate to compare the remote site's (e621.net) certificate with. You can get the certificate [here](http://curl.haxx.se/ca/cacert.pem). After you have the cert downloaded, you can point cURL to it like so:

```bash
curl_setopt($ch, CURLOPT_CAINFO, "/server_dir/apache/cacert.pem");
```

Alternatively you can disable SSL alltogether (not advised)

</br>

## User-Agent Requirements

Making any requests to the e621 API **requires** a user-agent string. Making this something helpful like your username + project can help e621 get in touch with you if issues arise.

**NOTE**: Impersonating a browser user-agent will quickly have your IP address blocked from API access by e621.
