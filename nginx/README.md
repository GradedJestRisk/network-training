# Nginx-training

## Setup
Install ruby

Check install
``` shell
erb --version
```

## Start debug mode

Add debug directive in`nginx.conf.erb`
```
error_log /var/log/nginx/error.log debug;
```

Start nginx
``` shell
erb nginx.conf.erb > nginx.conf
docker run -v $(pwd)/nginx.conf:/etc/nginx/conf.d/default.conf:ro -p 80:80 --entrypoint nginx-debug nginx '-g daemon off;'
```

Make a call
``` shell
curl localhost:80
```

You'll get
```html
<html>
<head><title>502 Bad Gateway</title></head>
<body>
<center><h1>502 Bad Gateway</h1></center>
<hr><center>nginx/1.23.3</center>
</body>
</html>
```


## Proxy
https://nginx.org/en/docs/beginners_guide.html
> One of the frequent uses of nginx is setting it up as a proxy server, which means a server that receives requests, passes them to the proxied 
> servers, retrieves responses from them, and sends them to the clients.

It listens on the port 80.

It currently maps requests: 
- with the `/images/` prefix; 
- to the files under the /data/images directory.

Check
- terminal: `curl localhost:80/images/foo.jpg`
- browser: http://localhost/images/foo.jpg
