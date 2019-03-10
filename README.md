# lightsail-openvpn-as
Run OpenVPN-AS on Amazon Lightsail with Duck DNS

## Edit config
Edit the following lines in `user-data.txt` 
```
EMAIL=example@mail.com
URL=example.duckns.org
TOKEN=duck-dns-token
TZ=Europe/Brussels
```

## Create instance
Create AWS Lightsail instance via [AWS Lightsail CLI](https://docs.aws.amazon.com/cli/latest/reference/lightsail/index.html "AWS Lightsail CLI")
```
aws lightsail create-instances --instance-names "lightsail-eu-central-vm" --availability-zone eu-central-1a --blueprint-id centos_7_1805_01 --bundle-id nano_2_0 --user-data file://user-data.txt
```
You can find the script in `/var/lib/cloud/instance/user-data.txt` on the instance

## Configure instance - open ports
```
aws lightsail open-instance-public-ports --port-info fromPort=443,toPort=443,protocol=TCP --instance-name lightsail-eu-central-vm
aws lightsail open-instance-public-ports --port-info fromPort=1194,toPort=1194,protocol=UDP --instance-name lightsail-eu-central-vm
```

## Application Setup
The admin interface is available at ` https://yoursubdomain.duckdns.org/admin` with a default user/password of admin/password

hostname:
```
yoursubdomain.duckdns.org
```

dynamic IP address network:
```
10.0.0.0/20
```

routing using NAT:
```
10.0.0.0/20
172.20.0.0/16 - app_net subnet in docker-compose
```

DNS by Google
```
primary: 8.8.8.8
secondary: 8.8.4.4
```

## Aftercare
Download the key file [here](https://lightsail.aws.amazon.com/ls/webapp/account/keys "AWS Lightsail keys")
```
chmod 600 LightsailDefaultKey-eu-central-1.pem 
```
Obtain the public IP
```
aws lightsail get-instance --instance-name lightsail-eu-central-vm | grep publicIpAddress
```
Login to your instance
```
ssh -i LightsailDefaultKey-eu-central-1.pem  centos@PUBLIC_IP
```
