# web-application

This is a repo for hosting my travel website with Docker Container in AWS EC-2.

# Building using Docker
Build and run:
```
docker build -t web-application . 
docker run -d -p 5173:3000 --name web-application web-application
```
Open `http://localhost:5173` in your browser.
