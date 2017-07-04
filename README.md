# Android SDK Gradle
[![/android-sdk-gradle](http://dockeri.co/image/alexisduque/android-sdk-gradle)](https://hub.docker.com/r/alexisduque/android-sdk-gradle/)

## Included
* OpenJDK 8
* Git
* Gradle 4.0
* Android SDK (android-25)
* Android Build-tools (25.0.3)
* Android Support Libraries
* Google Play Services

## Build image

```bash
docker build -t alexisduque/android-sdk-gradle .
```

## Push build version to repository

```bash
docker push alexisduque/android-sdk-gradle 
```
## Usage
### GitLab CI
This is what my .gitlab-ci.yml looks like:

```yaml
image: alexisduque/android-sdk-gradle

stages:
- build

before_script:
- export GRADLE_USER_HOME=$(pwd)/.gradle
- chmod +x ./gradlew

cache:
  key: ${CI_PROJECT_ID}
  paths:
  - .gradle/

build:
  stage: build
  script:
  - ./gradlew assembleDebug
  only:
    - master
  artifacts:
    paths:
    - app/build/outputs/apk/app-debug.apk
```
### Without GitLab

```bash
docker pull alexisduque/android-sdk
```
Change directory to your project directory, then run:

```bash
docker run --tty --interactive --volume=$(pwd):/opt/workspace --user `id -u` --workdir=/opt/workspace --rm alexisduque/android-sdk-gradle /bin/sh -c "gradle build"
```
