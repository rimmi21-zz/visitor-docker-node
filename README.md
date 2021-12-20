# visitor-docker-node

In this mini project, we create a node app, that counts the number of times, one would visit the site.

At first, we create a `package.json` file and include the very 2 packages we would be using. The express and the redis servers.

Then, we create the `index.js` file and require the 2 servers (redis & express). We write some code to count the number of visitors for the site, and make our port `8081` listen to the server.

Once, we do this, we create a new `Dockerfile` and create the node image. But, we are using the redis server too! So, how do we run it?

We open a new terminal, and run the below command:

`docker run redis`

Docker downloads redis and keeps running it on the terminal. We create another terminal, and keep the redis server initiated. In this new terminal, we build our docker file, using the command:

`docker build .`

And then, we tag it with our **username/app-name:latest**.

`docker build -t sohinipattanayak/visitor-app:latest .`

Now, we are not done yet. We need to create a communication between the two containers, the redis server container and the node server container. To do that, we'll use **docker compose**

We'll create a **docker-compose.yml** file where we do the following:

- Include the containers that we want (redis-server and node-server)
- create `redis-server` (create using the redis-image)
- create `node-server` (create using the dockerfile in the current repository)
- MAP port 8081 to 8081

You can look at the **docker-compose.yml** for more details.

Now, we run a couple of docker-compose commands:

- `docker-compose up`

Now let's say, you are making changes to the index.js file and you want them to be updated, to reflect on the site, you can try this command below, as it's a combination of the `docker build .`
and `docker run` command.

- `docker-compose up --build`

Finally, this is how the server should look like:

![](https://github.com/rimmi21/visitor-docker-node/blob/main/visitor-app.png)

With the help of **docker-compose** we can have multiple containers running at the same time. Let's say we'd like to launch **docker-compose** in the background. We should use the following command:

`docker-compose up -d`

Now, if we'd like to stop all the running containers, individually extracting their id's and then stopping them would be a pain!

So, we can stop all of them together at a time, using the below command:

`docker-compose down`

To check the status of running containers inside our docker-compose.yml file, we must type the below command inside the directory our docker-compose.yml file is located in.

`docker-compose ps`
