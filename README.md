# lightsail-openvpn-as
Run OpenVPN-AS on Amazon Lightsail

Create AWS Lightsail instance via [AWS Lightsail CLI](https://docs.aws.amazon.com/cli/latest/reference/lightsail/index.html "AWS Lightsail CLI")
```
aws lightsail create-instances --instance-names "lightsail-eu-central-vm" --availability-zone eu-central-1a --blueprint-id centos_7_1805_01 --bundle-id nano_2_0 --user-data file://ud.txt
```

You can find the script in `/var/lib/cloud/instance/user-data.txt` on the instance


