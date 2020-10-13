This Jenkins pipeline/seed job is based on Tom Gregory's microservice devops series articles that 
discuss making a Spring Boot application pipelined to AWS ECS/Fargate. 

You can view the original article (and access the original repositorites) here:

https://tomgregory.com/building-a-spring-boot-application-in-jenkins/ 

This repo has an edit in the codebase so that
the docker container data is persisted in a folder /volume in the working directory. You will need 
to create the folder in the topmost directory. Do not delete the /volume folder as that is 
where the save state is loaded/saved in case the container is stopped. 

This Jenkins Docker container is configured to run Scala/Java. The docker container has a seed job that can be used to generate a main build job of the application 
you'd like to build. I'm actually using a similar setup for the CI/CD both at work and in my side projects. 

Make sure in createJobs.groovy you replace the github repo with the actual repo you are using this
CI/CD to test on (there's a companion Scala/Spring Boot app in my blog's original post that you 
can use with this), and in seedJob.xml do change the userRemoteConfigs to the URL of the jenkins
pipeline repo itself. 

To run docker container: 

./gradlew build docker dockerRun

Jenkins will then be available at http://localhost:8080