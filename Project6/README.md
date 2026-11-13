## 2. Building A Web Service Container

- Website built by ChatGPT, `Build a complete themed website with an index page, a second page and a css page`
- Website on space exploration and the solar system, includes information on space exploration and solar system.
- [index.html](web-content/index.html) - Main home page
- [about.html](web-content/about.html) - Contains the information about the planets
- [style.css](web-content/style.css) - Stylesheet used for both pages.

---

- [Dockerfile](Dockerfile) uses the httpd:2.4 server and copies all the contents of the website into the default web directory for apache
- Instructions to build and push the container image to your DockerHub repository
    1. On your Docker account go to account setting.
    2. Go to Personal Access Token and Generate New Token.
    3. Make it so it is set to read and write so you can make changes later. Make sure this key isn't shared.
    4. On terminal go to the active working directory where the code is stored.
    5. On terminal run `docker build -t apatel1406/aws-lb:latest .`
    6. Go to hub.docker.com and click create new repository.
    7. The image should show up, if not run `docker build -t apatel1406/aws-lb:latest .` again, then it should.
    8. Run the container, 
       `docker run -d --name project6-web -p 8080:80 apatel1406/aws-lb:latest`
    9. Open a browser and go to `http://localhost:8080` to view the website.

- [Docker Repository](https://hub.docker.com/repository/docker/apatel1406/aws-lb/general)

- Links Used
    1. [Docker Image & Container Help](https://docs.docker.com/build/concepts/dockerfile)
    2. [Building, Tagging and publishing a dockerfile image](https://docs.docker.com/get-started/docker-concepts/building-images/build-tag-and-publish-an-image/)