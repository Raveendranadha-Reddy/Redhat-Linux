
# Kubernetes Kernel Module and Sysctl Setup

These steps configure the necessary kernel modules and sysctl parameters required for Kubernetes networking, especially for `kubeadm` installations.

---

## ✅ Load Required Kernel Modules

```bash
cat <<EOF | sudo tee /etc/modules-load.d/k8s.conf
overlay
br_netfilter
EOF

# Load modules immediately
sudo modprobe overlay
sudo modprobe br_netfilter
```

---

## ✅ Set Required sysctl Parameters for Kubernetes Networking

```bash
cat <<EOF | sudo tee /etc/sysctl.d/k8s.conf
net.bridge.bridge-nf-call-ip6tables = 1
net.bridge.bridge-nf-call-iptables  = 1
net.ipv4.ip_forward                 = 1
EOF

# Apply sysctl params without reboot
sudo sysctl --system
```

---

## 📌 Explanation

| Setting                          | Purpose                                                                 |
|----------------------------------|-------------------------------------------------------------------------|
| `overlay`, `br_netfilter`       | Required kernel modules for container networking                       |
| `net.bridge.bridge-nf-call-*`   | Ensures iptables can see bridged traffic                               |
| `net.ipv4.ip_forward`           | Enables routing of traffic between pods and services                   |

---

## ✅ Confirm Changes

```bash
lsmod | grep br_netfilter
lsmod | grep overlay
sysctl net.bridge.bridge-nf-call-iptables
sysctl net.ipv4.ip_forward
```

If all commands return expected results, your system is **Kubernetes networking-ready**.
