# Self Host Error Monitoring
- Preferable to self-host Sentry on the server stack you're maintaining. Documentation [here](https://develop.sentry.dev/self-hosted/)
- Setup the domain at `sentry.<your_first_name>.yral.com`. You will use the wildcard mechanism here the same way you're hosting the other services
- Setup auth on your Sentry instance to use OAuth 2.0 for Google Login and limited to only users with a `@gobazzinga.io` email
- Connect the production services you own and host and send a pull request [here](https://github.com/dolr-ai/yral/blob/main/service-summary.md) with the relevant details updated
