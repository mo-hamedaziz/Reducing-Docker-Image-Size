1. Initial docker file
```
FROM node:latest
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
RUN npm run build
EXPOSE 3000
CMD ["npm", "run", "start"]
```

![alt text](image.png)
The current image size is 1.86GB

2. Changing to a smaller base image
```
FROM node:alpine
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
RUN npm run build
EXPOSE 3000
CMD ["npm", "run", "start"]

```
![alt text](image.png)
The current image size is 903MB (from 1.86GB previously)

Read more about slim vs alpine ()


2. Using a multi-stage Dockerfile
```
FROM node:alpine AS build
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
RUN npm run build

FROM node:alpine AS production
WORKDIR /app
COPY --from=build /app/build /app/build
RUN npm install -g serve
EXPOSE 3000
CMD ["serve", "-s", "build", "-l", "3000"]

```
![alt text](image.png)
The current image size is MB (from 903MB previously)