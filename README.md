# demo-spring-template

```
language: java
  jdk:
   - openjdk8
  install: cd Hello && mvn install -DskipTests=true -Dmaven.javadoc.skip=true
  script: mvn test
  
  ```
  
  
```
language: java
sudo: false
install: true


jdk:
- oraclejdk8

services:
- docker

env:
  global:
  - secure: "encrypted-sonar-token"
  - secure: "encrypted-dockerhub-username"
  - secure: "encrypted-dockerhub-password"
  - secure: "encrypted-heroku-api-key"
  - COMMIT=${TRAVIS_COMMIT::7}

addons:
  sonarcloud:
    organization: "bobit"
    token:
      secure: $SONAR_TOKEN
script:
- ./mvnw clean install -B
- ./mvnw clean org.jacoco:jacoco-maven-plugin:prepare-agent package sonar:sonar

after_success:
- docker login -u $DOCKER_USER -p $DOCKER_PASS
- export TAG=`if [ "$TRAVIS_BRANCH" == "master" ]; then echo "latest"; else echo $TRAVIS_BRANCH&amp;amp;amp;amp;amp;amp;lt;span data-mce-type="bookmark" style="display: inline-block; width: 0px; overflow: hidden; line-height: 0;" class="mce_SELRES_start"&amp;amp;amp;amp;amp;amp;gt;&amp;amp;amp;amp;amp;amp;lt;/span&amp;amp;amp;amp;amp;amp;gt;; fi`
- export IMAGE_NAME=bobit/demo-java
- docker build -t $IMAGE_NAME:$COMMIT .
- docker tag $IMAGE_NAME:$COMMIT $IMAGE_NAME:$TAG
- docker push $IMAGE_NAME

cache:
  directories:
  - '$HOME/.m2/repository'
  - '$HOME/.sonar/cache'







```