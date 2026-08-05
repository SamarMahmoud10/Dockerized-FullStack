# syntax=docker/dockerfile:1.4 
FROM node:lts AS development 

ARG NODE_ENV=production 
ENV NODE_ENV=$NODE_ENV

WORKDIR /code 

ARG PORT=80
ENV PORT=$PORT
EXPOSE $PORT 

COPY package.json package-lock.json ./
COPY .npmrc .yarnrc.yml ./

RUN npm ci 

COPY . .
HEALTHCHECK --interval=30s \
    CMD node healthcheck.js 

CMD ["npm","start"]

FROM development as dev-env 

RUN apt-get update && \
    apt-get install -y --no-install-recommends git

RUN groupadd docker && \
    useradd -s /bin/bash -m -G docker vscode

COPY --from=gloursdocker/docker / /
