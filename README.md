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

* **Disable SELinux**

Linux is regarded as one of the most secure operating systems you can use today, that is because of its illustrious security implementation features such as SELinux. Disabling it makes life easier for installation of Docker, Docker compose and so on.

To disble SELinux do the following as root
```
vi /etc/selinux/config
```
Change following line (As shown in the picture)

`SELINUX=enforced`
 
With

`SELINUX=disabled`


| ![images/selinux.png](images/selinix.png) |
| ------------------------------------------------------------------- |

* **Disable firewall**

To disable the firewall use following command as Root user
```
systemctl disable firewalld
```
* **Install Docker**

1 - Make sure you have latest version of docker. Remove older version of docker if installed. Run following command
```
udo dnf remove docker \
                  docker-client \
                  docker-client-latest \
                  docker-common \
                  docker-latest \
                  docker-latest-logrotate \
                  docker-logrotate \
                  docker-selinux \
                  docker-engine-selinux \
                  docker-engine
```

2 - Install docker by using repository method
```
sudo dnf -y install dnf-plugins-core

sudo dnf config-manager \
    	--add-repo \
    	https://download.docker.com/linux/fedora/docker-ce.repo

sudo dnf install docker-ce docker-ce-cli containerd.io
 ```
3 - Add your user to group docker 

Make sure your user is a member of the group "docker". If not, add it with gpasswd -a <username> docker. You will need to logout (of the GUI session) and login again for the changes to take effect. Run the following command as **Root** user.

`gpasswd -a salman docker`

4 - Cgroups Exception

First install grubby by using following command
```
yum install -y grubby
```

For Fedora 31 and higher, you need to enable the [backward compatibility for Cgroups](https://fedoraproject.org/wiki/Common_F31_bugs#Other_software_issues)

```
grubby --update-kernel=ALL --args="systemd.unified_cgroup_hierarchy=0"
```

After running the command, you must reboot for the changes to take effect.

5 - Enable & Start Docker

After reboot run following commands to enable and run docker engine.

```
systemctl enable docker
systemctl start docker
```
