As you can see I’ve added a bw-stripPrefix middleware for Websocket. This middle ware will be added in dynamic.yml as below:

# Dynamic configuration
...
        stsSeconds: 31536000        
        
    bw-stripPrefix:
      stripPrefix:
        prefixes:
          - "/notifications/hub"
        forceSlash: false
        
    user-auth:
...

There are a lot of settings you can use on official wiki. In my set up, I’ve set WebSocket, Admin Page, Disable registration and Disable invitations. You can add/remove features to suit your needs. I want to mention Admin Page specially because a lot of setting like SMTP can be set on Admin page. You don’t have to usea config.json file or a lot of environment variables on your docker-compose.yml file.

Admin Page is relatively easy to set up. All you need is a ADMIN_TOKEN environment variable. On the official document, they provided command openssl rand -base64 48 to generate a 48 bit random token with OpenSSL.

I will update this post with a video later. If you have any questions, please feel free to contact me.

Thank you for reading, see you next time.
