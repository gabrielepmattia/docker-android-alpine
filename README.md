# docker-android-alpine

[gabrielepmattia/android-build:latest](https://hub.docker.com/r/gabrielepmattia/android-build)

This Docker image contains the Android SDK and most common packages necessary for building Android apps in a CI tool like GitLab CI. Make sure your CI environment's caching works as expected, this greatly improves the build time, especially if you use multiple build jobs.

A `.gitlab-ci.yml` with caching of your project's dependencies would look like this:

```
image: preventis/android-build:latest

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
  artifacts:
    paths:
    - app/build/outputs/apk/app-debug.apk
```

## Credits

- [Preventis](https://github.com/Preventis) for the [original docker android image](https://github.com/Preventis/docker-android-alpine)
