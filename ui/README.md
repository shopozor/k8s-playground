# Frontend setup

## Caddy server

In the `Caddyfile`, do not mention `localhost` if you want to enable https. Also, with the current setup, the TLS does not seem to be completely setup, there is a problem with the handshake. 

## Persistent volume

The idea is that we share a persistent volume between the frontend and a service that builds the frontend to an SPA or a static site. Only install the persistent volume claim, it will automatically create the persistent volume.