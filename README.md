# Deploy from this repo

On the GKEOP cluster

```shell
kubectl create secret generic git-creds \
--namespace=config-management-system \
--from-file=ssh=/path/to/[KEYPAIR-PRIVATE-KEY-FILENAME]

kubectl apply -f - <<EOF
apiVersion: configmanagement.gke.io/v1
kind: ConfigManagement
metadata:
  name: config-management
spec:
  clusterName: arctiqtim
  git:
    syncRepo: git@github.com:arctiqtim/acm-test.git
    syncBranch: master
    secretType: none
EOF
```
