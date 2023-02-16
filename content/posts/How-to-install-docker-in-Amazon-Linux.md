---
                title: How-to-install-docker-in-Amazon-Linux
                date: 2021-01-01    
                draft: true
                tags: []
               ---


            # How-to-install-docker-in-Amazon-Linux

# How to install docker in Amazon Linux
Created: June 13, 2020 12:14 AM
URL: https://www.lewuathe.com/how-to-install-docker-in-amazon-linux.html
!Our daily development tends to depend on the container platform highly.But I found AWS Linux I recently launched does not have Docker engine as default.Here is the process to install Docker engine in your AWS Linux.That article is written mainly for avoiding my memory lost :)
FYI: The AMI I used in this experiment is `ami-0f9ae750e8274075b`.# Install Docker Engine
```
$ sudo yum update -y
$ sudo yum install -y docker
$ sudo service docker start
Starting cgconfig service: [ OK ]
Starting Docker: [ OK ]
```
# Add User Group
But you need to prepend `sudo` every time you run docker command.```
$ sudo usermod -a -G docker ec2-user
```
After you log in the instance again, you should be able to run docker command without any difficulty.