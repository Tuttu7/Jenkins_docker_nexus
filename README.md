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

![Screenshot_20210902_114604](https://user-images.githubusercontent.com/56312182/131793395-357d8d3b-1eb9-418c-b846-a491710050f4.png)

#### Creating a repository in-order to push the jar file to nexus repository

![Screenshot_20210902_120132](https://user-images.githubusercontent.com/56312182/131793970-b0063ea3-3268-41f2-980b-40b1ebfc2b41.png)

#### Create a password text file to pass the login password of nexus user created in above step

```
cat my_password.txt | sudo docker login --username tuttu --password-stdin localhost:8030
```

#### Create a tag to link the created image to nexus repository

```
sudo docker tag tuttu_project localhost:8030/tuttu-repo-git/tuttu_project
```
#### Finally push the image to nexus repository

```
sudo docker push localhost:8030/tuttu-repo-git/tuttu_project
```

#### Final code :

```
git clone http://tuttu@git.ndzhome.com/tuttu/project1.git
cd project1
./mvnw package
cd /opt/jenkins/workspace/tuttu-project/
sudo docker build -t tuttu_project .
cat my_password.txt | sudo docker login --username tuttu --password-stdin localhost:8030
sudo docker tag tuttu_project localhost:8030/tuttu-repo-git/tuttu_project
sudo docker push localhost:8030/tuttu-repo-git/tuttu_project
```

#### Once the above process is success we get as follows

![Screenshot_20210902_121143](https://user-images.githubusercontent.com/56312182/131795465-38435297-e0d9-497b-b38d-e580e1e3809b.png)

#### The image will be uploaded in nexus

![Screenshot_20210902_121504](https://user-images.githubusercontent.com/56312182/131795572-b43e9eff-2e36-4ea1-aa7a-03ec6a039fc9.png)



