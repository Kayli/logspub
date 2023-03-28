# notes on aws cloud services


## compute services

- ec2: virtual machines
- ecs: elastic container services
  - managed container orchestration service
  - operates with clusters and tasks
- fargate
  - run docker containers without managing any servers for container orchestration
- lambda
  - time limit of 15 minutes per function
  - runs on ephemeral containers behind the scenes
  - it is possible to set concurrency limits on individual aws lambda functions

- copilot
  - cli for containerized applications
  - manages following services behind the scenes
    - ecs (container orchestration services)
    - fargate (serverless compute for containers)
    - app runner 
  - supports IaaC via yaml manifests


## data services

- s3
- redshift: big data analysis platform (etl, bi, reports)
- aurora
- dynamodb


## container repository service (ecr)

- create repository
  > aws ecr create-repository 


## other services

- vpc (network management)
- cloudfront (content delivery network)
- elastic cache (in-memory caching)
- sns (notification service)


## useful tools

- localstack (most popular aws services available locally) https://www.youtube.com/watch?v=8hi9P1ffaQk
  - it is possible to use iac tools like pulumi with localstack