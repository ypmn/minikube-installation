# minikube-installation
Installation of Minikube on EC2 Ubuntu

1. Install kubectl

curl -LO https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl


chmod +x ./kubectl


sudo mv ./kubectl /usr/local/bin/kubectl


2. Install Docker

bash <(curl -Ls https://raw.githubusercontent.com/ypmn/ypmn-k8s/master/scripts/docker-install.sh)


3. Install Minikube

curl -Lo minikube https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64 && chmod +x minikube && sudo mv minikube /usr/local/bin/


4. Check Minikube Version

minikube version

###############################################   We have now successfully installed Minikube!

######################################            Let’s test it!

############################                      Running Minikube on EC2 Ubuntu

######################                            Become a root user.

5. if you want 
sudo -i


If you are not comfortable running commands as root, you must always add sudo before the commands minikube and kubectl.

6. Start Minikube

minikube start --vm-driver=none



Do not worry about the warning. As long as you see the message ‘Kubectl is now configured to use the cluster.’ you have successfully ran Minikube.

Note: In the Install Minikube documentation from Kubernetes.io it says that you need to enable virtualization by accessing the computer’s BIOS. For EC2 Instances we do not have access to the BIOS since AWS EC2 instance is a Virtual Machine. Thus we are using the --vm-driver=none tag. No need to install a Hypervisor (VirtualBox or KVM)

7. Check the status of Minikube

minikube status


If you see the status as ‘running’ then we can now run kubectl commands.

8. Let us run our first container

kubectl run hello-minikube --image=gcr.io/google_containers/echoserver:1.4 --port=8080



9. Expose the container ports so that we can access it.

kubectl expose deployment hello-minikube --type=NodePort


10. Know the service with port 

kubectl get services --all-namespaces

11. Access the our container via the EC2 Instance Port on a web browser.

The address is <ipv4_public_ip>:<ec2_port>.




12. Delete the exposed service (port)

kubectl delete services hello-minikube



13. Delete the deployed container (hello-minikube)

kubectl delete deployment hello-minikube


14.Stopping Minikube/Shutting Down the Cluster

minikube stop

