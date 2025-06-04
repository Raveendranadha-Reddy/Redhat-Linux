
# Assign Static IP Address in CentOS Stream 9

This guide shows how to assign a static IP to a network interface (e.g., `ens192`) on CentOS Stream 9 using `nmcli`.

---

## Step-by-Step Instructions

### 1. Delete Existing Connection (if needed)
```bash
nmcli connection delete ens192
```

### 2. Recreate the Connection with Static IP
```bash
nmcli connection add type ethernet con-name ens192 ifname ens192 \
  ipv4.addresses 192.168.1.35/24 \
  ipv4.gateway 192.168.1.1 \
  ipv4.dns "8.8.8.8 8.8.4.4" \
  ipv4.method manual \
  autoconnect yes
```

### 3. Restart NetworkManager (recommended due to version mismatch)
```bash
systemctl restart NetworkManager
```

### 4. Bring the Connection Up
```bash
nmcli connection up ens192
```

### 5. Verify IP Address
```bash
ip addr show ens192
```

---

## Notes

- CIDR `/24` = subnet mask `255.255.255.0`
- Replace the IPs as per your network setup.
- Use `nmcli connection show` to see current connections.

---

**Backup (Optional):**
```bash
cp /etc/NetworkManager/system-connections/ens192.nmconnection /root/ens192.backup
```
