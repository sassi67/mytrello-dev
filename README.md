# mytrello-dev
Node container with Bootstrap, Typescript, JQuery used as development platform.

The construction of this container requires two steps:

## Step. 1 construction of the Node application
 - clone this repository
 - enter the cloned directory
 - docker build -t mytrello-pre -f Dockerfile.pre .  
 - docker run --rm -it -p 8099:3000 -v ${PWD}:/mytrello mytrello-pre
At this time you are in the container. Type:
 - nmp init -y
 - npm i typescript@3.5.3
 - npm i jquery@3.6.0
 - npm i bootstrap@5.2.0
 - npm i express@4.18.1
 - npm i nodemon@2.0.11
 - exit
Remove the mytrello-pre image
 - docker rmi mytrello-pre

You should see a new directory node-modules and two files: package-lock.json and package.json.
These will be used to create a new Node container in which the dependencies to our application will be found in them. 

## Step. 2 construction of the final Node container
Change the package.json in this way:
"scripts": {
    // other stuffs
    "start": "nodemon L --inspect=0.0.0.0 server.js"
},
 - docker build -t mytrello-dev -f Dockerfile.dev . 
 - docker run -d -p 8099:3000 -v ${PWD}:/mytrello mytrello-dev

## To use the existing container without building it
An existing image has been published into the Docker Hub. To download it:
 - docker pull sassi67/mytrello-dev:1.0

## To run the pulled container
 - docker run -d -p 8099:3000 -v ${PWD}:/mytrello sassi67/mytrello-dev:1.0

## (Optional) Publish the repository
 - docker build -t sassi67/mytrello-dev:1.0 -f Dockerfile.dev .
 - docker push sassi67/mytrello-dev:1.0