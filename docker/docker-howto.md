##
##
## https://www.r-bloggers.com/deploying-an-r-shiny-app-with-docker/
##
## https://www.bjoern-hartmann.de/post/learn-how-to-dockerize-a-shinyapp-in-7-steps/
##


## build docker
docker build -t shinyapp .

## build docker, force using no cache
docker build --no-cache -t shinyapp .

## Run on port 4000
docker run -p 4000:3838 shinyapp

## +run in background, remove contained after use, give nice name
docker run --rm -d -p 4000:3838 --name=app1 shinyapp

## map local data folder to docker data folder
docker run --rm -d -v /home/mydata:/omicsplayground/data -p 4000:3838 --name=app1 shinyapp

## To save your Docker Image as a tar-archive, you simply type into your terminal:
docker save -o ~/shinyapp.tar shinyapp

## To deploy your Docker Image
docker load -i shinyapp.tar
docker run shinyapp

## publish to Docker Hub
docker login
docker tag playground:v1 bigomics/playground:v1.0
docker tag playground:v1 bigomics/playground:latest

docker push bigomics/playground
