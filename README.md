# web-application

This is a repo for hosting my travel website with Docker Container in AWS EC-2.

# Building using Docker
Build and run:
```
docker build -t web-application . 
docker run -d -p 5173:3000 --name web-application web-application
```
Open `http://localhost:5173` in your browser.

# Building using Docker on AWS EC2 
1. Create and launch AWS EC2 Linux instance using your AWS account.
2. Connect to the instance using EC2 Instance Connect
3. In EC2 Instance Connect terminal window type the following commands:
    1. Update the packages and download Docker
    ```
    sudo yum update -y
    ```
    2. Download Docker on EC2 Linux instance
    ```
    sudo amazon-linux-extras install docker
    ```     
    3. Start Docker service
    ```
    sudo service docker start
    ```     
    4. Modify user permissions to EC2 instance users to grant them access when they want to perform Docker commands
    ```
    sudo usermod -a -G docker {ec2-user-account}
    ```  
    5. Make a project directory
    ```
    mkdir {project-directory}
    ```
    6. Change the current directory to the project directory
    ```
    cd {project-directory}
    ```
4. On your local machine (Mac-OS) go to the project directory and make sure .pem (EC2 instance permission file) is copied:
    1. Modify the permissions of .pem so that we can use it for authenticating to the EC2 instance
    ```
    chmod 600 {your-pem-file-name.pem}
    ```    
    2. Upload project to the EC2 instance
    ```
    scp -r -i {your-pem-file-name.pem} src/ {ec2-user-account}@{ec2-public-ip}:{project-directory-on-ec2}
    ```
5. In EC2 Instance Connect terminal window build and run Docker
   ```
    docker build -t web-application . 
    docker run -d -p 5173:3000 --name web-application web-application
   ```
6. Open `http://{ec2-public-ip}:5173` in your browser.
7. Once you are finished working on Docker container and EC2 instance, perform the clean-up:
    1. Stop Docker container
    2. Terminate EC2 instance
            
