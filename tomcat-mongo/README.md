## viki19/tomcat-mongo
This image contains tomcat, mongoDB. It comes from [viki19/centos-jre-python](https://github.com/vignesh-kumar19/docker.git)

## Build
`docker build -t viki19/tomcat-mongo:<version> .`

## Run
`docker run -d -p 7080:8080 --name=tomcat-mongo viki19/tomcat-mongo:<version>`
