# Docker-Manual-Deployment-for-Frontend-Backend-Application(Full-Stack)

Step Up the Server on Azure / AWS Ubuntu vm 24
sudo apt update & sudo apt upgrade -y
docker
sudo snap install docker
sudo chmod 666 /var/run/docker.sock
docker network create aitech

docker run -p 5432:5432 --name computex -e POSTGRES_PASSWORD=12345 -e POSTGRES_DB=computex -e POSTGRES_USER=admin -d --network aitech postgres


GO TO GITHUB AND GET THE  REPO FOR THE FULL-STACK
git clone https://github.com/soundn/Containerisation-React-Django-App
cd Containerisation-React-Django-App/


MOVE TO THE FRONTEND      “ComputexFrontend”
cd ComputexFrontend
ls
nano src/components/api/auth.ts
Change the IP Address
docker build -t computexfrontend .
docker image ls
docker run -d --name frontend -p 5173:5173 --network aitech computexfrontend
docker logs frontend
Validate 
72.144.23.229:5173



MOVE TO BACKEND
ls
cd computex
nano Computex/settings.py

THIS DATABASE IS JUST HOW IT LOOK DO NOT RUN IT AGAIN
DATABASES = {
    "default": {
        "ENGINE": "django.db.backends.postgresql",
        "NAME": "computex",      I change this 
        "USER": "admin",
        "PASSWORD": "12345",
        "HOST": “72.144.54.46”,          I change this 
        "PORT": "5432"
    }
}

Ls
cat Dockerfile
docker build -t backend .
docker image ls

START THE BACKEND
docker run -d --name computexbackend -p 8000:8000 --network aitech backend
docker ps
docker logs computexbackend



CHECK IF IT WORKING BY USING THE IP
http://72.144.54.46:8000/
