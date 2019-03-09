# lightsail-openvpn-as
Run OpenVPN-AS on Amazon Lightsail with Duck DNS

## edit config
edit the following lines in `user-data.txt` 
```
EMAIL=example@mail.com
URL=example.duckns.org
TOKEN=duck-dns-token
TZ=Europe/Brussels
```

## create instance
Create AWS Lightsail instance via [AWS Lightsail CLI](https://docs.aws.amazon.com/cli/latest/reference/lightsail/index.html "AWS Lightsail CLI")
```
aws lightsail create-instances --instance-names "lightsail-eu-central-vm" --availability-zone eu-central-1a --blueprint-id centos_7_1805_01 --bundle-id nano_2_0 --user-data file://ud.txt
```
You can find the script in `/var/lib/cloud/instance/user-data.txt` on the instance

## configure instance - open ports
```
aws lightsail open-instance-public-ports --port-info fromPort=443,toPort=443,protocol=TCP --instance-name lightsail-eu-central-vm
aws lightsail open-instance-public-ports --port-info fromPort=1194,toPort=1194,protocol=UDP --instance-name lightsail-eu-central-vm
```

