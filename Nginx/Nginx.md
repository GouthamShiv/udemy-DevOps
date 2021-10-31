# Installing and configuring `NGINX`
---


### Installing `NGINX`
> sudo apt install nginx

---
---

### `NGINX` config for jenkins
```config
    upstream jenkins {
    keepalive 4; # keepalive connections
    server 127.0.0.1:8080; # jenkins ip and port
    }

    server {
        
        listen 80;
        root /var/run/jenkins/war;

        server_name <<host-name>>

        location ~ "^/static/[0-9a-fA-F]{8}\/(.*)$" {
            # rewrite all static files into requests to the root
            # E.g /static/12345678/css/something.css will become /css/something.css
            rewrite "^/static/[0-9a-fA-F]{8}\/(.*)" /$1 last;
        }

        location /userContent {
            # have nginx handle all the static requests to userContent folder
            # note : This is the $JENKINS_HOME dir
            root /var/lib/jenkins/;
            if (!-f $request_filename){
                # this file does not exist, might be a directory or a /**view** url
                rewrite (.*) /$1 last;
                break;
            }
                sendfile on;
        }

        location / {
            sendfile off;
            proxy_pass         http://jenkins;
            proxy_redirect     default;
            proxy_http_version 1.1;

            proxy_set_header   Host              <<host-name>>;
            proxy_set_header   X-Real-IP         <<ip-address>>;
            #proxy_set_header   X-Forwarded-Port  <<port>>;
            proxy_set_header   X-Forwarded-Proto https;
            proxy_max_temp_file_size 0;

            #this is the maximum upload size
            client_max_body_size       10m;
            client_body_buffer_size    128k;

            proxy_connect_timeout      90;
            proxy_send_timeout         90;
            proxy_read_timeout         90;
            proxy_buffering            off;
            proxy_request_buffering    off; # Required for HTTP CLI commands
            proxy_set_header Connection ""; # Clear for keepalive
        }

    }
```

---
---