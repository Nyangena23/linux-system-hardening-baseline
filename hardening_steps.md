## Linux System Hardening Baseline - Implementation Steps

### Summary
This project applies a Linux security baseline to reduce attack surface and harden a system against common attack vectors.

### Controls Applied
1. **Root Login Disabled** - Prevents direct root SSH access
2. **Firewall Enforced** - UFW configured with deny-by-default policy
3. **SSH Hardened** - SSH configuration restricted for enhanced security
4. **Password Policy Enforced** - Minimum complexity and aging requirements
5. **Unused Services Disabled** - Minimizes attack surface

### Step-by-Step Implementation

#### Step 1: User & Permission Hardening
```bash
sudo adduser secadmin
sudo usermod -aG sudo secadmin
sudo passwd -l root
```

#### Step 2: SSH Hardening
```bash
sudo ./scripts/ssh_hardening.sh
```

#### Step 3: Firewall Configuration
```bash
sudo ./scripts/firewall_setup.sh
```

#### Step 4: Password Policy Hardening
Edit `/etc/login.defs`:
- PASS_MAX_DAYS: 90
- PASS_MIN_DAYS: 10
- PASS_WARN_AGE: 7

Install PAM module:
```bash
sudo apt install libpam-pwquality -y
```

#### Step 5: Disable Unused Services
```bash
sudo systemctl disable cups
sudo systemctl stop cups
```

#### Step 6: Enable Auto Security Updates
```bash
sudo apt install unattended-upgrades -y
sudo dpkg-reconfigure unattended-upgrades
```

### Verification
- Before hardening state: `verification/before_hardening.txt`
- After hardening state: `verification/after_hardening.txt`

### Result
**System attack surface significantly reduced** with improved security posture and reduced exposure to common attack vectors.