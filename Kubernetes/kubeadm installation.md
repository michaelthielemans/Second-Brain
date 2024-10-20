# Prerequisites for installing kubernetes with kubeadm

## disable swap
    swapoff -a
    /etc/fstab
## add port 6443 to firewall
    firewall-cmd --add-port=6443/tcp --permanent

[root@localhost ~]# systemctl stop firewalld
[root@localhost ~]# systemctl disable firewalld



## Enable IPv4 packet forwarding
    To manually enable IPv4 packet forwarding:

    ### sysctl params required by setup, params persist across reboots

cat <<EOF | sudo tee /etc/sysctl.d/k8s.conf
net.ipv4.ip_forward = 1
EOF

    ### Apply sysctl params without reboot
        sudo sysctl --system

    #### Verify that net.ipv4.ip_forward is set to 1 with:

        sysctl net.ipv4.ip_forward

## install containerd    
    ### download and extract from official binaries
        in dir /usr/local

        wget https://github.com/containerd/containerd/releases/download/v1.7.15/containerd-1.7.15-linux-amd64.tar.gz
        tar Cxzvf /usr/local containerd-1.7.15-linux-amd64.tar.gz

    ### enable start containerd with systemd
        cd /usr/lib/systemd/system/
        wget https://raw.githubusercontent.com/containerd/containerd/main/containerd.service

        systemctl daemon-reload
        systemctl enable --now containerd

    ### install runc
        cd /usr/local
        wget https://github.com/opencontainers/runc/releases/download/v1.1.12/runc.amd64
        install -m 755 runc.amd64 /usr/local/sbin/runc

    ### adjustment of the config.toml file for systemd

            The systemd cgroup driver is recommended if you use cgroup v2.
        --> rocky linux 9 uses cgroup2fs
            the cgroup you use can be checked with   $ stat -fc %T /sys/fs/cgroup/

        The default configuration can be generated via (run as root)
        $ containerd config default > /etc/containerd/config.toml

        Open the config.toml and adjust the settings

        [plugins."io.containerd.grpc.v1.cri".containerd.runtimes.runc]
        ...
            [plugins."io.containerd.grpc.v1.cri".containerd.runtimes.runc.options]
                SystemdCgroup = true

    ### adjust config file for sandbox image that is compatible wit the kubetrnetes version
        [plugins."io.containerd.grpc.v1.cri"]
            sandbox_image = "registry.k8s.io/pause:3.9"

    ### restart container d
        systemctl restart containerd

## install CNI plugins
    in dir /opt
    wget https://github.com/containernetworking/plugins/releases/download/v1.4.1/cni-plugins-linux-amd64-v1.4.1.tgz
    mkdir -p /opt/cni/bin
    tar Cxzvf /opt/cni/bin cni-plugins-linux-amd64-v1.4.1.tgz


## manually configure the cgroup driver for kubelet.
    Kubeadm will use the systemd cgroup driver, from
    this is not needed when using kubeadm version higher then 1.28

## install kubeadm, kubelet, kubecli
    ### Set SELinux in permissive mode (effectively disabling it)
        sudo setenforce 0
        sudo sed -i 's/^SELINUX=enforcing$/SELINUX=permissive/' /etc/selinux/config

    ### add the kubernetes repository


cat <<EOF | sudo tee /etc/yum.repos.d/kubernetes.repo
[kubernetes]
name=Kubernetes
baseurl=https://pkgs.k8s.io/core:/stable:/v1.30/rpm/
enabled=1
gpgcheck=1
gpgkey=https://pkgs.k8s.io/core:/stable:/v1.30/rpm/repodata/repomd.xml.key
exclude=kubelet kubeadm kubectl cri-tools kubernetes-cni
EOF


    ### install packages
        sudo yum install -y kubelet kubeadm kubectl --disableexcludes=kubernetes


    ### Enable the kubelet service before running kubeadm
        sudo systemctl enable --now kubelet


# create a cluster
    ## check if network route is ok, there s
        ip route show # Look for a line starting with "default via"

    ## Initializing your control-plane node
        $ kubeadm init --apiserver-advertise-address=192.168.10.89 --pod-network-cidr
    
    ## export the KUBECONFIG alias if you are the root user
        export KUBECONFIG=/etc/kubernetes/admin.conf

# deploying the cilium pod network
    ## Install the Cilium CLI with helm

        ### install helm
            $ curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3
            $ chmod 700 get_helm.sh
            $ ./get_helm.sh

        ### add the cilium helm repo
            helm repo add cilium https://helm.cilium.io/

        ###
            helm install cilium cilium/cilium --version 1.15.4 \
            --namespace kube-system


# adding nodes to the cluster

kubeadm join 192.168.10.39:6443 --token abcdef.0123456789abcdef \
        --discovery-token-ca-cert-hash sha256:6847cfd8e88a3c3422b95db8c0b0f7024f87a1f28b913d8e775240f485f8b0b1

    ## if you cannot find the token you can list it
        $ kubeadm token list



# Troubleshooting

kubeadm checks
$ kubeadm cluster-info

kubeclt checks


containerd checks
$ ctr