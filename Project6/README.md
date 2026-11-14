## 1. Create a Docker container image

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

## 2. GitHub Actions and DockerHub
- Configuring Github Repo Secrets
    - How to create a PAT for authentication
        - 1. Go to dockerhub
        - 2. Open `Sccount Settings`
        - 3. Go to `Personal Access Token`
        - 4. Click `Create New Token`
        - 5. Set name and set as `Read & Write`
        - 6. Copy the token and put it somewhere safe. 
    - How to set repository Secrets for use by GitHub Actions
        - 1. On your repository go to Settings 
        - 2. Click on `Secrets and Variables `> Actions
        - 3. Click `New Repository Secret`
        - 4. Add the Secret Name and value 
        - 5. Do this for both USERNAME and TOKEN
    - Describe the Secrets set for this project
        - In this case, Secret = `DOCKER_USERNAME`, Value = `apatel1406` and Secret = `DOCKER_TOKEN`, Value = `Dockerhub Generated Token` 
---
- CI with Github Actions
    - I created a Github actions workflow file called [Docker-build.yml](../.github/workflows/docker-build.yml) This code runs everytime something is pushed to the main brunch
    - Workflow Steps
        - Checkout: Uses `actions/checkout@v6` to access the repo files
        - Login To Docker Hub: Uses `docker/login-action@v4` and the repo secrets added earlier as the username and password to authenticate with Dockerhub
        - Build and Push: Uses `docker/build-push-action@v7` to build the docker image from the Project6 folder and pushes it to dockerhub with the latest tag
    - Values that may need to the updated if used in a different repo
        - `Branch` may need to updated if pushed to another branch besides main.
        - `Context` needs to be changed to a different repo folder
        - `Tags` need to be changed to match the dockerhub username and repo name if changed
    - Link to Workflow File 
        - [Docker-build.yml](../.github/workflows/docker-build.yml)
    - Permalink 
        - https://github.com/WSU-kduncan/ceg3120-cicd-patel1599-f26/blob/4f7f32345b369c1af2a53f13c2b5702d10346ff8/.github/workflows/docker-build.yml
---
- Testing and Validation
    - Test the workflow by pushing changes to the main branch and in the github actions tag we should see a new workflow with the green checkmark. 
    - Also checked that it didn't work using a test-branch. 
    - To verify the docker image, i pulled the image from dockerhub and ran it as a conatiner. One thing to remember is that port 8080 is already taken up with the original image, and if we want to really test then we would run using 8081:80
    - [Docker Repo](https://hub.docker.com/r/apatel1406/aws-lb)
---
- Links Used
    - ![Sample-Workflow](https://github.com/pattonsgirl/CEG3120/blob/main/Projects/Project6/sample-workflows/docker-workflow-v2.yml)
    - ![Building and Pushing Docker Images](https://github.com/marketplace/actions/build-and-push-docker-images)
    - ![Publishing Docker Images](https://docs.github.com/en/actions/tutorials/publish-packages/publish-docker-images#publishing-images-to-docker-hub)
    - ![Publishing and Exposing Ports](https://docs.docker.com/get-started/docker-concepts/running-containers/publishing-ports)
