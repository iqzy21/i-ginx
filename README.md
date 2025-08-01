# i-ginx - An Nginx Website
## http://nginx.iqbaal.uk/ 
This is a mini project i did to reinforce my learning about networking.

## Step 1: Domain Purchase

Firstly i purchased a domain from cloudflare

![Domain Purchase](https://github.com/user-attachments/assets/02492801-a368-4825-bcdf-735921dc6731)

## Step 2: EC2 Instance Setup

Secondly i created a ec2 instance with AWS and set it up in linux

![EC2 Instance Setup](https://github.com/user-attachments/assets/49e8d8b7-5384-467b-aa4d-96c9ceb6662f)

## Step 3: Nginx Installation

Thirdly i used the SSH command to go into my ec2 instance and downloaded nginx which a web server package for hosting websites on an operating system

### Commands Used:

- `sudo apt install nginx -y` - this command installs nginx
- `sudo systemctl start nginx` - this command starts nginx and lets it listen on port 80 for any website set ups
- `sudo systemctl enable nginx` - this allows nginx to start when the ec2 starts
- `sudo systemctl status nginx` - and this checks if nginx is up and running You should see a green "active (running)" message.

![Nginx Status](https://github.com/user-attachments/assets/627e2291-5d49-4345-9812-c881900656c2)

## Step 4: DNS Configuration

After that i then copied the IPV4 from the aws instance then used it to created a dns with cloudflares dns records so that my site can be access through a name instead of the ip

![DNS Records](https://github.com/user-attachments/assets/d302a982-8ce2-4efc-bac0-9495610eed23)

## Step 5: Initial Testing and Problem Discovery

After that i decided to test my website and see if it would load and was working however i ran into an issue where the site would not load

![Website Not Loading](https://github.com/user-attachments/assets/0c692b83-8907-4ae5-9d92-0022262f72ed)

### Initial Troubleshooting Steps:

1. **Check for spelling errors** - there was none
2. **Verify cloudflare domain settings** - everything checked out
3. **Test nginx status** - used `sudo systemctl status nginx` and status was up and running

## Step 6: Advanced Troubleshooting

After that to troubleshoot why my website would not load i used 3 commands:

- **ping** - The ping command is used to test connectivity between devices and servers
- **dig** - is an advance query tool and provides more information than nslookup
- **nslookup** - Nslookup is a tool to query dns or website

### Diagnostic Results:

After using these commands to diagnose the situation i noticed they all outputted similar messages:

- **ping** returned - "Name or service not known," suggesting a DNS resolution failure.
- **dig** returned - NXDOMAIN meaning the domain doesn't exist in the DNS records.
- **nslookup** also returned - NXDOMAIN, verifying the domain couldn't be resolved by the DNS server.

![Troubleshooting Commands](https://github.com/user-attachments/assets/3c6f1a7d-7b09-4321-9265-5201ceb77a51)

## Step 7: Root Cause Analysis

These tests helped me identify that the root issue is to do with the dns. What i did was after refer back to my notes i have been making while learning networking and came across a note i made about ports:

> Ports are like logical doors for a device each door is numbered and each number is used for a specific type of network communication. For example when traffic goes through port 80 which IS HTTP and 443 which is HTTPS.

After reading this it started to come to me as i was having the same issue about the website not opening and then i decided to check about port 80.

After that i searched up issues regarding port 80 in ec2 and came across this:
https://repost.aws/questions/QULEJ7laChQEOgIf-iPyBZBQ/my-ec2-is-not-responding-from-browser-ec2-intance-connect-or-a-web-server-on-port-80

And low and behold i found my answer:

![AWS Solution](https://github.com/user-attachments/assets/5b233b71-5eb7-4364-9c32-0d1222b999cf)

## Step 8: Security Group Configuration

So i went to ec2 security and seen that there was no port for inbound port for 80/HTTP after finding this out i created my port

![Security Group Configuration](https://github.com/user-attachments/assets/664ca12b-3941-452d-9564-0d177be41291)

## Step 9: Problem Resolution

After creating my port and waiting for around 1 minute i went to load the website and it loaded

![Website Working](https://github.com/user-attachments/assets/26bfbd86-3e4f-41a1-9fb0-e28244c5b1c0)

## Step 10: Website Customization

I was happy that i managed to solve this problem and went a bit further to design my page by going into the var/www/html file and submitting html code to style the page into this

<img width="1914" height="1029" alt="Screenshot 2025-08-01 132535" src="https://github.com/user-attachments/assets/fae15627-e791-4d05-a20a-8a8356ac62e7" />

Here is the website after the customisation

![Customized Website](https://github.com/user-attachments/assets/5e0de35f-25e3-4923-8704-25a553ff27f4)


## Step 11: Git Deployment
I then decided to create this repo on github/git to show my work and my website 
in this image you can see me staging and commiting the index.html file for my nginx website
<img width="1097" height="452" alt="Screenshot 2025-08-01 134422" src="https://github.com/user-attachments/assets/9850041b-f147-41c7-af75-6025954b17c8" />

after that I did the samething again and updated the code within the index.html file 
<img width="1081" height="401" alt="image" src="https://github.com/user-attachments/assets/66a2bc98-52db-49b4-ad64-f63fb10b46bf" />

and now you can see this on my github repo :)

## Conclusion

Overall im happy with how this project turned out and gave me the opportunity to be hands on a solve a real world problem!

## Key Learnings

- **DNS Configuration**: Understanding how to properly set up DNS records to map domain names to IP addresses
- **Security Groups**: Learning that AWS EC2 instances require proper inbound rules for HTTP traffic on port 80
- **Troubleshooting Methods**: Using `ping`, `dig`, and `nslookup` commands to diagnose network connectivity issues
- **Nginx Configuration**: Setting up and managing a web server on Linux
- **Problem-Solving Process**: Systematic approach to identifying and resolving network-related issues
