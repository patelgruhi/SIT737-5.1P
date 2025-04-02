Docker Compose for Web Application Dockerization

The instructions for Dockerizing a web application with Docker Compose and a Dockerfile are contained in this repository. It covers the steps of building a Docker image, deploying it as a container, and putting in place container health checks to guarantee the dependability of the application.

Steps
1. Install Docker
First, we need to install Docker. 

2. Clone the Sample Web Application
Clone the web application that we want to Dockerize. 

git clone https://github.com/your-username/your-app.git

3. Create a Dockerfile
A Dockerfile is required to build a Docker image for the application. 

FROM node:18

WORKDIR /app

COPY package.json ./
RUN npm install

COPY . .

EXPOSE 4000

CMD ["node", "app.js"]

4. Build the Docker Image

docker build -t my-web-app .

5. Create a Docker Compose File

version: '3.8'

services:
  web:
    image: image1:latest
    build: .
    ports:
      - "4000:4000"
    volumes:
      - .:/app
    environment:
      - NODE_ENV=production
    restart: always
    healthcheck:
      test: ["CMD", "curl", "-f", "http://localhost:4000"]
      interval: 30s
      timeout: 10s
      retries: 3
      start_period: 5s

6. Start the Docker Compose Environment
We need to start the application using Docker Compose:

docker-compose up

7. Test the Application
Once the container is running, we can test the application by visiting http://localhost:4000 in the browser.

8. Push the Docker Image to a Registry
If we want to push the image to a Docker registry (e.g., Docker Hub), using following commands:

docker tag my-web-app username/my-web-app:latest
docker push username/my-web-app:latest

