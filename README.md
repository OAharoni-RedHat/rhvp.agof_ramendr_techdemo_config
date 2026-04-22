# AGOF Config — RamenDR TechDemo

AGOF (Ansible GitOps Framework) controller configuration for the
**RamenDR TechDemo** validated pattern.

This repository is consumed by AGOF to configure AAP Controller with the
resources needed to install Redis on RHEL VMs and manage Route 53
failover DNS for the pattern.

## What It Creates in AAP

| Resource | Name | Purpose |
|----------|------|---------|
| Organization | RamenDR TechDemo | Top-level org for all resources |
| Project | RamenDR TechDemo Ansible Collection | SCM project pointing to [rhvp.ramendr_techdemo](https://github.com/validatedpatterns-demos/rhvp.ramendr_techdemo) |
| Inventory | RamenDR VM Inventory | Placeholder — playbooks discover hosts dynamically |
| Credential | vm_ssh_credential | Machine credential for SSH to RHEL VMs |
| Job Template | Discover and Install Redis | Discovers the Redis VM LB, registers RHEL, installs Redis |
| Job Template | Setup AWS Route53 Failover | Creates Route 53 failover CNAME records |

## Secrets

This config references secrets that must be available in the AGOF vault
file (`agof-vault-file` secret in Vault):

| Variable | Source |
|----------|--------|
| `admin_password` | AAP Controller admin password |
| `rhsm_username` | Red Hat Subscription Manager username |
| `rhsm_password` | Red Hat Subscription Manager password |
| `vm_ssh_private_key` | SSH private key for the `cloud-user` on RHEL VMs |

## Usage

Set this repo as the `agof.iac_repo` in your pattern overrides:

```yaml
agof:
  iac_repo: https://github.com/validatedpatterns-demos/agof_ramendr_techdemo_config.git
  iac_revision: main
```
