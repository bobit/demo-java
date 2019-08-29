# demo-spring-template
[![Build Status](https://travis-ci.org/bobit/demo-java.svg?branch=master)](https://travis-ci.org/bobit/demo-java)

```
language: java

# 指定需要sudo权限
sudo: required
jdk:
- openjdk8

install: mvn install -DskipTests=true -Dmaven.javadoc.skip=true
script: mvn test

# 指定执行脚本的分支
branches:
  only:
  - master

cache:
  directories:
  - '$HOME/.m2/repository'
  - '$HOME/.sonar/cache'
  ```
  
  
```







```