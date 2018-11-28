# Kubernetes

Run on all hosts:

```
$ sudo su -
# curl --silent https://packages.cloud.google.com/apt/doc/apt-key.gpg | apt-key add -
# echo "deb http://apt.kubernetes.io/ kubernetes-xenial main" > /etc/apt/sources.list.d/kubernetes.list
# apt-get -qq update
# apt-get -qq install --yes kubeadm
# exit
```

Run on master:

```
$ sudo kubeadm init --pod-network-cidr 10.244.0.0/16
```

Output:

```
[init] using Kubernetes version: v1.12.3
[preflight] running pre-flight checks
        [WARNING SystemVerification]: this Docker version is not on the list of validated versions: 18.04.0-ce. Latest validated version: 18.06
[preflight/images] Pulling images required for setting up a Kubernetes cluster
[preflight/images] This might take a minute or two, depending on the speed of your internet connection
[preflight/images] You can also perform this action in beforehand using 'kubeadm config images pull'
[kubelet] Writing kubelet environment file with flags to file "/var/lib/kubelet/kubeadm-flags.env"
[kubelet] Writing kubelet configuration to file "/var/lib/kubelet/config.yaml"
[preflight] Activating the kubelet service
[certificates] Generated front-proxy-ca certificate and key.
[certificates] Generated front-proxy-client certificate and key.
[certificates] Generated ca certificate and key.
[certificates] Generated apiserver certificate and key.
[certificates] apiserver serving cert is signed for DNS names [master kubernetes kubernetes.default kubernetes.default.svc kubernetes.default.svc.cluster.local] and IPs [10.96.0.1 192.168.1.74]
[certificates] Generated apiserver-kubelet-client certificate and key.
[certificates] Generated etcd/ca certificate and key.
[certificates] Generated etcd/server certificate and key.
[certificates] etcd/server serving cert is signed for DNS names [master localhost] and IPs [127.0.0.1 ::1]
[certificates] Generated etcd/peer certificate and key.
[certificates] etcd/peer serving cert is signed for DNS names [master localhost] and IPs [192.168.1.74 127.0.0.1 ::1]
[certificates] Generated apiserver-etcd-client certificate and key.
[certificates] Generated etcd/healthcheck-client certificate and key.
[certificates] valid certificates and keys now exist in "/etc/kubernetes/pki"
[certificates] Generated sa key and public key.
[kubeconfig] Wrote KubeConfig file to disk: "/etc/kubernetes/admin.conf"
[kubeconfig] Wrote KubeConfig file to disk: "/etc/kubernetes/kubelet.conf"
[kubeconfig] Wrote KubeConfig file to disk: "/etc/kubernetes/controller-manager.conf"
[kubeconfig] Wrote KubeConfig file to disk: "/etc/kubernetes/scheduler.conf"
[controlplane] wrote Static Pod manifest for component kube-apiserver to "/etc/kubernetes/manifests/kube-apiserver.yaml"
[controlplane] wrote Static Pod manifest for component kube-controller-manager to "/etc/kubernetes/manifests/kube-controller-manager.yaml"
[controlplane] wrote Static Pod manifest for component kube-scheduler to "/etc/kubernetes/manifests/kube-scheduler.yaml"
[etcd] Wrote Static Pod manifest for a local etcd instance to "/etc/kubernetes/manifests/etcd.yaml"
[init] waiting for the kubelet to boot up the control plane as Static Pods from directory "/etc/kubernetes/manifests"
[init] this might take a minute or longer if the control plane images have to be pulled
[apiclient] All control plane components are healthy after 184.012835 seconds
[uploadconfig] storing the configuration used in ConfigMap "kubeadm-config" in the "kube-system" Namespace
[kubelet] Creating a ConfigMap "kubelet-config-1.12" in namespace kube-system with the configuration for the kubelets in the cluster
[markmaster] Marking the node master as master by adding the label "node-role.kubernetes.io/master=''"
[markmaster] Marking the node master as master by adding the taints [node-role.kubernetes.io/master:NoSchedule]
[patchnode] Uploading the CRI Socket information "/var/run/dockershim.sock" to the Node API object "master" as an annotation
[bootstraptoken] using token: magb4r.atgo9lf1iluzp1tx
[bootstraptoken] configured RBAC rules to allow Node Bootstrap tokens to post CSRs in order for nodes to get long term certificate credentials
[bootstraptoken] configured RBAC rules to allow the csrapprover controller automatically approve CSRs from a Node Bootstrap Token
[bootstraptoken] configured RBAC rules to allow certificate rotation for all node client certificates in the cluster
[bootstraptoken] creating the "cluster-info" ConfigMap in the "kube-public" namespace
[addons] Applied essential addon: CoreDNS
[addons] Applied essential addon: kube-proxy

Your Kubernetes master has initialized successfully!

To start using your cluster, you need to run the following as a regular user:

  mkdir -p $HOME/.kube
  sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
  sudo chown $(id -u):$(id -g) $HOME/.kube/config

You should now deploy a pod network to the cluster.
Run "kubectl apply -f [podnetwork].yaml" with one of the options listed at:
  https://kubernetes.io/docs/concepts/cluster-administration/addons/

You can now join any number of machines by running the following on each node
as root:

  kubeadm join 192.168.1.74:6443 --token magb4r.atgo9lf1iluzp1tx --discovery-token-ca-cert-hash sha256:d77c0e09fb9f6b95b8622f457e19cd15c32b65e776d7196e51fae7fcc2c80681

```

