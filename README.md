# cloudflare-docker-proxy

![deploy](https://github.com/lileixuan/cloudflare-docker-proxy/actions/workflows/deploy.yaml/badge.svg)

[![Deploy to Cloudflare Workers](https://deploy.workers.cloudflare.com/button)](https://deploy.workers.cloudflare.com/?url=https://github.com/lileixuan/cloudflare-docker-proxy)

> If you're looking for proxy for helm, maybe you can try [cloudflare-helm-proxy](https://github.com/lileixuan/cloudflare-helm-proxy).

## Deploy

1. click the "Deploy With Workers" button
2. follow the instructions to fork and deploy
3. update routes as you requirement

[![Deploy to Cloudflare Workers](https://deploy.workers.cloudflare.com/button)](https://deploy.workers.cloudflare.com/?url=https://github.com/lileixuan/cloudflare-docker-proxy)

## Routes configuration tutorial

1. use cloudflare worker host: only support proxy one registry
   ```javascript
   const routes = {
     "${workername}.${username}.workers.dev/": "https://registry-1.docker.io",
   };
   ```
2. use custom domain: support proxy multiple registries route by host
   - host your domain DNS on cloudflare
   - add `A` record of xxx.example.com to `192.0.2.1`
   - deploy this project to cloudflare workers
   - add `xxx.example.com/*` to HTTP routes of workers, such as `docker`/`quay`/`gcr`/`k8s`/`k8s-gcr`/`ghcr`/`cloudsmith`/`ecr`
   - add more records and modify the project Settings, add your domain to CUSTOM_DOMAIN secret
   - or modify the config as you need by hand 
   ```javascript
   const routes = {
     "docker.xxx.so": "https://registry-1.docker.io",
     "quay.xxx.so": "https://quay.io",
     "gcr.xxx.so": "https://gcr.io",
     "k8s.xxx.so": "https://registry.k8s.io",
     "k8s-gcr.xxx.so": "https://k8s.gcr.io",
     "ghcr.xxx.so": "https://ghcr.io",
     "cloudsmith.xxx.so": "https://docker.cloudsmith.io",
     "ecr.xxx.so": "https://public.ecr.aws",
   };
   ```

