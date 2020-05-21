## Commands

```diff
# to start the nginx server
- nginx

# Command syntac
- nginx -s [COMMAND]

# COMMANDS

+ quit – Shut down gracefully
+ reload – Reload the configuration file
+ reopen – Reopen log files
+ stop – Shut down immediately (fast shutdown)

```

### simple static server with proxy
```
http {
    # server 1
    server {
          listen 8080;
          root /Users/jigneshmodi/Desktop/projects/Aanushthan;

          location /images {
            root /Users/jigneshmodi/Desktop/projects/images;
          }
          
          // to stop from using .jpg images and return 403
          location ~ .jpg$ {
            return 403;
          }
    }
    
    # server 2
      server {
          listen 3000;
          root /Users/jigneshmodi/Desktop/projects/Aanushthan;
          
          //proxy path
          location / {
            proxy_pass http://localhost:8080;
          }
          
           location /img {
            proxy_pass http://localhost:8080/images;
          }
    }
    

}

events { }
```


### Layer 7(Http) loadbalancing example
-- will have max of 10 tcp connections 2 b/w browser and nginx, and reset from nginx to localservers
```
  http {
    
    upstream app1backend {
      # ip_hash; \\can stick to just the first ip address 
      server 127.0.0.0.1:2222;
      server 127.0.0.0.1:3333;
      server 127.0.0.0.1:4444;
      server 127.0.0.0.1:5555;
    }
    
    upstream app2backend {
      # ip_hash; \\can stick to just the first ip address 
      server 127.0.0.0.1:2222;
      server 127.0.0.0.1:3333;
      server 127.0.0.0.1:4444;
      server 127.0.0.0.1:5555;
    }
    
    server {
      listen 80;
      
      # load-balancing for app1
      location /app1 {
        proxy_pass http://app1backend/; 
      }
      
      # load-balancing for app2
       location /app2 {
        proxy_pass http://app2backend/; 
      }
      
    }
    
    server {
      listen 8080;
    }
    
  }
  
  events {}
```

### Layer 4(tcp) loadbalancing example
-- saves the number of tcp connections by mapping (techincally just 1 tcp connection)
```
 stream {
    
    upstream backend {
      # ip_hash; \\can stick to just the first ip address 
      server 127.0.0.0.1:2222;
      server 127.0.0.0.1:3333;
      server 127.0.0.0.1:4444;
      server 127.0.0.0.1:5555;
    }
    
    server {
      listen 80;
      
      # tcp proxy
      proxy_pass backend;
          
    }
    
  }
  
  events {}
  
```


### Hosting, https example
steps:
1. brew install letsencrypt
2. sudo certbot certonly --standalone
3. copy path to the generated certificates
4. copy the below config and sudo nginx

```
 http {
    
    server {
      # http port
      listen 80;
     
      # https port 
      listen 443 ssl http2;
      
      # public key
      ssl_certificate /path/to/public/certificate/fullchain.pem
      
      # private key
      ssl_certificate /path/to/private/certificate/privkey.pem
      
      # to work only for tls 1.3
      ssl_protocols TLSv1.3;
      
      root /path/to/project/
      
    }
    
  }
  
  events {}


```







### Sample config
```bash
#user  nobody;
worker_processes  1;

#error_log  logs/error.log;
#error_log  logs/error.log  notice;
#error_log  logs/error.log  info;

#pid        logs/nginx.pid;


events {
    worker_connections  1024;
}


http {
    include       mime.types;
    default_type  application/octet-stream;

    #log_format  main  '$remote_addr - $remote_user [$time_local] "$request" '
    #                  '$status $body_bytes_sent "$http_referer" '
    #                  '"$http_user_agent" "$http_x_forwarded_for"';

    #access_log  logs/access.log  main;

    sendfile        on;
    #tcp_nopush     on;

    #keepalive_timeout  0;
    keepalive_timeout  65;

    #gzip  on;

    server {
        listen       8080;
        server_name  localhost;

        #charset koi8-r;

        #access_log  logs/host.access.log  main;

        location / {
            root   html;
            index  index.html index.htm;
        }

        #error_page  404              /404.html;

        # redirect server error pages to the static page /50x.html
        #
        error_page   500 502 503 504  /50x.html;
        location = /50x.html {
            root   html;
        }

        # proxy the PHP scripts to Apache listening on 127.0.0.1:80
        #
        #location ~ \.php$ {
        #    proxy_pass   http://127.0.0.1;
        #}

        # pass the PHP scripts to FastCGI server listening on 127.0.0.1:9000
        #
        #location ~ \.php$ {
        #    root           html;
        #    fastcgi_pass   127.0.0.1:9000;
        #    fastcgi_index  index.php;
        #    fastcgi_param  SCRIPT_FILENAME  /scripts$fastcgi_script_name;
        #    include        fastcgi_params;
        #}

        # deny access to .htaccess files, if Apache's document root
        # concurs with nginx's one
        #
        #location ~ /\.ht {
        #    deny  all;
        #}
    }


    # another virtual host using mix of IP-, name-, and port-based configuration
    #
    #server {
    #    listen       8000;
    #    listen       somename:8080;
    #    server_name  somename  alias  another.alias;

    #    location / {
    #        root   html;
    #        index  index.html index.htm;
    #    }
    #}


    # HTTPS server
    #
    #server {
    #    listen       443 ssl;
    #    server_name  localhost;

    #    ssl_certificate      cert.pem;
    #    ssl_certificate_key  cert.key;

    #    ssl_session_cache    shared:SSL:1m;
    #    ssl_session_timeout  5m;

    #    ssl_ciphers  HIGH:!aNULL:!MD5;
    #    ssl_prefer_server_ciphers  on;

    #    location / {
    #        root   html;
    #        index  index.html index.htm;
    #    }
    #}
    include servers/*;
}
```

### Static file server


