# syntax=docker/dockerfile:1.4
FROM node:lts As development 

WORKDIR ./code 

ENV CI=true
ENV PORT=3000

COPY package.json package-lock.json ./
COPY .npmrc .yarnrc.yml ./

RUN npm ci

COPY . .

CMD ["npm","start"]

FROM development AS builder 

RUN npm run build 

FROM dvelopment AS dev-env 

RUN apt-get update && \
    apt-get install -y --no-install-recommends git

RUN groupadd docker && \
    useradd -s /bin/bash -m -G docker vscode

COPY --from=gloursdocker/docker / /

FROM nginx:1.13-alpine 
COPY --from=builder /code/build /usr/show/nginx/html