# Reference
1. https://www.youtube.com/watch?v=PGyhBwLyK2U

# Gitlab Infra for CI-CD 
1. Gitlab infra for running a pipeline: gitlab server leveraging gitlab runner.
2. Execution of job
    1. Gitlab runner will execute the job
    2. pulls docker image as per job config/default docker image
    3. start docker container
    4. git pull the project within the container
    5. run the commands mentioned in script tag
    6. job result returned to gitlab server from runner
    7. gitlab server terminate the container

# Gitlab Job & stages in pipeline
1. jobs with dependencies achieved using concept of stages
2. parallel run of jobs can happen in single stage
3. stages execute in sequence of defined order in config
   
# Gitlab pipleline config
1. defined in ".gitlab-ci.yml"

## JOB level Config
1. image: base docker image to start the job with by gitlab runner
2. stage: specify job is part of which stage
3. script: commands to execute once dockerized container with project code is setup by gitlab runner running current job.
4. artifacts: to save current job results withhin gitlab infra and reuse in subsequent jobs.
5. rules: conditional run of jobs
6. environment
    1. Helps in reusing the same steps of job to be run for different environments like dev, stg. and prod.
    2. gitlab variables can have per environemnt values.

# Continous Integration
Automate and safely push code to master/stag(pre pod) env. 

## How to keep master branch green
1. dev do feture development in feature branches
2. direct push to master is blocked via gitlab/github config.
3. merge to master only via Pull Request with CI pipeline is green

# Continous Deployment versus Continous Delivery
Automation where commit will lead to prod release is Continous deployment
Automation where commit is propogated till stg./prepod env. and manual intervention is need for prod deployment. Use gitlab rules to conditional deploy to prod env.

# Gitlab Variables - Protected and Masking
1. Protected - not available across different branches
2. Masking - this avoids password to be printed in logs

# Gitlab CI Pipeline - AWS Integration
## S3 access(host website, cp, sync files etc.)
1. create IAM user in AWS with policy of programmatic access to s3 buckets
2. Store following variables in gitlab CI
    1. AWS_ACCESS_KEY_ID
    2. AWS_SECRET_ACCESS_KEY
    3. AWS_DEFAULT_REGION
3. Use aws cli to use above credentials and talk to s3

