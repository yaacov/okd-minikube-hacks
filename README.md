# okd-minikube-hacks

### Set up kernel paramtets

Add `intel_iommu=on systemd.unified_cgroup_hierarchy=0` to `GRUB_CMDLINE_LINUX`
```
sudo vim /etc/default/grub # Adit GRUB_CMDLINE_LINUX
sudo grub2-mkconfig -o /boot/grub2/grub.cfg
reboot
```

### Install virtualization

https://docs.fedoraproject.org/en-US/quick-docs/getting-started-with-virtualization/

```
sudo dnf install @virtualization
sudo systemctl start libvirtd
sudo systemctl enable libvirtd
virt-host-validate 
sudo usermod -a -G libvirt $(whoami)
```

### Install minikube

https://kubernetes.io/docs/setup/learning-environment/minikube/

```
curl -Lo minikube https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64   && chmod +x minikube
sudo mkdir -p /usr/local/bin/
sudo install minikube /usr/local/bin/
```
```
minikube start --vm-driver=kvm2
```

### Install OLM

https://github.com/operator-framework/operator-lifecycle-manager

```
curl -L https://github.com/operator-framework/operator-lifecycle-manager/releases/download/0.13.0/install.sh -o install.sh
chmod +x install.sh
./install.sh 0.13.0 
```

### Run the console

```
source ./contrib/environment.sh && ./bin/bridge
```

In the web-ui console http://localhost:9000 install the `kubevirt` operator using the OLM menu.
