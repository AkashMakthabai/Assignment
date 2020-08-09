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
docker tag nodejs:latest 724994165886.dkr.ecr.ap-southeast-1.amazonaws.com/nodejs:latest\
docker push 724994165886.dkr.ecr.ap-southeast-1.amazonaws.com/nodejs:latest\



