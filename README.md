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

# AWS ECR Login :

aws ecr get-login-password --region ap-southeast-1 | docker login --username AWS --password-stdin 724994165886.dkr.ecr.ap-southeast-1.amazonaws.com\
docker build -t nodejs .\

docker build -t nodejs .\
Sending build context to Docker daemon 79.87 kB\
Step 1/7 : FROM node:13\
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



