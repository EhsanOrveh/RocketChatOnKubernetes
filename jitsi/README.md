# jitsi Installation
1. Adding official rocketchat helm 
```
helm repo add jitsi https://jitsi-contrib.github.io/jitsi-helm/
```
2. installing rocket chat with value.
```
helm install myjitsi jitsi/jitsi-meet -f value.yml
```
