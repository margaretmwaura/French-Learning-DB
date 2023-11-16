# French-Learning-DB

This the containarized mysql db that is used in the french learning project.

## Getting started

### Requirements 
- Ensure you have docker installed on your local machine.

### Setting Up

1. Clone the project to your local host

2. Create a network to be used across the 3 containers if it does not exist already

``` docker network create french-network```

3. Build the image

``` docker build -t french-db -f Dockerfile . ```

4. Create a db container from the image and run it

``` docker run -it -p 3306:3306 -e MYSQL_ROOT_PASSWORD=<MYSQL_ROOT_PASSWORD> -e MYSQL_DATABASE=<DB_NAME> -e MYSQL_HOST=<MYSQL_HOST> --network=french-network --name=french-db french-db ```

- Please note the db_name, the mysql_root_password and the host will be required in the sequelize setup of the backend
- Setting up of the db container should be done before setting up of the backend container as the backend container depends on the db container

A db container should be successfully running and accessible from a db management app on port 3306

## Contribution

Bug reports and Pull Requests are welcomed.
