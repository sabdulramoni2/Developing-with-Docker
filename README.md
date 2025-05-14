## demo app - developing with Docker

This demo app shows a simple user profile app set up using 
- index.html with pure js and css styles
- nodejs backend with express module
- mongodb for data storage

All components are docker-based

### With Docker

#### To start the application

Step 1: Create docker network

    docker network create mongo-network 

![image](https://github.com/user-attachments/assets/8d4a1f41-914b-435c-ba6f-2015f2a3d512)


Step 2: start mongodb 

    docker run -d -p 27017:27017 -e MONGO_INITDB_ROOT_USERNAME=admin -e MONGO_INITDB_ROOT_PASSWORD=password --name mongodb --net mongo-network mongo
    

 ![image](https://github.com/user-attachments/assets/abe5747e-e092-4b69-8bca-63608fdcb1ce)


Step 3: start mongo-express
    
    docker run -d -p 8081:8081 -e ME_CONFIG_MONGODB_ADMINUSERNAME=admin -e ME_CONFIG_MONGODB_ADMINPASSWORD=password --net mongo-network --name mongo-express -e ME_CONFIG_MONGODB_SERVER=mongodb mongo-express   

![image](https://github.com/user-attachments/assets/32269b85-aad7-43d3-9245-ff41e75dc60a)


_NOTE: creating docker-network in optional. You can start both containers in a default network. In this case, just emit `--net` flag in `docker run` command_

Step 4: open mongo-express from browser

    http://localhost:8081

 ![image](https://github.com/user-attachments/assets/aa84d163-4189-445f-805d-178f0ff604c9)


Step 5: create `user-account` _db_ and `users` _collection_ in mongo-express


![image](https://github.com/user-attachments/assets/979bcbbc-8f19-4fb5-b60a-a5f42c75eb74)


Step 6: Start your nodejs application locally - go to `app` directory of project 

    cd app
    npm install 
    node server.js
    
Step 7: Access you nodejs application UI from browser

    http://localhost:3000

![image](https://github.com/user-attachments/assets/9207da44-0da9-4517-b722-52f147888bda)


![image](https://github.com/user-attachments/assets/1abb9c40-2bcf-4fd5-82bb-f8b5a6618d34)


### With Docker Compose

#### To start the application

Step 1: start mongodb and mongo-express

    docker-compose -f docker-compose.yaml up

![image](https://github.com/user-attachments/assets/51f73463-058f-48b8-929b-b1c76ab1004d)


![image](https://github.com/user-attachments/assets/aa1dac94-c25f-4810-8071-4570f50e28b5)


    
_You can access the mongo-express under localhost:8080 from your browser_
    
Step 2: in mongo-express UI - create a new database "user-account"

![image](https://github.com/user-attachments/assets/95254ab4-7d79-43d6-a119-2bdc6218869d)


Step 3: in mongo-express UI - create a new collection "users" in the database "user-account"       


![image](https://github.com/user-attachments/assets/561fb9b1-06f1-40ef-88bf-08114d62ecfd)


![image](https://github.com/user-attachments/assets/f1cbb5d7-ff33-4949-94f9-f663afaf06e1)


    
Step 4: start node server 

    cd app
    npm install
    node server.js
    
Step 5: access the nodejs application from browser 

    http://localhost:3000

#### To build a docker image from the application

    docker build -t my-app:1.0 .       


![image](https://github.com/user-attachments/assets/56f70227-47b3-4135-aa30-b0ae94ab87ff)


![image](https://github.com/user-attachments/assets/ea9cc0fe-2915-4c2e-9278-d5afd5981d07)


    
The dot "." at the end of the command denotes location of the Dockerfile.
