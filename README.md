# Shiori

Test shiori with talos and local-path-provisioner.

```sh
talosctl cluster create

# https://www.talos.dev/v1.8/kubernetes-guides/configuration/local-storage/#local-path-provisioner
cd storage
kustomize build | kubectl apply -f -

# create a PersistentVolumeClaim named local-path-pvc
kubectl create -f https://raw.githubusercontent.com/rancher/local-path-provisioner/master/examples/pvc/pvc.yaml

# https://github.com/go-shiori/shiori/blob/master/docs/Installation.md#using-kubernetes-manifests
kubectl apply -f shiori.yaml

kubectl port-forward svc/shiori 8088:8080

# check the PV
kubectl apply -f pv-inspector.yaml
kubectl exec -it pv-inspector -- ls -la /data

total 80
drwxrwxrwx    2 root     root          4096 Oct 28 19:10 .
drwxr-xr-x    1 root     root          4096 Oct 28 19:17 ..
-rw-r--r--    1 1000     1000         73728 Oct 28 19:10 shiori.db
```
