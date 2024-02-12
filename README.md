
Minikube for Windows


Minikube is a tool that enables you to run Kubernetes clusters locally on your Windows machine. It is particularly useful for development, testing, and learning Kubernetes concepts without needing access to a cloud or remote Kubernetes cluster.

Installation Steps
Download Minikube:
Download the Minikube installer for Windows from the latest release or use   to download and install:

 
 
New-Item -Path 'c:\' -Name 'minikube' -ItemType Directory -Force
Invoke-WebRequest -OutFile 'c:\minikube\minikube.exe' -Uri 'https://github.com/kubernetes/minikube/releases/latest/download/minikube-windows-amd64.exe' -UseBasicParsing
Set Environment Variables:
Set the Minikube folder path in the environment variables:

 
 
$oldPath = [Environment]::GetEnvironmentVariable('Path', [EnvironmentVariableTarget]::Machine)
if ($oldPath.Split(';') -inotcontains 'C:\minikube'){
  [Environment]::SetEnvironmentVariable('Path', $('{0};C:\minikube' -f $oldPath), [EnvironmentVariableTarget]::Machine)
}

Start Docker Engine:
Ensure that the Docker engine is running on your machine.

Start Minikube:
Open CMD and run the following command to start Minikube using the Docker driver:

$ minikube start --driver=docker
-----------------------------------
Check Status:
After Minikube has started successfully, check its status using:
$ minikube status
-----------------------------------
Usage
With Minikube running, you can now interact with your local Kubernetes cluster using kubectl commands. You can deploy, manage, and test your Kubernetes applications directly on your Windows machine.
-----------------------------------
to get cluster details
$ kubectl cluster-info
-----------------------------------
to get nodes infomation
$ kubectl get nodes
-----------------------------------


All Set now we are using local docker to communicate with minikube so we have to use below commmand

$ minikube docker-env


![alt text](image-1.png)
--------------------------------


Now Create a docker image in my case am using 2048-game image 

Replo link :- https://github.com/chaitanya-online/2048-game

After cloning repo goto directory of repo in local machine and type below command

docker build -t richeb/2048-game .


----------------------------------

Now After sucessfull building the docker file have to apply manifest file

kubectl apply -f manifest.yaml

---------------------------------

check status by using 

kubectl get pods

kubectl logs <pod name>

![alt text](image-2.png)

----------------------------------

check ip by using 

kubectl get svc
$ minikube service game-service-2048 --url

![alt text](image-3.png)

Now access the application in browser by using

http://127.0.0.1:53349/

![alt text](image-5.png)

--------------


To See the Full Dashboard

![alt text](image-4.png)

http://127.0.0.1:53877/api/v1/namespaces/kubernetes-dashboard/services/http:kubernetes-dashboard:/proxy/#/workloads?namespace=default

![alt text](image-6.png)
Create manifest file for check manifest.yaml in root directory 
Enjoy exploring and learning Kubernetes with Minikube!
