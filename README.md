<h1># ml-cnn-model</h1>

![Head](https://github.com/Jatinbanger/mlcnnmodel/blob/master/images/Capture.PNG)

**This task is to automate the process of a perfect model creation by changing the hyperparams based on accuracy rate of model**

Pre-requisite:
1. Jenkins 
2. Docker
3. Github
4. Machine learning model

<h3>Building and starting the container from dockerfile</h3>
1. Copy dockerfile in rhel8 system
2. Run : docker build -t cnn:v1 <path/to/dockerfile>
3. We need to create a volume attachment also for the docker so that we can put the files in that volume to be run in the docker.
4. docker run -d -it --name cnntrainer --mount type=bind,source=<path/to/host/sourcedir>,target=<path/to/dockerhost/targetdir> cnn:v1
5. After to inspect whether the volume is attached or not use.
6. docker inspect cnntrainer : Look for Mounts section, your volume attachement will be present there.
7. In <path/to/host/sourcedir> put the Mymodel.py, cnn_dataset and configuration.txt
 
 
> Sometimes the target directory inside won't be giving permission to write anything
> Use the following command to resolve this issue
> chcon -Rt svirt_sandbox_file_t <path/to/host/sourcedir>
> Restart the docker container

<h3>Jenkins setup</h3>
 - Install Java first : sudo yum install java-1.8.0-openjdk-devel
 - Enable Jenkins Repo : curl --silent --location http://pkg.jenkins-ci.org/redhat-stable/jenkins.repo | sudo tee /etc/yum.repos.d/jenkins.repo
 - sudo rpm --import https://jenkins-ci.org/redhat/jenkins-ci.org.key
 - Install Jenkins : sudo yum install jenkins
 - Start Jenkins : sudo systemctl start jenkins
 - Access Jenkins : http://your_ip_or_domain:8080
 - Provide the first time password from : sudo cat /var/lib/jenkins/secrets/initialAdminPassword
 - Install Plugins and start using Jenkins

<h4>Task 1 :: Polling to the developers repository and pulling the code whenever there is change in the code.</h4>

![Task1_1](https://github.com/Jatinbanger/mlcnnmodel/blob/master/images/Task1_1.png)

![Task1_2](https://github.com/Jatinbanger/mlcnnmodel/blob/master/images/Task1_2.png)

![Task1_3](https://github.com/Jatinbanger/mlcnnmodel/blob/master/images/Task1_3.png)


<h3>Task 2 :: Run the container for cnn code (as of now)</h3>

![Task2_1](https://github.com/Jatinbanger/mlcnnmodel/blob/master/images/Task2_1.png)

![Task2_2](https://github.com/Jatinbanger/mlcnnmodel/blob/master/images/Task2_2.png)


<h3>Task 3 :: Train the model using the pulled code and dataset</h3>

![Task3_1](https://github.com/Jatinbanger/mlcnnmodel/blob/master/images/Task3_1.png)

![Task3_2](https://github.com/Jatinbanger/mlcnnmodel/blob/master/images/Task3_2.png)


<h3>Task 4 :: Retrain model if accuracy is less then 80%</h3>

![Task4_1](https://github.com/Jatinbanger/mlcnnmodel/blob/master/images/Task4_1.png)

![Task4_2](https://github.com/Jatinbanger/mlcnnmodel/blob/master/images/Task4_2.png)


<h3>Task 5 :: Monitor the Container</h3>

![Task5_1](https://github.com/Jatinbanger/mlcnnmodel/blob/master/images/Task5_1.png)

![Task5_2](https://github.com/Jatinbanger/mlcnnmodel/blob/master/images/Task5_2.png)
