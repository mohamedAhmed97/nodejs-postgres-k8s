# Node.js and PostgreSQL Project

This project is a simple Node.js web application that uses PostgreSQL as a database. The project can be run locally using Docker Compose or deployed to a Kubernetes cluster.

## Prerequisites

To run this project, you will need to have the following tools installed on your machine:

- Docker
- Docker Compose (for local development)
- Kubernetes (for deployment)

## Local Development
****
To run the project locally using Docker Compose, follow these steps:

1. Clone the repository to your local machine:

   ````
   git clone https://github.com/your-username/nodejs-postgres-k8s.git
   ````

2. Change into the project directory:

   ````
   cd nodejs-postgres-k8s
   ````
3. Start the project using Docker Compose:
   - Connect to your PostgreSQL database and run the following SQL command to create the posts table:
      ````
         \c postgres_db ;
      ````
      ````
         CREATE TABLE posts (
            id SERIAL PRIMARY KEY,
            title TEXT NOT NULL,
            body TEXT NOT NULL,
            created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
         );
      ````
   
4. Inserting Data Into the Database Table
    ````
    INSERT INTO posts (title, body) VALUES ('Post #1', 'This is the first post');
   INSERT INTO posts (title, body) VALUES ('Post #2', 'This is the second post');
   INSERT INTO posts (title, body) VALUES ('Post #3', 'This is the third post');
   ````
   

5. Start the project using Docker Compose:

   ````
   docker-compose up
   ````

6. Access the web application in your browser at `http://localhost:3000`.

## Deployment to Kubernetes

To deploy the project to a Kubernetes cluster, follow these steps:

1. Create a Kubernetes cluster or use an existing one.

2. Set up a PostgreSQL database in the cluster. You can use a managed database service like Amazon RDS or Google Cloud SQL, or you can deploy PostgreSQL as a container in the cluster.

3. Build the Docker image for the Node.js web application:

   ````
   docker build -t {{your-username}}/nodejs-postgres .
   ````
4. Change the name of image in /k8s/app/app.yaml
   ````
      spec:
      containers:
      - name: nodejs-app
        image: {{your-username}}/nodejs-postgres
   ````
5. Push the Docker image to a container registry that is accessible to your Kubernetes cluster.
   ````
      docker push {{your-username}}/nodejs-postgres
   ````

6. Deploy the Kubernetes manifest files of database:
   ````
   kubectl apply -f k8s/db/db-config.yaml
   kubectl apply -f k8s/db/db-secrets.yaml
   kubectl apply -f k8s/db/database.yaml
   ````
7. Deploy the Kubernetes manifest files of node app:
   ````
   kubectl apply -f k8s/app/app-config.yaml
   kubectl apply -f k8s/app/app-secrets.yaml
   kubectl apply -f k8s/db/app.yaml
   ````

8. Access the web application in your browser at the URL of the Kubernetes service that is exposed by the deployment.

## Conclusion

This project demonstrates how to build and deploy a Node.js web application with a PostgreSQL database using Docker Compose and Kubernetes. Use this project as a starting point for your own projects, and feel free to modify the code and configuration to suit your needs.