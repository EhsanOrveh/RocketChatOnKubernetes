# About
This is a guide to running a rocketchat with jitsi as a full function chat solution.
## K8S environment
1. RKE Cluster with three node added to rancher.
2. Single rancher node has been ran as a single container on docker.
3. Nginx ingress
4. Metlallb as a L2 loadbalancer
5. Longhorn as a storage provider
6. Helm
## Note
In this repo you can find minimum configuration you need to setup service. for complete guide please check official github [RocketChat](https://github.com/RocketChat/Rocket.Chat) and [Jitsi](https://github.com/jitsi-contrib/jitsi-helm/tree/main).
## Free ssl certificate - Letsencrypte
The modern browsers do not allow you to use webcame/microphone without valid ssl/https.
1. I have used [certbot](https://certbot.eff.org/) to generating valid free ssl from lets's encrypt. This [guid](https://www.digitalocean.com/community/tutorials/how-to-acquire-a-let-s-encrypt-certificate-using-dns-validation-with-acme-dns-certbot-on-ubuntu-18-04) from digitalocean can help you completely.
### Step 1 — Installing Certbot
```
sudo apt-add-repository ppa:certbot/certbot
sudo apt install certbot
certbot --version
```
### Step 2 — Installing acme-dns-certbot
```
wget https://github.com/joohoi/acme-dns-certbot-joohoi/raw/master/acme-dns-auth.py
chmod +x acme-dns-auth.py
nano acme-dns-auth.py
```
Add a 3 to the end of the first line:
#!/usr/bin/env python3
```
sudo mv acme-dns-auth.py /etc/letsencrypt/
```
### Step 3 — Setting Up acme-dns-certbot
```
sudo certbot certonly --manual --manual-auth-hook /etc/letsencrypt/acme-dns-auth.py --preferred-challenges dns --debug-challenges -d chat.your-domain
```
You use the --manual argument to disable all of the automated integration features of Certbot. In this case you’re just issuing a raw certificate, rather than automatically installing it on a service as well.
You configure Certbot to use the acme-dns-certbot hook via the --manual-auth-hook argument. You run the --preferred-challenges argument so that Certbot will give preference to DNS validation.
You must also tell Certbot to pause before attempting to validate the certificate, which you do with the --debug-challenges argument. This is to allow you to set the DNS CNAME record(s) required by acme-dns-certbot. Without the --debug-challenges argument, Certbot wouldn’t pause, so you wouldn’t have time to make the required DNS change.
