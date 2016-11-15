    curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | apt-key add -

    curl https://packages.cloud.google.com/apt/doc/apt-key.gpg \
      | apt-key add -

    cat <<EOF > /etc/apt/sources.list.d/kubernetes.list
    deb http://apt.kubernetes.io/ kubernetes-xenial main
    EOF

    apt-get update

    apt-get install -y docker.io kubelet kubeadm kubectl kubernetes-cni

    kubeadm init --api-advertise-addresses=51.15.41.67

    kubectl taint nodes --all dedicated-

    kubectl apply -f https://git.io/weave-kube

    kubectl create -f https://rawgit.com/kubernetes/dashboard/master/src/deploy/kubernetes-dashboard.yaml

    scp root@51.15.41.67:/etc/kubernetes/admin.conf .
