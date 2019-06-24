# Install docker
The steps I followed to install docker in my centos 7 VM offline, taken from docker.com
  1. Go to https://download.docker.com/linux/centos/7/x86_64/stable/Packages/ and download the .rpm file for the Docker version you want to install.
  2. Install Docker CE, changing the path below to the path where you downloaded the Docker package.
      $ sudo yum install /path/to/package.rpm
      
 But this gave me error. The cause was that I had configured the docker repository to download docker. So, I had to remove that. I run the
 following command.
      $ yum-config-manager --disable docker-ce-edge

Than, again I tried running install command.
Start the docker
        systemctl start docker
Test docer docler run hello-world.

Install Kubernetes Client (kubectl)
KUBE_VERSION=v1.12.2
or if latest stable: 
KUBE_VERSION=$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)
curl -Lo kubectl https://storage.googleapis.com/kubernetes-release/release/${KUBE_VERSION}/bin/linux/amd64/kubectl \
  && chmod +x kubectl \
  && mv -f kubectl /usr/local/bin/ \
  && kubectl version

# Output:
% Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100 54.6M  100 54.6M    0     0   421k      0  0:02:13  0:02:13 --:--:-- 13.8M
Client Version: version.Info{Major:"1", Minor:"12", GitVersion:"v1.12.2", GitCommit:"17c77c7898218073f14c8d573582e8d2313dc740", GitTreeState:"clean", BuildDate:"2018-10-24T06:54:59Z", GoVersion:"go1.10.4", Compiler:"gc", Platform:"linux/amd64"}
The connection to the server localhost:8080 was refused - did you specify the right host or port?

# Install minikube:
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64  \
  && install minikube-linux-amd64 /usr/local/bin/minikube \
  && minikube version

#Output
% Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100 40.3M  100 40.3M    0     0   311k      0  0:02:12  0:02:12 --:--:-- 8693k
minikube version: v0.30.0

# Remove minikube
sudo yum remove kubeadm kubectl kubelet kubernetes-cni kube
sudo yum autoremove
sudo rm -rf ~/.kube
