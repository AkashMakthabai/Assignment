# Assignment
mkdir Assignment\
cd Assignment/\
git init\
git add .\
git commit -m "Assignment files"\
git remote add origin https://github.com/Akhilnagothu18/Assignment.git\
git push -u origin master\
Username for 'https://github.com': Akhilnagothu18\
Password for 'https://Akhilnagothu18@github.com':\
Counting objects: 7, done.\
Compressing objects: 100% (6/6), done.\
Writing objects: 100% (6/6), 5.13 KiB | 0 bytes/s, done.\
Total 6 (delta 0), reused 0 (delta 0)\
To https://github.com/Akhilnagothu18/Assignment.git\
   db3c55a..2439a95  master -> master\
Branch master set up to track remote branch master from origin.\

# AWS ECR Login and pushing the image to registry :

aws ecr get-login-password --region ap-southeast-1 | docker login --username AWS --password-stdin 724994165886.dkr.ecr.ap-southeast-1.amazonaws.com\
docker build -t nodejs .\

docker build -t nodejs .\
Sending build context to Docker daemon 79.87 kB\
Step 1/7 : FROM node\
 ---> 2b9604a36e49\
Step 2/7 : WORKDIR /app\
 ---> Using cache\
 ---> 9e30c17c2227\
Step 3/7 : COPY package.json /app\
 ---> Using cache\
 ---> c60e15cdecc1\
Step 4/7 : RUN npm install\
 ---> Using cache\
 ---> eee1fcd92195\
Step 5/7 : COPY . /app\
 ---> 9d124dba03a4\
Removing intermediate container 46847cf728ef\
Step 6/7 : CMD node index.js\
 ---> Running in 991cb29276fb\
 ---> a637b370cfab\
Removing intermediate container 991cb29276fb\
Step 7/7 : EXPOSE 3000\
 ---> Running in fd4ba9f7138e\
 ---> 63828eb39179\
Removing intermediate container fd4ba9f7138e\
Successfully built 63828eb39179\

docker tag nodejs:latest 724994165886.dkr.ecr.ap-southeast-1.amazonaws.com/nodejs:latest\
docker push 724994165886.dkr.ecr.ap-southeast-1.amazonaws.com/nodejs:latest\

# Docker containers

docker run -dt --name node_js -p 3000:3000 shivaji1/nodejsapp\
23e7aff0e3276f4b66fa991c73091237a00834982cf13d10aa8bad821c1bb34c\

docker ps\
CONTAINER ID        IMAGE                COMMAND                  CREATED             STATUS              PORTS                             NAMES\
23e7aff0e327        shivaji1/nodejsapp   "docker-entrypoint..."   6 seconds ago       Up 5 seconds        0.0.0.0:3000->3000/tcp            node_js\
0ce369fd0fdd        nodejs               "docker-entrypoint..."   8 minutes ago       Up 8 minutes        3000/tcp, 0.0.0.0:32768->80/tcp   node-js

# KOPS for Kubernetes Clustering

Used kops for kubernetes cluster since I have experience with AWS and Kops is the clustering type which works on AWS.

First installed Kops and kubectl to create cluster and respective nodes for deployment.\

KOPS Installation:

curl -LO https://github.com/kubernetes/kops/releases/download/$(curl -s https://api.github.com/repos/kubernetes/kops/releases/latest | grep tag_name | cut -d '"' -f 4)/kops-linux-amd64\
chmod +x kops-linux-amd64\
sudo mv kops-linux-amd64 /usr/local/bin/kops

Kubectl Installation :

curl -LO "https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl"\
chmod +x ./kubectl\
sudo mv ./kubectl /usr/local/bin/kubectl

Below is the output of creation of cluster using kops command.\

kops create cluster --yes --state=s3://kops-storage-12908 --zones=ap-southeast-1a,ap-southeast-1b --node-count=2 --node-size=t2.micro --master-size=t2.medium --name=test1.k8s.local

