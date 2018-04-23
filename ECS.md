# ECS

https://docs.aws.amazon.com/AmazonECS/latest/developerguide/Welcome.html

 ECS (Elastic Container Service) is a container orchestration service that supports Docker containers.

 * One region, but more AZ
 * ECS is an AWS managed alternative to systems like Kubernetes, Mesos or Docker Swarm

### ECS concepts
* Cluster
* Service
* Task

#### Task
A __task__ is a description of how a container should be started. Think of it like specifying the parameters of a _docker run_ command + some AWS specific settings.
* 1-10 containers

#### Service
* A group of __tasks__
* Auto scaling has to be triggered by _Cloudwatch Alarms_
* Keeps a number of Tasks running

#### Cluster
* Region Specific
* IAM policy is the same in the same cluster
* Auto scale EC2's


# How to manage ECS
* Web UI
* aws cli
* CloudFormation

# Auto Scaling
https://aws.amazon.com/blogs/compute/automatic-scaling-with-amazon-ecs/
* Auto Scaling Group

* AZ aware

* Cluster and Service are scaled separately
