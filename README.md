# PROJECT Rocky-VM

_I have a dedicated server running Ubuntu, and I was looking to set up a Rocky box for practicing systems administration and creating a personal sandbox. I utilized KVM-QEMU, and here is the wack_

# Rocky Linux 9.5 VM Setup Guide
## 1. Create VM with text console
```bash
virt-install \
  --name rocky \
  --memory 2048 \
  --vcpus 2 \
  --disk size=20 \
  --location /var/lib/libvirt/images/isos/Rocky-9.5-x86_64-minimal.iso \
  --os-variant rhel9.0 \
  --network bridge=virbr0 \
  --graphics none \
  --console pty,target_type=serial \
  --extra-args "console=ttyS0,115200n8 inst.text"
```

## 2. Complete text-mode installation

- Selected text mode
- Used automatic partitioning with LVM
- Set root password
- Minimal installation profile
- Network enabled (DHCP)

## 3. Configure SSH to allow root login

```bash
# Check current SSH configuration
grep PermitRootLogin /etc/ssh/sshd_config

# Edit SSH configuration
vi /etc/ssh/sshd_config
# Add line: PermitRootLogin yes

# Restart SSH service
systemctl restart sshd
```

## 4. Get VM IP address

```bash
ip -br addr
```

## 5. SSH from host to VM

```bash
ssh root@192.000.000
```

## 6. Optional: Create SSH alias on host

```bash
# Add to ~/.bashrc
alias rocky='ssh root@192.000.000'

# Apply changes
source ~/.bashrc
```
