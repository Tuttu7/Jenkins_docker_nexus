#### Configure a Jenkins job to create dockerized build of java application and push the same to nexus repository.

#### Tools Required :

```
1. Gitlab
2. Jenkins
3. Maven
4. Docker
5. Nexus
```
#### Jenkins Build Stages :

```
1. Clone the repository to Jenkins server.
2. Create the jar using Maven.
3. Build the docker image including the jar.
4. Push the docker image to nexus.
```
#### Setup a Jenkins Job

```
git clone http://tuttu@git.ndzhome.com/tuttu/project1.git
cd project1
./mvnw package
```
#### Now the jar file is created. Now we need to build the docker image, for that run below command in jenkins build area

```
cd /opt/jenkins/workspace/tuttu-project/
sudo docker build -t tuttu_project .
```

#### Create user in nexus with username and a password

![Screenshot_20210902_114604.png]


