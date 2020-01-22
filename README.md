# k8s-multus-calico-sandbox
Kubernetes Multus CNI Calico

~~~~
kubectl get node -o wide
kubectl get pod --all-namespaces -o wide
git clone https://github.com/intel/multus-cni.git
cd multus-cni/
"cat ./images/multus-daemonset.yml | kubectl apply -f -"

kubectl get pods --all-namespaces | grep -i multus
kube-system   kube-multus-ds-amd64-knnkx                 1/1     Running   0          8m5s
kube-system   kube-multus-ds-amd64-pr7zf                 1/1     Running   0          8m5s
kube-system   kube-multus-ds-amd64-xshww                 1/1     Running   0          8m5s
~~~~

~~~~
>vagrant up
>vagrant ssh remotecontrol01
sudo ansible-playbook -i /vagrant/kube-cluster/hosts /vagrant/kube-cluster/1_initial.yml
sudo ansible-playbook -i /vagrant/kube-cluster/hosts /vagrant/kube-cluster/2_kube-dependencies.yml
sudo ansible-playbook -i /vagrant/kube-cluster/hosts /vagrant/kube-cluster/3_masters.yml
sudo ansible-playbook -i /vagrant/kube-cluster/hosts /vagrant/kube-cluster/4_workers.yml

vagrant ssh k8s-master01
$ kubectl get nodes
NAME           STATUS   ROLES    AGE   VERSION
k8s-master01   Ready    master   20m   v1.16.0
worker01       Ready    <none>   12m   v1.16.0
worker02       Ready    <none>   12m   v1.16.0
$ kubectl get pods --all-namespaces
NAMESPACE     NAME                                      READY   STATUS    RESTARTS   AGE
kube-system   calico-kube-controllers-55754f75c-kckwb   1/1     Running   0          19m
kube-system   calico-node-6qhgc                         1/1     Running   7          19m
kube-system   calico-node-8648z                         1/1     Running   0          11m
kube-system   calico-node-m4thf                         1/1     Running   0          11m
kube-system   coredns-5644d7b6d9-2844c                  1/1     Running   0          19m
kube-system   coredns-5644d7b6d9-2dwp2                  1/1     Running   0          19m
kube-system   etcd-k8s-master01                         1/1     Running   0          18m
kube-system   kube-apiserver-k8s-master01               1/1     Running   0          19m
kube-system   kube-controller-manager-k8s-master01      1/1     Running   0          18m
kube-system   kube-proxy-2cwcx                          1/1     Running   0          11m
kube-system   kube-proxy-7xbfz                          1/1     Running   0          11m
kube-system   kube-proxy-dfgxk                          1/1     Running   0          19m
kube-system   kube-scheduler-k8s-master01               1/1     Running   0          18m
~~~~

~~~~
Quickstart Guide
https://github.com/intel/multus-cni/blob/master/doc/quickstart.md
How to setup Multus CNI phase1 demo environment
https://github.com/intel/multus-cni/wiki/How-to-setup-Multus-CNI-phase1-demo-environment
Creating multiple network interfaces for pods in Kubernetes to enable NFV and SDN use cases in container environments
https://01.org/kubernetes/building-blocks/multus-cni
Cluster Networking
https://kubernetes.io/docs/concepts/cluster-administration/networking/
How to Bring your Virtual Machine VNF to Container World?
https://events19.linuxfoundation.org/wp-content/uploads/2017/12/How-to-Bring-your-Virtual-Machine-VNF-to-Container-World-Tomofumi-Hayashi-Red-Hat.pdf
Advanced Networking Features in Kubernetes*and Container Bare Metal
https://builders.intel.com/docs/networkbuilders/adv-network-features-in-kubernetes-app-note.pdf
~~~~
