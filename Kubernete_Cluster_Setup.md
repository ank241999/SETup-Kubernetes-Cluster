1\--\>\> Create 4 Machine \[ t2.medium \] \[ 1 Master , 3 Worker \] \[
allow all traffic or allow require port in firewall \] 2\--\>\> Access
all machine with mobaxterm 3\--\>\> set unique hostname of all 4 machine
4\--\>\> install docker on all machines 5\--\>\> open
/etc/containerd/config.toml file and comment this line \--\>\>
disabled_plugins = \[\"cri\"\] 6\--\>\> Now paste this content version =
2 \[plugins\] \[plugins.\"io.containerd.grpc.v1.cri\"\]
\[plugins.\"io.containerd.grpc.v1.cri\".containerd\]
\[plugins.\"io.containerd.grpc.v1.cri\".containerd.runtimes\]
\[plugins.\"io.containerd.grpc.v1.cri\".containerd.runtimes.runc\]
runtime_type = \"io.containerd.runc.v2\"
\[plugins.\"io.containerd.grpc.v1.cri\".containerd.runtimes.runc.options\]
SystemdCgroup=true \-\-\-\-\-\-- and save this file
\-\-\-\-\-\-\-\-\-\-\-\-- 7\--\>\> now restart containerd service
8\--\>\> run these command on control plane:- \--\>\> apt-get update
\--\>\> apt-get install -y apt-transport-https ca-certificates curl
\--\>\> curl -fsSLo /etc/apt/keyrings/kubernetes-archive-keyring.gpg
https://packages.cloud.google.com/apt/doc/apt-key.gpg \--\>\> echo \"deb
\[signed-by=/etc/apt/keyrings/kubernetes-archive-keyring.gpg\]
https://apt.kubernetes.io/ kubernetes-xenial main\" \| sudo tee
/etc/apt/sources.list.d/kubernetes.list \--\>\> apt-get update \--\>\>
apt-get install -y kubelet kubeadm kubectl \--\>\> apt-mark hold kubelet
kubeadm kubectl

9\--\>\> on master machin run \--\>\> kubeadm init 10\--\>\> this
command will initialize your control plane and prints the cluster
joining command, now run join command on all worker machine 11\--\>\>
make an entry in .bash_profile on master machine \--\>\>\>\> export
KUBECONFIG=/etc/kubernetes/admin.conf 12\--\>\> logout and login again
with root 13\--\>\> run this command \--\>\> curl
https://raw.githubusercontent.com/projectcalico/calico/v3.25.1/manifests/calico.yaml
-O 14\--\>\> run this command \--\>\> kubectl apply -f calico.yaml
15\--\>\> run this command on control plane == kubectl completion bash
\| sudo tee /etc/bash_completion.d/kubectl \> /dev/null 16\--\>\>
Done\....!!!!!!!!!
