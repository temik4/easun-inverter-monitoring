# EaSunPower inverter monitoring

## Table of Contents

- [About](#about)
- [Getting Started](#getting_started)
- [Troubleshooting](#troubleshooting)
- [Usage](#usage)

## About <a name = "about"></a>
Simple monitoring for <a href="https://www.easunpower.com/products/easun-power-pwm-3kva-2400w-24v-solar-inverter-off-grid-hybrid-220v-80a-charging-current" target="_blank">EaSunPower hybrid solar 2.4kW</a> inverter over RS232

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
cd easun-inverter-monitoring
docker-compose up -d
```

### Troubleshooting <a name = "troubleshooting"></a>

In my particular case, the USB-RS232 adapter was used, which was defined as ```/dev/ttyUSB0``` in the system.</br>
If your case is different, then you should make the necessary changes in the [app.py](easun_monitoring/app.py) file in this part of the code:

```
def get_inverter() -> Inverter:
    global _inverter
    if _inverter is None:
        _inverter = Inverter('/dev/ttyUSB0')
    return _inverter
```

For troubleshooting and development purposes, you can run the application in the console and get the metrics on port 8000 (```http://yourServerIP:8000/metrics```) without having to run docker containers: 

```
python -m venv .env
source .env/bin/activate
make deps
make ENV=.env
source .env/bin/activate
python -m easun_monitoring.app
```


## Usage <a name = "usage"></a>

After running the application, you should make sure that all the required docker containers (prometheus, grafana and easun_monitoring) are running.</br>
If everything went well, you will be able to access the Grafana dashboard at the link:</br> ```http://yourServerIP:3000/d/l2a2zy04k/power-monitoring?orgId=1```</br>
You can find the Grafana credentials in the [config.monitoring file](grafana/config.monitoring)