I0809 13:44:58.024037    2155 create_cluster.go:557] Inferred --cloud=aws from zone "ap-southeast-1a"\
I0809 13:44:58.084518    2155 subnets.go:184] Assigned CIDR 172.20.32.0/19 to subnet ap-southeast-1a\
I0809 13:44:58.084539    2155 subnets.go:184] Assigned CIDR 172.20.64.0/19 to subnet ap-southeast-1b\
I0809 13:44:58.334533    2155 create_cluster.go:1547] Using SSH public key: /home/centos/.ssh/id_rsa.pub\
I0809 13:45:01.448881    2155 apply_cluster.go:545] Gossip DNS: skipping DNS validation\
I0809 13:45:01.743950    2155 executor.go:103] Tasks: 0 done / 94 total; 42 can run\
I0809 13:45:02.612136    2155 vfs_castore.go:590] Issuing new certificate: "etcd-manager-ca-events"\
I0809 13:45:02.873224    2155 vfs_castore.go:590] Issuing new certificate: "apiserver-aggregator-ca"\
I0809 13:45:03.456451    2155 vfs_castore.go:590] Issuing new certificate: "ca"\
I0809 13:45:03.601438    2155 vfs_castore.go:590] Issuing new certificate: "etcd-peers-ca-main"\
I0809 13:45:03.625744    2155 vfs_castore.go:590] Issuing new certificate: "etcd-peers-ca-events"\
I0809 13:45:03.881506    2155 vfs_castore.go:590] Issuing new certificate: "etcd-manager-ca-main"\
I0809 13:45:04.249486    2155 vfs_castore.go:590] Issuing new certificate: "etcd-clients-ca"\
I0809 13:45:04.409010    2155 executor.go:103] Tasks: 42 done / 94 total; 27 can run\
I0809 13:45:05.441940    2155 vfs_castore.go:590] Issuing new certificate: "apiserver-proxy-client"\
I0809 13:45:05.803181    2155 vfs_castore.go:590] Issuing new certificate: "kube-proxy"\
I0809 13:45:06.014391    2155 vfs_castore.go:590] Issuing new certificate: "apiserver-aggregator"\
I0809 13:45:06.420738    2155 vfs_castore.go:590] Issuing new certificate: "kube-controller-manager"\
I0809 13:45:06.569812    2155 vfs_castore.go:590] Issuing new certificate: "kubelet"\
I0809 13:45:06.641665    2155 vfs_castore.go:590] Issuing new certificate: "kubecfg"\
I0809 13:45:06.795897    2155 vfs_castore.go:590] Issuing new certificate: "kops"\
I0809 13:45:06.957105    2155 vfs_castore.go:590] Issuing new certificate: "kube-scheduler"\
I0809 13:45:07.055414    2155 vfs_castore.go:590] Issuing new certificate: "kubelet-api"\
I0809 13:45:07.188240    2155 executor.go:103] Tasks: 69 done / 94 total; 21 can run\
I0809 13:45:07.395724    2155 launchconfiguration.go:375] waiting for IAM instance profile "nodes.test1.k8s.local" to be ready\
I0809 13:45:07.401345    2155 launchconfiguration.go:375] waiting for IAM instance profile "masters.test1.k8s.local" to be ready\
I0809 13:45:17.755591    2155 executor.go:103] Tasks: 90 done / 94 total; 3 can run\
I0809 13:45:18.109407    2155 vfs_castore.go:590] Issuing new certificate: "master"\
I0809 13:45:18.407206    2155 executor.go:103] Tasks: 93 done / 94 total; 1 can run\
I0809 13:45:18.690782    2155 executor.go:103] Tasks: 94 done / 94 total; 0 can run\
I0809 13:45:18.759915    2155 update_cluster.go:308] Exporting kubecfg for cluster\
kops has set your kubectl context to test1.k8s.local

Cluster is starting.  It should be ready in a few minutes.

$ kops get clusters\
NAME            CLOUD   ZONES\
test1.k8s.local aws     ap-southeast-1a,ap-southeast-1b

# Created Kubernetes object deploymemt for the manifest file with Imperative command

kubectl create deployment nodejs-deployment --image=shivaji1/nodejsapp:latest

# Exposed the deployment with type Load Balancer to port 80 so that it can be accessed.

kubectl expose deployment nodejs-deployment --type="LoadBalancer" --port=80 --target-port 8080

kubectl run nodejs-deployment --image=shivaji1/nodejsapp:latest --port=80 --expose { for pods }

# Autoscaling for the deployment with cpu 50% and maximum of 10 replicas, ensuring at least 7 replicas are running at all times :

kubectl autoscale deployment nodejs-deployment --cpu-percent=50 --min=7 --max=10





# Thank you !!!!