Run on master:

```
$ mkdir $HOME/.kube
$ sudo cp /etc/kubernetes/admin.conf $HOME/.kube/config
$ sudo chown $(id --user):$(id --group) $HOME/.kube/config
```

Run on all nodes (see above):

```
$ sudo kubeadm join 192.168.1.74:6443 --token magb4r.atgo9lf1iluzp1tx --discovery-token-ca-cert-hash sha256:d77c0e09fb9f6b95b8622f457e19cd15c32b65e776d7196e51fae7fcc2c80681
```

Output:

```
[preflight] running pre-flight checks
        [WARNING RequiredIPVSKernelModulesAvailable]: the IPVS proxier will not be used, because the following required kernel modules are not loaded: [ip_vs_wrr ip_vs_sh ip_vs ip_vs_rr] or no builtin kernel ipvs support: map[ip_vs:{} ip_vs_rr:{} ip_vs_wrr:{} ip_vs_sh:{} nf_conntrack_ipv4:{}]
you can solve this problem with following methods:
 1. Run 'modprobe -- ' to load missing kernel modules;
2. Provide the missing builtin kernel ipvs support

        [WARNING SystemVerification]: this Docker version is not on the list of validated versions: 18.04.0-ce. Latest validated version: 18.06
[discovery] Trying to connect to API Server "192.168.1.74:6443"
[discovery] Created cluster-info discovery client, requesting info from "https://192.168.1.74:6443"
[discovery] Requesting info from "https://192.168.1.74:6443" again to validate TLS against the pinned public key
[discovery] Cluster info signature and contents are valid and TLS certificate validates against pinned roots, will use API Server "192.168.1.74:6443"
[discovery] Successfully established connection with API Server "192.168.1.74:6443"
[kubelet] Downloading configuration for the kubelet from the "kubelet-config-1.12" ConfigMap in the kube-system namespace
[kubelet] Writing kubelet configuration to file "/var/lib/kubelet/config.yaml"
[kubelet] Writing kubelet environment file with flags to file "/var/lib/kubelet/kubeadm-flags.env"
[preflight] Activating the kubelet service
[tlsbootstrap] Waiting for the kubelet to perform the TLS Bootstrap...
[patchnode] Uploading the CRI Socket information "/var/run/dockershim.sock" to the Node API object "node01" as an annotation

This node has joined the cluster:
* Certificate signing request was sent to apiserver and a response was received.
* The Kubelet was informed of the new secure connection details.

Run 'kubectl get nodes' on the master to see this node join the cluster.
```

Run on master:

```
$ kubectl get nodes
```

Output:

```
NAME     STATUS     ROLES    AGE   VERSION
master   NotReady   master   13m   v1.12.3
node01   NotReady   <none>   11m   v1.12.3
node02   NotReady   <none>   11m   v1.12.3
node03   NotReady   <none>   11m   v1.12.3
node04   NotReady   <none>   11m   v1.12.3
```

Run on master:

```
$ kubectl apply --filename=https://raw.githubusercontent.com/coreos/flannel/bc79dd1505b0c8681ece4de4c0d86c5cd2643275/Documentation/kube-flannel.yml
```

Output:

