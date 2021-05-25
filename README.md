Create AWS codepipeline for angular app and deploy via cloudfront:
1) Take the github repository:https://github.com/awstechguide/angular-demo
and watch video till ceation of S3 bucket.: https://www.youtube.com/watch?v=2VuULW1yNHE
everything is at my own github : https://github.com/krunalbhoyar/aws-s3-cloudfront.git
___________________
buildspec.yaml
version: 0.2

env:
    variables:
        CACHE_CONTROL: "86400"
        S3_BUCKET: "{{s3_bucket_url}}"
        BUILD_FOLDER: "dist"
phases:
  install:
    runtime-versions:
        nodejs: 14
    commands:
        - echo Installing source NPM dependencies...
        - npm install
        - npm install -g @angular/cli
  build:
    commands:
        - echo Build started 
        - ng build
artifacts:
    files:
        - '**/*'
    base-directory: 'dist*'
    discard-paths: yes
====================================================
after this create distribution in aws cloudfront: and there is no need of domain
watch video: https://www.youtube.com/watch?v=-DDGYzKtNwc&t=118s
then search the url given in cloudfront. every time we have to create new distribution in cloudfront
================ Done =================



sample buildspec.yaml files
___________________
https://github.com/sudolabs-io/sudo-app/blob/develop/buildspec.yml
version: 0.2

phases:
  pre_build:
    commands:
      - cd client && npm install && cd ..
      - cd server && npm install && cd ..
  build:
    commands:
      - cd client && npm run build && cd ..
  post_build:
    commands:
      - mv ./client/build ./build
artifacts:
  secondary-artifacts:
    client:
      files:
        - '**/*'
      base-directory: build
    server:
      files:
        - '**/*'
      base-directory: server
_________________________
https://apoorv.blog/deploy-reactjs-cloudfront-codepipeline-cdk/
version: 0.2

phases:
  install:
    runtime-versions:
      nodejs: 14.x
    commands:
      - echo Installing npm packages
      - npm install
      - npm update
  build:
    commands:
      - echo Building react app
      - npm run build
      - echo Built react app on `date`

artifacts:
  base-directory: ./build
  files:
    - '**/*'
_______________________________
