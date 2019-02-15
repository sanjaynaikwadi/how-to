# How to intall GitLab CE on Ubuntu 18.0.4

### Enviornment
- Google cloud instance
- Ubuntu 18.0.4 LTS version
- Instance 2 vcpu + 7.5 GB Ram recommended
- Storage disk atleat 50GB recommended

### Installing the Dependencies
Lets install the required dependencies before installing gitlab

```bash
sudo apt update
sudo apt install ca-certificates curl openssh-server
```

### Installing GitLab
Now that the dependencies are in place, we can install GitLab itself


```bash
cd /tmp
curl -LO https://packages.gitlab.com/install/repositories/gitlab/gitlab-ce/script.deb.sh
sudo bash /tmp/script.deb.sh
```
This will setup the required respository and now we can proceed to install gitlab

```bash
sudo apt install gitlab-ce
```
This will install all required software on the system.

### Firewall Rules
Check if you have firewall running, if `YES` then you need to allow few ports in firewall

```bash
sudo ufw status
```
If you get status `Inactive` then you can skip this step. If its enable then run the following commands to allow 

```bash
sudo ufw allow http
sudo ufw allow https
sudo ufw allow OpenSSH
```

### GitLab Configuration File

Edit the file and set the `external_url` to you domain, also enable the letsencrpyt which will generate the SSL and you can have a valid cert for your gitlab

```bash
sudo vim /etc/gitlab/gitlab.rb

external_url 'https://gitlab.example.com'
letsencrypt['enable'] = true
letsencrypt['contact_emails'] = ['abc@example.com'] # This should be an array of email addresses to add as contacts

```

Reconfigure the gitlab
```
sudo gitlab-ctl reconfigure
```

`NOTE` - Make sure you make the proper entry in you DNS to point to gitlab URL whatever you would be setting or else your letsencrypt will fail.

### Configuration Through the Web Interface

Login to your gitlab URL and set the password, default user is `root`.

Your set now to create projects/users/groups and assign persmissions accordingly.

### Optional/Additional configuration
- Disable Signup
- Changes existing user account details
- Domain blacklist