```
clusterrole.rbac.authorization.k8s.io/flannel created
clusterrolebinding.rbac.authorization.k8s.io/flannel created
serviceaccount/flannel created
configmap/kube-flannel-cfg created
daemonset.extensions/kube-flannel-ds-amd64 created
daemonset.extensions/kube-flannel-ds-arm64 created
daemonset.extensions/kube-flannel-ds-arm created
daemonset.extensions/kube-flannel-ds-ppc64le created
daemonset.extensions/kube-flannel-ds-s390x created
```

Run on master:

```
$ kubectl get all --all-namespaces
```

Output:


```
NAMESPACE     NAME                                 READY   STATUS    RESTARTS   AGE
kube-system   pod/coredns-576cbf47c7-4zwrx         1/1     Running   0          109m
kube-system   pod/coredns-576cbf47c7-bdk24         1/1     Running   0          109m
kube-system   pod/etcd-master                      1/1     Running   0          109m
kube-system   pod/kube-apiserver-master            1/1     Running   1          109m
kube-system   pod/kube-controller-manager-master   1/1     Running   0          109m
kube-system   pod/kube-flannel-ds-arm-cv7x8        1/1     Running   0          20m
kube-system   pod/kube-flannel-ds-arm-gvlqg        1/1     Running   0          20m
kube-system   pod/kube-flannel-ds-arm-gxnkz        1/1     Running   0          20m
kube-system   pod/kube-flannel-ds-arm-kqnjr        1/1     Running   0          20m
kube-system   pod/kube-flannel-ds-arm-pwb5z        1/1     Running   0          20m
kube-system   pod/kube-proxy-9bplx                 1/1     Running   0          108m
kube-system   pod/kube-proxy-cn8z8                 1/1     Running   0          108m
kube-system   pod/kube-proxy-cwltf                 1/1     Running   0          108m
kube-system   pod/kube-proxy-ndjfh                 1/1     Running   0          109m
kube-system   pod/kube-proxy-q49kt                 1/1     Running   0          107m
kube-system   pod/kube-scheduler-master            1/1     Running   0          109m

NAMESPACE     NAME                 TYPE        CLUSTER-IP   EXTERNAL-IP   PORT(S)         AGE
default       service/kubernetes   ClusterIP   10.96.0.1    <none>        443/TCP         111m
kube-system   service/kube-dns     ClusterIP   10.96.0.10   <none>        53/UDP,53/TCP   110m

NAMESPACE     NAME                                     DESIRED   CURRENT   READY   UP-TO-DATE   AVAILABLE   NODE SELECTOR                     AGE
kube-system   daemonset.apps/kube-flannel-ds-amd64     0         0         0       0            0           beta.kubernetes.io/arch=amd64     20m
kube-system   daemonset.apps/kube-flannel-ds-arm       5         5         5       5            5           beta.kubernetes.io/arch=arm       20m
kube-system   daemonset.apps/kube-flannel-ds-arm64     0         0         0       0            0           beta.kubernetes.io/arch=arm64     20m
kube-system   daemonset.apps/kube-flannel-ds-ppc64le   0         0         0       0            0           beta.kubernetes.io/arch=ppc64le   20m
kube-system   daemonset.apps/kube-flannel-ds-s390x     0         0         0       0            0           beta.kubernetes.io/arch=s390x     20m
kube-system   daemonset.apps/kube-proxy                5         5         5       5            5           <none>                            110m

NAMESPACE     NAME                      DESIRED   CURRENT   UP-TO-DATE   AVAILABLE   AGE
kube-system   deployment.apps/coredns   2         2         2            2           110m

NAMESPACE     NAME                                 DESIRED   CURRENT   READY   AGE
kube-system   replicaset.apps/coredns-576cbf47c7   2         2         2       109m
```

Run on master:

```
$ kubectl get nodes
```

Output:

```
NAME     STATUS   ROLES    AGE    VERSION
master   Ready    master   100m   v1.12.3
node01   Ready    <none>   98m    v1.12.3
node02   Ready    <none>   98m    v1.12.3
node03   Ready    <none>   98m    v1.12.3
node04   Ready    <none>   98m    v1.12.3
```

## References

* [Creating a single master cluster with kubeadm](https://kubernetes.io/docs/setup/independent/create-cluster-kubeadm/)
* [Setup Kubernetes on a Raspberry Pi Cluster easily the official way!](https://blog.hypriot.com/post/setup-kubernetes-raspberry-pi-cluster/)
