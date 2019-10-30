# 🚀John's awesome zsh

## ZSH
1. Change dir to `$ZSH_CUSTOM`
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

## Docker
1. Build Docker image and assign tag to $IMAGE_ID
```
IMAGE_ID=$(docker build -t go-socket-io . -q)
```
2. Tag Docker Image with variable $IMAGE_ID
```
docker tag "$IMAGE_ID" xxxxxx.dkr.ecr.ap-northeast-1.amazonaws.com/go-socket-io
```
3. Push Docker image
```
docker push xxxxxx.dkr.ecr.ap-northeast-1.amazonaws.com/go-socket-io
```

## Kubernetes
1. List all pods in the namespace, with more details (thanks @chhetripradeep)
```
k get pods -o wide --namespace staging
```
2. Delete resources from config yaml
```
k delete -f deployment.yaml
```
3. Delete pods by label `k8s-app`
```
k delete pods -l k8s-app=go-socket-io --namespace staging      
```
4. Get ELB host of a service
```
export ELB=$(kubectl get svc -n grafana grafana -o jsonpath='{.status.loadBalancer.ingress[0].hostname}')
echo "http://$ELB"
```
5. AWS EKS secret
```
kubectl -n kube-system describe secret $(kubectl -n kube-system get secret | grep eks-admin | awk '{print $1}')
```

## AWS [Named Profile](https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-profiles.html)
```
export AWS_PROFILE=hashnest // custom profile
export AWS_PROFILE=default // default profile
```

## Tiller Server
```
export TILLER_NAMESPACE=tiller 
tiller -listen=localhost:44134 -storage=secret -logtostderr
```

