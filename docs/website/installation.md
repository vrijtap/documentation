# Installation

This page contains the entire installation of the website and what is needed to run the website in its current state. If the installation guide does not perform as expected, you could try to use a newer version. This installation is specifically targeted towards the Raspberry Pi 3.

## Installing Prerequisites

```bash
sudo apt update
sudo apt upgrade
sudo apt install git
```

## Installing Go

Fetch, install and delete the Installation Files.

```bash
wget https://go.dev/dl/go1.21.4.linux-arm64.tar.gz
sudo tar -C /usr/local -xzf go1.21.4.linux-arm64.tar.gz
rm go1.21.4.linux-arm64.tar.gz
```

Enter the profile config to configure the GO path.

```bash
nano ~/.profile

# Add to the bottom of the file and save (with CTRL+X and then select Y):
PATH=$PATH:/usr/local/go/bin
GOPATH=$HOME/go
```

Refresh the .profile file and check if go was installed succesfully.

```bash
source ~/.profile
go version
```

## Fetching the dev-payment-gate

```bash
cd ~/
git clone https://github.com/vrijtap/dev-payment-gate.git
cd ~/dev-payment-gate
```

## Fetching the website Repository

```bash
cd ~/
git clone https://github.com/vrijtap/website.git
cd ~/website
```

## Run dev-payment-gate (development)

When you are running a development instance of the website, you might want to use our fake payment server to simulate purchases. To do this, you can copy '.env.template' as '.env' and fill in all of the information requested.

```bash
cd ~/dev-payment-gate
cp .env.template .env
nano .env
```

Here is how you can set it up:

```bash
# Server Communication
MONGO_URI= # [The key to your personal mongodb environment]

# HTTP Information
PORT="9090"

# API key for using this server
API_KEY="dev-payment-gate-key"
```

The command underneath starts the payment gate locally.

```bash
cd ~/dev-payment-gate
go run cmd/main.go
```

## Run website

After installing all of the prerequisites and go and fetching the github repository, you can copy '.env.template' as '.env' and fill in all of the information requested.

```bash
cd ~/website
cp .env.template .env
nano .env
```

Here is how you can set it up for development:

```bash
# Environment
ENVIRONMENT="development"

# HTTP Information (development)
PORT_HTTP="8080"

# HTTPS Information (production)
PORT_HTTPS="4443"
PATH_CERT_FILE=
PATH_KEY_FILE=

# Server Communication
MONGO_URI= # [The key to your personal mongodb environment]

# Server Secrets
SERVER_SECRET="secret"
PASSWORD_DEFAULT="default"

# Payment Gate Information
PAYMENT_GATE_URL="http://raspberry:9090/transaction"
PAYMENT_GATE_KEY="dev-payment-gate-key"
WEBHOOK_KEY="website-webhook-key"

# Information
NAME="Test Bar"
PRICE="2.95"
```

The command underneath starts the website locally.

```bash
cd ~/website
go run cmd/main.go
```
