## Vault basics

### Encrypt
```bash
ansible-vault --vault-password-file=./pass encrypt crypted-file
```

### Decrypt
```bash
ansible-vault --vault-password-file=./pass decrypt crypted-file
```
