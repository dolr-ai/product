# Getting temporary root access

You can look up the list of accessible servers here: [server list](https://github.com/dolr-ai/yral-bare-metal-kubernetes-cluster/blob/main/apps/hetzner-bare-metal-fleet/ansible/inventory/hosts.yml)

To get temporary till-end-of-week root access to these servers, ask an operator (Saikat) to grant it — the fleet automation now lives in the [yral-bare-metal-kubernetes-cluster](https://github.com/dolr-ai/yral-bare-metal-kubernetes-cluster) monorepo, and access is granted by an operator running the local mise task:

```
mise run fleet-ssh-access -- --limit <hostname|bare_metal> -e team_member_name=<your-first-name>
```

For example, for Rishi to get access to `rishi-1`, an operator runs the command above with `--limit rishi-1 -e team_member_name=rishi`. Server names come from the [server list](https://github.com/dolr-ai/yral-bare-metal-kubernetes-cluster/blob/main/apps/hetzner-bare-metal-fleet/ansible/inventory/hosts.yml).

Your key must first be registered under `team_members` in [`apps/hetzner-bare-metal-fleet/ansible/inventory/group_vars/all/vars.yml`](https://github.com/dolr-ai/yral-bare-metal-kubernetes-cluster/blob/main/apps/hetzner-bare-metal-fleet/ansible/inventory/group_vars/all/vars.yml). Access is automatically revoked by the weekly maintenance run (Mondays 9 AM IST).