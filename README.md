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


