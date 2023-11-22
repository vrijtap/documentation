# Backend [Golang]

In order for our project to function, we need a UI. For this we decided to use a website that's being hosted using a Golang backend.

## reason

The main reason why we are implementing a Golang backend is because it is a relatively new, but popular choice for backend development. In the previous semester I (Brian) had a course in backend development, but this was in Typescript, so in order to broaden my skill-set, I wanted to apply the knowledge I've gained in a new environment. Besides that, I wanted to actually secure the backend using TLS, because we didn't touch that subject in the course.

## Installing Go

The first step in executing the backend would be to install the programming language on a pi.

```bash
sudo apt update
sudo apt upgrade
```

Fetch, install and delete the Installation Files. Before you do this step, check if you are actually running an arm64 chipset and you might want to migratge the backend to a newer version when the next stable long term support version of Go releases.

```bash
wget https://go.dev/dl/go1.21.1.linux-arm64.tar.gz
sudo tar -C /usr/local -xzf go1.21.1.linux-arm64.tar.gz
rm go1.21.1.linux-arm64.tar.gz
```

Edit the raspberry pi profile config

```bash
nano ~/.profile
```

Add to the bottom of the file and save:

```bash
PATH=$PATH:/usr/local/go/bin
GOPATH=$HOME/go
```

Refresh the rasp pi config and check the go version

```bash
source ~/.profile
go version
```

## Creating Test CA Certificates

In order for us to run and debug HTTPS, we need to supply our backend with the correct certificates. OpenSSL allows us to sign our own CA Certificates, but these do not work in production as they are not supported by any actual certificate authority. In production, this ofcourse would need to be changed.

```bash
sudo apt update
sudo apt upgrade
sudo apt install openssl
```

Create test certificates and protect them. The reason why we need to give everyone read acces to the test certificates is because this allows us to run the backend without the need for sudo. Allowing us to automate steps in development.

```bash
sudo mkdir -p /etc/ssl/testcerts
sudo openssl req -new -x509 -days 365 -nodes -out /etc/ssl/testcerts/ca.pem -keyout /etc/ssl/testcerts/ca.key
sudo chmod 604 /etc/ssl/testcerts/ca*
```

## Backend Build / Run

Within the backed folder, you first have to copy ".env.template" as ".env" in the same folder. After that you have to change the values within ".env" to represent your environment.

```bash
# Server Communication Ports
PortHTTP=:8080  # Port 8080 is the standard development port for HTTP
PortHTTPS=:4443 # Port 4443 is the standard development port for HTTPS

# TLS Certificate Paths
CertFilePath=   # /etc/ssl/testcerts/ca.pem (When following the OpenSSL example)
KeyFilePath=    # /etc/ssl/testcerts/ca.key (When following the OpenSSL example)
```

The commands underneath are simply to build and execute the backend. It is important to first go to the project folder "vrijtap".

```bash
cd src/backend
go build -o bin/backend cmd/main.go
./bin/backend
```

Note that you need to execute the backend with sudo when you're using root protected ca certificates and/or root protected ports (such as port 80 and 443).

## Installing Air

Air is the automated compile and execute platform for golang. By using air we can achieve the same as we can with nodemon (except we don't need to install a javascript environment to run it). When using air, changes in files get detected automatically and this signals air to refresh the server build.

```bash
go install github.com/cosmtrek/air@latest
```

Now you can try if the environment work by going to the project folder and using the command.

```bash
cd ~/vrijtap/src/backend
air
```

In the case that it does not work, try again after running the following command.

```bash
sudo mv ~/go/bin/air /usr/local/bin
```
