# RocketChat Installation
1. Adding official rocketchat helm 
```
helm repo add rocketchat https://rocketchat.github.io/helm-charts
```
2. installing rocket chat with value. Check the value file in RocketChat Folder.
```
helm install myrocketchat -f Values.yaml rocketchat/rocketchat
```
