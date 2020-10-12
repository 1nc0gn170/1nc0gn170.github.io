# Bugpoc LFI Challenge
------
<center><img src="/posts/CTF-Writeups/Images/bugpoc-1.png"></center>

We are given a website  **Social Media Sharer** , which will create a set of sharing options for a given website.Our aim to read `/etc/passwd` from their system. 

<center><img src="/posts/CTF-Writeups/Images/bugpoc-2.png"></center>

So the functionality of this website is simple.It creates content from the given URL based on facebook open graph meta tags ("og:").

So I quickly framed a html file with meta tags 

```html
<!DOCTYPE html>
<html>
<head>
	<title>Testing</title>
		<meta property="og:type" content="website">
		<meta property="og:url" content="http://0.0.0.0/" />
		<meta property="og:title" content="Testing" />
		<meta property="og:description" content="Testing" />
		<meta property="og:image" content="XXXXXX/test.png">


</head>
<body>
</body>
</html>
```

## Observation 1

- Server first visits the given website and extracts meta tags content.
- Then server first makes **HEAD** request to the og:image url.
- If `HEAD` request fails server won't fetch image.
- Otherwise a **GET** request will be made to fetch the image

## Observation 2

As the server fetches the image based on the url provided in `og:image` meta tag.\
So I directly tried to access file `file:///etc/passwd` but that didn't work.Then I changed it to `<meta property="og:image" content="http://127.0.0.1/">`
```
Image Preview Error: HTTPConnectionPool(host='127.0.0.1', port=80): Max retries exceeded with url: / 
(Caused by NewConnectionError('<urllib3.connection.HTTPConnection object at 0x7f91d451f850>: Failed to establish a new connection: 
[Errno 111] Connection refused'))

```
So seems like server is using urllib3 to visit and fetch the website.

### RabbitHole
As the server is using urllib, I tried Orange Tsai, breaking urllib parser techniques.Nothing worked :(



## Observation 3

After many trails,I came to know that the server will only accept 
- png
- jpg
- gif
- svg

Any file other than this will fail the `HEAD` request.Smells like server is checking `Content-Type` header.
So any file with content-type starting with `image` (`Content-Type image/..`) will bypass the head test.

## Observation 4

Here comes the redirection part.As the `HEAD` request is only checking `Content-Type` header,add any other header makes no difference.
So I thought of adding `Location` header ie. (`Location: file:///etc/passwd`).So when server makes a `GET` request it will be redirected to the specified file
and fetches the content for us.

## Attack Scenario
- I used svg file (with header `Content-Type: image/svg+xml`)to fool HEAD request
- Then I added a Location header to which will redirect the server to fetch it's own file.(`Location: file:///etc/passwd`)
- Finally server fetches the file content :)
 

EXPLOIT
--------
### HTML with meta content
<script src="https://gist.github.com/n41n4/4bf777633e41dc4c80605add59d66030.js?file=main.html"></script>\
### Python Server
<script src="https://gist.github.com/n41n4/4bf777633e41dc4c80605add59d66030.js?file=server.py"></script>\


<script src="https://gist.github.com/n41n4/4bf777633e41dc4c80605add59d66030.js?file=env.json"></script>\
<script src="https://gist.github.com/n41n4/4bf777633e41dc4c80605add59d66030.js?file=app.py"></script>\



