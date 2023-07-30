# easun-inverter-monitoring
Simple monitoring for EaSunPower hybrid solar 2.4kW inverter over RS232

I'm not sure how true this is, but the documentation for the inverter communication protocol that I found on the net is very similar to what works.

curl -L "https://github.com/docker/compose/releases/latest/download/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
chmod +x /usr/local/bin/docker-compose
usermod -aG docker $USER
git clone https://github.com/temik4/easun-inverter-monitoring.git
docker-compose up -d

for trublshuting you can run app in console and get metrics on port 8000 (http://ip:8000/metrics)
make deps
make ENV=.env
source .env/bin/activate
python -m easun_monitoring.app
