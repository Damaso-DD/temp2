Context
do-nyc1-garden-guide

kubectl create secret tls garden-example-tls --key narsil.dev.key --cert narsil.dev.crt

garden --env=remote plugins kubernetes cluster-init

>Modify hosts file
> namespace: garden-guide

Garden must be run from a repo

## Digital Ocean Registry

https://docs.digitalocean.com/products/container-registry/how-to/use-registry-docker-kubernetes/

I need to create a container registry called `garden-guide`

registry.digitalocean.com/garden-guide

Click **Actions** button and then Download Docker Credentials (read and write permissions)

Create a secret

kubectl create secret generic do-registry \
  --from-file=.dockerconfigjson=docker-config.json \
  --type=kubernetes.io/dockerconfigjson



garden --env=remote plugins kubernetes cluster-init
garden --env=remote deploy

garden --env=remote call node-service/hello

# Testing local

garden --env=local plugins local-kubernetes cluster-init
garden --env=local deploy --watch

```
Deploy 🚀 

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
🌍  Running in namespace default in environment local
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

✔ providers                 → Getting status... → Cached
   ℹ Run with --force-refresh to force a refresh of provider statuses.
✔ graph                     → Resolving 2 modules... → Done
✔ go-service                → Building go-service:v-6b53a2650e... → Done (took 171 sec)
✔ node-service              → Building node-service:v-ecee711f57... → Done (took 108.6 sec)
✔ go-service                → Deploying version v-02add50d5a... → Done (took 3.4 sec)
   ℹ go-service                → Resources ready
   Ingress: http://remote-development.local.app.garden
✔ node-service              → Deploying version v-ed49483d6f... → Done (took 3 sec)
   ℹ node-service              → Resources ready
   Ingress: http://remote-development.local.app.garden/hello
   Ingress: http://remote-development.local.app.garden/call-go-service
```

garden --env=local call node-service/hello

```
Call 📞 

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
🌍  Running in namespace default in environment local
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

✔ providers                 → Getting status... → Cached
   ℹ Run with --force-refresh to force a refresh of provider statuses.
✔ graph                     → Resolving 2 modules... → Done
✔ Sending HTTP GET request to http://remote-development.local.app.garden/hello

200 OK

Hello from Node service!
(node:87966) Warning: Setting the NODE_TLS_REJECT_UNAUTHORIZED environment variable to '0' makes TLS connections and HTTPS requests insecure by disabling certificate verification.
(Use `garden --trace-warnings ...` to show where the warning was created)
```

garden delete environment
garden delete environment --env=remote

## other test

garden --env=remote plugins kubernetes cluster-init
garden --env=remote deploy

