# Getting temporary root access

You can look up the list of accessible servers here: [server list](https://github.com/dolr-ai/hetzner-bare-metal-fleet/blob/main/ansible/inventory/hosts.yml)

To get temporary till-end-of-week root access to these servers, run the Github Action [here](https://github.com/dolr-ai/hetzner-bare-metal-fleet/actions/workflows/grant-ssh-access.yml)

You can run the workflow by selecting your name from the list and passing in the exact name of the server that you need root access to from [this list](https://github.com/dolr-ai/hetzner-bare-metal-fleet/blob/main/ansible/inventory/hosts.yml)