# Docker Cluster for AWS with ansible

## Dependencies

Install ansible, awscli and boto

```
sudo pip install ansible awscli botocore boto3
```

Configure your AWS credencials

```
aws configure
```

You need to generate a key pair on AWS Console and add its name on
'template_parameters' section inside **deploy.yml**

## Creating Swarm Cluster

```
ansible-playbook deploy.yml
```

This command will create a stack on cloudformation on AWS, please check the stack

**This cloudformation template was done by Docker for the Docker-for-aws product**

## Configuring your access to docker Swarm

After create the stack, check the output and click on Managers link and get the
public DNS name.

```
ssh -i <path-to-private-key> -NL localhost:2374:/var/run/docker.sock docker@<public DNS name> &
export DOCKER_HOST='localhost:2374'
docker info
```

## To deploy example app

```
docker deploy --compose-file docker-compose.yml example
```
