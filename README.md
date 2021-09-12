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

## Debian
1. apt update and installation
```
sudo apt update
sudo apt install git
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
8. Start and SSH into the container, good for *debug* and *develop* Dockerfile  
```
docker start -a -i 912176b700a38fb0eaadee778f217030e4acf23066688c8d262d71a5d834b9e0
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
7. Get log of a Pod
```shell
# Log
k logs pod-a7x0gafg --namespace staging

# Tail the log and grep
k logs --follow ghost-proxy-5496664987-qmbvh --namespace prod | grep 'chicken'
```

## Spinnaker
1. For anyone that wants to have the old spinnaker capabilities back (basically, being able to rollback a deployment from the UI), we can use a little hack. Go to your browsers console, and set:
```
window.spinnakerSettings.kubernetesAdHocInfraWritesEnabled = true;
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

2. Bucket: Upload files to a Bucket Folder
```
gsutil cp ./build/main.js gs://cdn/dir/
```

3. Bucket: Add allUsers (public Internet) access to a file
```
gsutil acl ch -u AllUsers:R gs://cdn/dir/main.js
```

4. Bucket: Add metadata to a Bucket file
```
gsutil setmeta -h "cache-control:max-age=0" gs://cdn/dir/main.js
```

5. Bucket: Get stats of a Bucket file
```
gsutil stat gs://BUCKET_NAME/OBJECT_NAME
```

## Helm
1. Start Helm client
```
export HELM_HOST=:44134 
helm init --client-only             
```

## Tiller Server
```
export TILLER_NAMESPACE=tiller 
tiller -listen=localhost:44134 -storage=secret -logtostderr
```

## Utils
1. Tail log real-time
```
tail -f output.log
```

## NPM / YARN
1. Upgrade Yarn
```
npm upgrade --global yarn 
```

2. See why dependency exists
```
yarn why <package>
```


## MongoDB
1. Connection URI
```
mongodb://<username>:<password>@<hosts>:<port>/<database>?authSource=<authDatabase>
```
2. Aggregate Query:
```
db.getCollection('customerjourneys').aggregate(
    [{
        $group : {
            _id : { month: { $month: "$createdAt" }, day: { $dayOfMonth: "$createdAt" }, year: { $year: "$createdAt" } },
            dailyEvents: { $sum: 1 }
                }
            }
    ] )
```

## SDKMan
1. List SDKs
```
sdk list java
```

2. Install SDKs
```
sdk install java 8.0.252.hs-adpt
```

## Flutter
1. Switch Flutter version:
```
flutter channel <env>
```
2. Build Android 
```
flutter bundle
```
3. Build iOS (Release & No Codesign)
```
flutter build ios --release --no-codesign
```
4. Flutter Upgrade
```
flutter upgrade
```
5. Flutter Clean
```
flutter clean
```
6. Flutter Run
```
flutter run -d <deviceId>
```
7. Flutter Code Gen - build part file (w/o deletion of existing files)
```
flutter pub run build_runner build
flutter packages pub run build_runner watch --delete-conflicting-outputs
```
8. Flutter Code Gen - translate Intl messages in Dart to arb files
```
flutter pub run intl_translation:extract_to_arb --output-dir=assets/intl ./lib/**/*.dart
```

# Database
## Cassandra
1. Alter Keyspace replication (for local)
```cql
ALTER KEYSPACE message WITH REPLICATION = { 'class' : 'org.apache.cassandra.locator.SimpleStrategy', 'replication_factor': '1' };
```

# Android
## ADB
1. Send SMS
```shell
adb emu sms send <sender> <msg>
```
