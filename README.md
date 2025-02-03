# my-python-app
Flask app deployed using AWS ECR & EC2

## Install the required MySQL package, Run the Application Locally, and Build Containers
```sh
# Install MySQL package
sudo apt-get update -y
sudo apt-get install mysql-client -y

# Running application locally
pip3 install -r requirements.txt
sudo python3 app.py

# Building MySQL Docker image
docker build -t my_db -f Dockerfile_mysql .

# Building application Docker image
docker build -t my_app -f Dockerfile .

# Running MySQL container
docker run -d -e MYSQL_ROOT_PASSWORD=pw my_db

# Get the IP of the database and export it as DBHOST variable
docker inspect <container_id>

# Example when running DB as a Docker container and app is running locally
export DBHOST=127.0.0.1
export DBPORT=3307

# Example when running DB as a Docker container and app is running locally
export DBHOST=172.17.0.2
export DBPORT=3306

# Set Application Variables
export APP_COLOR=blue
export DATABASE=employees

# Run the application, make sure it is visible in the browser
docker run -p 8080:8080 -e DBHOST=$DBHOST -e DBPORT=$DBPORT -e DBUSER=$DBUSER -e DBPWD=$DBPWD my_app

