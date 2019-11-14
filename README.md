# 🚀John's awesome zsh

## ZSH
1. Edit my alias file
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

## Linux / Unix
1. Restart service (NGINX example)
```
service nginx start
service nginx stop
service nginx reload
```
2. Kill process by port
```
kill $(lsof -t -i:4000) 
```
3. Default dir
```
cd /etc/nginx
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
4. Remove dangling images
```
docker image prune
```
5. Remove image
```
docker image rm zenbot_server --force // force
```
6. Build image with args
```
docker build --build-arg SSH_PRIVATE_KEY="$(cat ./bucket_privatekey)" --build-arg SSH_PUBLIC_KEY="$(cat ./bucket_pubkey)" -t go-socket-io .
```
7. Run an image with ENV variables; port forward
```
docker run --rm -p 3000:3000 -e "RAILS_ENV=staging" my-rails-app:latest
```

## Kubernetes 
Note: I use `k` as an alias of `kubectl`
1. List all pods in the namespace, with more details (thanks ❤️ [@chhetripradeep](https://github.com/chhetripradeep))
```
k get pods -o wide --namespace staging
k get pods -o wide --all-namespaces
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
6. AWS EKS aws-auth configmap
```
kubectl -n kube-system describe configmap aws-auth
```

## AWS
1. [Named Profile](https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-profiles.html)
```
export AWS_PROFILE=johnhandsome // custom profile
export AWS_PROFILE=default // default profile
```
2. Config kubectl profile
```
aws eks update-kubeconfig --name xxx-cluster-v2
```

## GCP
1. Config kubectl profile
```
gcloud container clusters get-credentials qa-cluster-2 --zone=asia-southeast1
```

## Tiller Server
```
export TILLER_NAMESPACE=tiller 
tiller -listen=localhost:44134 -storage=secret -logtostderr
```

