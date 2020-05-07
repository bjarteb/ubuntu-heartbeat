# ubuntu-heartbeat

An example setup to demonstrate heartbeat in a Vagrant environment.

## Introduction

Install nginx to serve site 'example.com'
Next, install haproxy and heartbeat in an HA setup.

## High Availability Testing

```bash
curl -H 'Host: www.example.com' http://10.0.10.10:8080

# output
<html>
    <head>
        <title>Welcome to example.com!</title>
    </head>
    <body>
        <h1>Success!  The example.com is served by lb1</h1>
    </body>
</html>
```
