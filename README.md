# About the repo:
A repository to help setting up Kubernetes environment on Fedora 31 - Created by Salman Mukhtar
* Preparing linux
* Install & setup docker engine
* Install & setup docker compose
* Install & setup kvm
* Install & setup gcloud (For remote kubernetes cluster)
* Install & setup minikube (For local kubernetes cluster)
* Install & setup Metallb (Load Balancer - Optional)
* Install & setup Heml (Optional)

# Preparing linux

* Disable SELinux
Linux is regarded as one of the most secure operating systems you can use today, that is because of its illustrious security implementation features such as SELinux. Disabling it makes life easier for installation of Docker, Docker compose and so on.

To disble SELinux do the following as root
```
vi /etc/selinux/config
```

