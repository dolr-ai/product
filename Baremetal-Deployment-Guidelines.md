When deploying to baremetal, there are certain problems that will be faced for each new instance. For eg. secret management, CI/CD, firewalls, etc. Each of these problems have multiple ways of being solved. This document aims to eventually land on having a consistent strategies for solving those problems.

The guidance is to follow the methods prescribed here, unless there's a more suitable method for your specific instance. If a new problem is solved that is general enough and not mentioned here, add it to the list.

## Ssh Access through CI

Prefer to restrict the CI's access to the machine down to a command. Example line in `.ssh/authorized_keys`

```ssh
restrict,command="<command>" ssh-ed25519 <key> github-actions.<service>@yral.com
```

## Firewall

Use `ufw`. Restrict all incoming requests, except necessary ports. For example, `22`, `80`, `443` for a web server.

## Reverse Proxy and SSL

Prefer to use `caddy` unless high throughput is a big concern. It has automatic ssl generation and a simple configuration format. 

## Secret Management

Use `systemd-cred` for managing secrets. MUST encrypt secrets. Prefer to encrypt with tpm2, unless unavailable. The following script can be used as the systemd unit's entrypoint:
```bash
#!/bin/bash

echo "=== Loading secrets and setting as environment variables ==="
if [ -n "$CREDENTIALS_DIRECTORY" ] && [ -d "$CREDENTIALS_DIRECTORY" ]; then
    echo "found secrets:"
    for cred in "$CREDENTIALS_DIRECTORY"/*; do
        if [ -f "$cred" ]; then
            secret_name=$(basename "$cred")
            declare -x $secret_name=$(cat "$cred")
            echo "  $secret_name"
        fi
    done
else
    echo "No credentials available"
fi

exec <service>
```

## User management for services

For every service that runs on the machine, prefer to create an unprivileged user. For example:
```bash
sudo groupadd <service>
sudo useradd -r -g <service> -s /sbin/nologin -d /var/cache/<service> <service>
```

> [!Tip]
> Systemd allows setting which user/group a binary will be run as

