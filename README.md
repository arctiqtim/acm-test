# Deploy from this repo

On the GKEOP Primary cluster

```shell
kubectl create secret generic git-creds \
--namespace=config-management-system \
--from-file=ssh=/path/to/[KEYPAIR-PRIVATE-KEY-FILENAME]

kubectl apply -f - <<EOF
apiVersion: addons.sigs.k8s.io/v1alpha1
kind: ConfigManagement
metadata:
  name: config-management
spec:
  clusterName: sandbox-user-cluster1
  git:
    syncRepo: git@github.com:arctiqteam/t-anthos.git
    syncBranch: master
    secretType: ssh
EOF
```

On the GKE Remote 1 cluster

```shell
kubectl apply -f - <<EOF
apiVersion: addons.sigs.k8s.io/v1alpha1
kind: ConfigManagement
metadata:
  name: config-management
spec:
  clusterName: hipster-canada
  git:
    syncRepo: git@github.com:arctiqteam/t-anthos.git
    syncBranch: master
    secretType: ssh
    policyDir: "acm-hipster-demo"
EOF
```

On the GKE Remote 2 cluster

```shell
kubectl apply -f - <<EOF
apiVersion: addons.sigs.k8s.io/v1alpha1
kind: ConfigManagement
metadata:
  name: config-management
spec:
  clusterName: hipster-usa
  git:
    syncRepo: git@github.com:arctiqteam/t-anthos.git
    syncBranch: kyledemo
    secretType: ssh
    policyDir: "acm-hipster-demo"
EOF
```
