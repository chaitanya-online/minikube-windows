
# Minikube for Windows


Minikube is a tool that enables you to run Kubernetes clusters locally on your Windows machine. It is particularly useful for development, testing, and learning Kubernetes concepts without needing access to a cloud or remote Kubernetes cluster.

Installation Steps
Download Kubectl

https://kubernetes.io/docs/tasks/tools/install-kubectl-windows/

![img.png](img.png)

Download Minikube:
Download the Minikube installer for Windows from the latest release or use   to download and install:


```
New-Item -Path 'c:\' -Name 'minikube' -ItemType Directory -Force
Invoke-WebRequest -OutFile 'c:\minikube\minikube.exe' -Uri 'https://github.com/kubernetes/minikube/releases/latest/download/minikube-windows-amd64.exe' -UseBasicParsing
```

2) Set Environment Variables:
Set the Minikube and Kubectl  folder path in the environment variables:

![img_1.png](img_1.png)

![img_2.png](img_2.png)


 
 
3) Make sure to run PowerShell as Administrator.
```
$oldPath = [Environment]::GetEnvironmentVariable('Path', [EnvironmentVariableTarget]::Machine)
if ($oldPath.Split(';') -inotcontains 'C:\minikube'){
[Environment]::SetEnvironmentVariable('Path', $('{0};C:\minikube' -f $oldPath), [EnvironmentVariableTarget]::Machine)
}
```

4) Start Docker Engine:
Ensure that the Docker engine is running on your machine.

Start Minikube:
Open CMD and run the following command to start Minikube using the Docker driver:
```
minikube start --driver=docker
```
![img_3.png](img_3.png)

Check Status:
After Minikube has started successfully, check its status using below comand : 
```
minikube status
```
Usage
With Minikube running, you can now interact with your local Kubernetes cluster using kubectl commands. You can deploy, manage, and test your Kubernetes applications directly on your Windows machine.

![img_4.png](img_4.png)

To get cluster details use below command :"

```
kubectl cluster-info
```

![img_5.png](img_5.png)

To get nodes infomation

```
kubectl get nodes
```

![img_6.png](img_6.png)


All Set now we are using local docker to communicate with minikube so we have to use below command

```
minikube docker-env
```


![alt text](image-1.png)
--------------------------------


Now Create a docker image in my case am using 2048-game image 

Replo link :- https://github.com/chaitanya-online/2048-game

After cloning repo goto directory of repo in local machine and type below command

```

docker build -t richeb/2048-game .
```

![img_7.png](img_7.png)

----------------------------------

Now After successfully building the docker file have to apply manifest file
Check manifest.yaml in root directory of this Repo


```
kubectl apply -f manifest.yaml
```

![img_8.png](img_8.png)



Check status by using  below command

```
kubectl get pods
```

```
kubectl logs <pod name>
```

![alt text](image-2.png)

----------------------------------

Check ip by using  below commands

```
kubectl get svc
```

```
minikube service game-service-2048 --url
```

![alt text](image-3.png)

Now access the application in browser by using

http://127.0.0.1:53349/

![alt text](image-5.png)

--------------


To See the Full Dashboard

```
minikube dashboard
```


![alt text](image-4.png)

http://127.0.0.1:53877/api/v1/namespaces/kubernetes-dashboard/services/http:kubernetes-dashboard:/proxy/#/workloads?namespace=default

![alt text](image-6.png)



Enjoy exploring and learning Kubernetes with Minikube!!
