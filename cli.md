# IPA CLI Tutorial

## Server Installation

Install server binaries on CentOS / Red Hat

```bash
sudo yum module install idm:DL1/{server,client,dns,adtrust}
```

Configure firewall

```bash
sudo firewall-cmd --add-service={freeipa-4,ntp} --permanent
sudo firewall-cmd --reload
```

Automated installation without user interaction

```bash
sudo ipa-server-install \
    --unattended \
    --realm DOMAIN.LOCAL \
    --domain domain.local \
    --ds-password PASSWORD \
    --admin-password PASSWORD \
    --setup-dns \
    --mkhomedir \
    --auto-reverse \
    --forward-policy first \
    --forwarder 8.8.8.8 \
    --forwarder 8.8.4.4
```

Confirm installation

```bash
ipactl status
```

Login as administrator and view token

```bash
kinit admin && klist
```

Add ipa replica

```bash
ipa hostgroup-add-member ipaservers --hosts ipa2.domain.local
```

Uninstall ipa-server

```bash
sudo ipa-server-install --uninstall
```

## Replicate Installation

Configure firewall

```bash
sudo firewall-cmd --add-service={freeipa-4,ntp} --permanent
sudo firewall-cmd --reload
```

Install replica packages

```bash
sudo yum module install idm:DL1/{server,client,dns,adtrust}
```

Install client 

```bash
sudo ipa-client-install \
    --unattended \
    --principal admin@domain.local \
    --password PASSWORD \
    --hostname ipa2.domain.local \
    --mkhomedir \
    --server ipa1.domain.local \
    --domain domain.local \
    --realm domain.LOCAL \
    --enable-dns-updates
```

Install Replica

```bash
sudo ipa-replica-install \
    --unattended \
    --setup-dns \
    --auto-reverse \
    --mkhomedir \
    --forward-policy first \
    --forwarder 8.8.8.8 \
    --forwarder 8.8.4.4
```

Uninstall ipa-client

```bash
sudo ipa-client-install --uninstall
```

## Client Installation

Install client packages

```bash
sudo yum module install idm:DL1/client
```

Install client

```bash
sudo ipa-client-install \
    --unattended \
    --principal admin@domain.local
    --password PASSWORD \
    --hostname ipa2.domain.local \
    --mkhomedir \
    --server ipa1.domain.local \
    --domain domain.local \
    --realm domain.LOCAL \
    --enable-dns-updates
```

Uninstall ipa-client

```bash
sudo ipa-client-install --uninstall
```
