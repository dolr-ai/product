We work exclusively on Github. The way we structure projects and services are using microservices with their owners maintaining and deploying them end to end. IF you've built it, it's your responsibility to maintain, scale, fix, troubleshoot, enhance it. If you're inheriting an existing service, the expectation is for you to refactor and rewrite that service so that you can own and maintain it end to end. This will also include all supporting services and infrastructure that you require to host and deploy it including databases, reverse proxies, monitoring, alerting, logging, etc.

We have a couple of shared infrastructure pieces that we maintain as a team. These are:
- Hashicorp Vault for secrets management
- Beszel for server monitoring and alerting
- Uptime Kuma for service uptime monitoring
- Sentry for detailed error monitoring and alerting. Including exception tracking, traces, performance monitoring, etc.

You can find all of the above and more linked at [dashboard.yral.com](https://dashboard.yral.com/). Ask Saikat on the team chat channel if you need access to something that you don't have.

# Getting Started

1. Create a github profile with your company email ID of the form `<your_first_name>-<your_last_name>-yral` on Github. Login with Google and your company email and setup Github profile with the above username. Once done, reach out to Saikat on the team chat channel to get added to the Yral Github organization.
2. When you're done with this, create your SSH key and send a pull request to this page so that subsequent infrastructure access can be given to this key. Pull request to be sent to this file: [ssh-keys.md](https://github.com/dolr-ai/yral/blob/main/yral-current-team-ssh-keys.md). Note that the SSH keys are listed in alphabetical order. Pull request should follow that convention.
3. Next, you will be given the following things to start with:
   1. 2 servers to deploy a redundant load balancer. They also need to double up as a reverse proxy and a TLS termination point
   2. A subdomain with a wildcard DNS record pointing to the load balancer servers. The wildcard is of the form `*.<your_first_name>.yral.com` and points to the load balancer servers.
   3. You need to look up the IP's of the servers given to you here: [server list](https://github.com/dolr-ai/hetzner-bare-metal-fleet/blob/main/ansible/inventory/hosts.yml). It will be of the form `<your_first_name>-<server_number>`. Congratulations, you have root access to these servers for a week till the end of the week when your access gets automatically revoked. Take this time to create sandboxed and non-root users on these servers and provision SSH access to the user so that you can configure your repo CI to deploy to these servers without using root access.
   4. We use containers exclusively for running all our services. You will use the sandboxed user to stand up whatever services you need via docker-compose ideally. The servers provided to you already come setup with docker installed.
4. Once done with setup, your first task is to deploy a simple "Hello World" service that returns "Hello World" on the `hello-world.<your_first_name>.yral.com` subdomain. The challenge with this task if for you to figure out redundancy and policies so that even if 1 of the servers is turned off or goes down, your service is still up and running and can serve traffic.
5. When done with this, you are ready to tackle larger problems. We can assign more challenging and interesting problems for you to solve during the next morning meeting.