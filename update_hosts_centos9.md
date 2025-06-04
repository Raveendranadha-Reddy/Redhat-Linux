
# Update /etc/hosts in CentOS Stream 9

This guide explains how to update the `/etc/hosts` file to set static hostname-to-IP mappings.

---

## Steps

### 1. Open the `/etc/hosts` file
Use your preferred text editor:

```bash
sudo vi /etc/hosts
```
or
```bash
sudo nano /etc/hosts
```

---

### 2. Add Host Entries

Each line should follow this format:

```
<IP-address>    <hostname>    [optional-aliases]
```

#### Example:
```
127.0.0.1       localhost localhost.localdomain
192.168.1.35    k8s-master
192.168.1.36    k8s-worker1
192.168.1.37    k8s-worker2
```

- `127.0.0.1` is the loopback address.
- Add private IP and hostname mappings.
- Aliases (e.g., short names) are optional.

---

### 3. Save and Exit

- In `vi`: Press `Esc`, then type `:wq` and hit Enter.
- In `nano`: Press `Ctrl+O`, Enter, then `Ctrl+X`.

---

### 4. Test Hostname Resolution

```bash
ping -c 2 k8s-worker1
```

---

## Permissions

Ensure file has correct permissions:

```bash
ls -l /etc/hosts
```

Expected output:
```
-rw-r--r--. 1 root root ... /etc/hosts
```

Only root should be allowed to modify this file.
