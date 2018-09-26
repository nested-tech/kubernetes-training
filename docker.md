## Starting with Docker

First we will build and run a docker image.

Inside the `application` folder run the below steps:
1. `npm run image:build`
2. `npm run image:run`
3. In a browser open http://localhost:3000

Once you have verified it has worked you can stop the image with
1. `docker ps`
2. `docker stop <our container id>`
