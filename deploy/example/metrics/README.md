# Get Prometheus metrics from CSI driver

1. Create `csi-blobfuse-controller` service with targetPort `29624`
```console
kubectl apply -f https://raw.githubusercontent.com/kubernetes-sigs/blobfuse-csi-driver/master/deploy/example/metrics/csi-blobfuse-controller-svc.yaml
```

2. Get ClusterIP of service `csi-blobfuse-controller`
```console
$ kubectl get svc csi-blobfuse-controller -n kube-system
NAME                       TYPE        CLUSTER-IP   EXTERNAL-IP   PORT(S)     AGE
csi-blobfuse-controller   ClusterIP   10.0.156.8   <none>        29624/TCP   32m
```

3. Run following command to get cloudprovider_azure metrics
```console
curl http://{CLUSTER-IP}:29624/metrics | grep cloudprovider_azure
```