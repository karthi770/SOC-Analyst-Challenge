# SOC Analyst Challenge

## Day - 1 - Schematic diagram
![Untitled Diagram](https://github.com/user-attachments/assets/d5285388-57e1-490c-a300-d90b0f3330a4)
## Day - 2 - Introduction to ELK slack
![image](https://github.com/user-attachments/assets/c184f051-c057-435a-9b6b-6f680619d83e)
![image](https://github.com/user-attachments/assets/bf5f5252-595a-4933-bf0b-420226743bc9)
![image](https://github.com/user-attachments/assets/4b9b4f25-d5b7-45fd-a476-52f7d1751c6f)
![image](https://github.com/user-attachments/assets/dd185454-ff6c-404b-aecf-3a8610d2d1cd)


## Day - 3 - Elasticsearch Setup
![image](https://github.com/user-attachments/assets/079e2c41-dd59-4bb8-84f1-6974ee9f0346)
![image](https://github.com/user-attachments/assets/e289fc10-e8fd-4a5c-b027-e1034902a25c)

Now add a droplet in the VPC:
![image](https://github.com/user-attachments/assets/647f9d64-ecfb-44d8-a6be-1f6b0410edac)
![image](https://github.com/user-attachments/assets/081fc850-055c-454c-a162-5ebefb3cdfee)
![image](https://github.com/user-attachments/assets/4ee42b33-adb8-4b7b-86ec-9b68585d4753)
![image](https://github.com/user-attachments/assets/980d4bcc-2fcb-4e70-af10-9377d0670925)

Refer this doc to generate the rsa key and use it in the Digital ocean account, add the SSH key and then continue:
![image](https://github.com/user-attachments/assets/2bb911ac-7c13-4361-863a-431373da7f38)

![image](https://github.com/user-attachments/assets/1a7f5e64-9beb-4efb-bf84-7521584ddf4e)

SSH into the Droplet
![image](https://github.com/user-attachments/assets/e0ae97a7-2774-44d1-95c0-0bd32f994711)

Steps to follow to ssh in to droplet.
- As mentioned in the previous step generate the SSH key.
- Now enter the console of the Droplet and enter into active  `echo [publickey] >> ~/.ssh/authorized_keys` this command will add the public key to the authorized key file.
- Now in the local PC make sure to save the private key to be save in `~/.ssh` folder, also make sure the file it .pem if it is in .ppk follow the steps:
	- `sudo apt-get install putty-tools`
	- ` puttygen ~/.ssh/SOC_analyst_digital_ocean.ppk -O private-openssh -o ~/.ssh/SOC_analyst_digital_ocean.pem`
- Now go to the local computer and open bash
- `ssh -i ~/.ssh/SOC_analyst_digital_ocean.pem root@143.198.39.218`
- This will ssh into the remote SOC PC but during the process this shall ask for the passphrase which we created during the key generation.

Now inside the SOC PC terminal:

`apt-get update && apt-get upgrade -y`

![image](https://github.com/user-attachments/assets/664fd4cf-395c-4f63-87dd-8c0786274d18)

`wget https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-8.15.3-amd64.deb`

`dpkg -i elasticsearch[tab]`

```
--------------------------- Security autoconfiguration information ------------------------------
Authentication and authorization are enabled.
TLS for the transport and HTTP layers is enabled and configured.
The generated password for the elastic built-in superuser is : d-b-P8UVi4f54+QqH-*Y
If this node should join an existing cluster, you can reconfigure this with
'/usr/share/elasticsearch/bin/elasticsearch-reconfigure-node --enrollment-token <token-here>'
after creating an enrollment token on your existing cluster.
You can complete the following actions at any time:
Reset the password of the elastic built-in superuser with
'/usr/share/elasticsearch/bin/elasticsearch-reset-password -u elastic'.
Generate an enrollment token for Kibana instances with
 '/usr/share/elasticsearch/bin/elasticsearch-create-enrollment-token -s kibana'.
Generate an enrollment token for Elasticsearch nodes with
'/usr/share/elasticsearch/bin/elasticsearch-create-enrollment-token -s node'.
```

`ip address` get the public IP and paste it in the  `elasticsearch.yml`

`cd /etc/elasticsearch` and open `elasticsearch.yml`

`nano elasticsearch.yml`

![image](https://github.com/user-attachments/assets/f021225a-21ce-40eb-886b-1f1d43843cb2)
Change the public IP address to SOC analyst PC ip address and then the http port. This will allow the SOC PC to access the elasticsearch instance.


![image](https://github.com/user-attachments/assets/39a6a077-8c5a-462f-bf59-cd94603feddf)
Update the fire wall rules. Change the inbound rules to SSH and ip of the SOC PC.

`systemctl daemon-reload`
`systemctl enable elasticsearch.service`
`systemctl start elasticsearch.service`
`systemctl status elasticsearch.service`



