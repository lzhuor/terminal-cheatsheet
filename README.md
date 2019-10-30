# 🚀John's awesome zsh

## ZSH
1. Change dir to $ZSH_CUSTOM
```
cd $ZSH_CUSTOM
```
2. Edit alias file
```
 vim $ZSH_CUSTOM/aliases.zsh 
```
## SSH
1. SSH
```
ssh -i private-key.pem ubuntu@1.1.1.1 
```
2. Copy file from remote SSH to local
```
scp -i private-key.pem ubuntu@1.1.1.1:server.log /Desktop/dev
```

## Kubernetes
1. List all pods in the namespace, with more details 
```
k get pods -o wide --namespace staging
```
2. Delete resources from config yaml
```

```
3. Delete pods by label `k8s-app`
```
k delete pods -l k8s-app=go-socket-io --namespace hashnest-staging      
```
