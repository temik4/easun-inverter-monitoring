# EaSunPower inverter monitoring

## Table of Contents

- [About](#about)
- [Getting Started](#getting_started)
- [Usage](#usage)

## About <a name = "about"></a>
Simple monitoring for EaSunPower hybrid solar 2.4kW inverter over RS232

I'm not sure how true this is, but the [documentation for the inverter communication protocol](HS_MS_MSX_RS232_Protocol_20140822_after_current_upgrade.pdf) that I found on the net is very similar to what works.

## Getting Started <a name = "getting_started"></a>

These instructions will help you copy and run a copy of the project on your local computer for development, testing, or use purposes.

### Prerequisites

Here is what you need to install the software (skip this step if you already have docker-compose installed):

```
curl -L "https://github.com/docker/compose/releases/latest/download/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
chmod +x /usr/local/bin/docker-compose
usermod -aG docker $USER
```

### Installing

A step-by-step series of commands that will allow you to run the application:

```
git clone https://github.com/temik4/easun-inverter-monitoring.git
docker-compose up -d
```

for trublshuting you can run app in console and get metrics on port 8000 (http://ip:8000/metrics)

```
make deps
make ENV=.env
source .env/bin/activate
python -m easun_monitoring.app
```


## Usage <a name = "usage"></a>

After running the application, you should make sure that all the required docker containers (prometheus, grafana and easun_monitoring) are running.</br>
If everything went well, you will be able to access the Grafana dashboard at the link: http://yourServerIP:3000/d/l2a2zy04k/power-monitoring?orgId=1
You can find the credentials in the [config.monitoring file](grafana/config.monitoring)