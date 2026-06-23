# Self Hosted Kafka

We expose all events emitted by our client apps, primarily mobile apps. All internal team members to consume this for access to raw events.

# Details

Endpoint: https://kafka-bridge.yral.com
Auth Header: `X-Bearer-Token: <secret_from_vault>` (Get the secret from [here](https://vault.yral.com/ui/vault/secrets/secret/kv/SAIKAT_KAFKA_BRIDGE_BEARER_TOKEN))
Topic: snowplow-enriched
Consumer group prefix: bridge-

Documentation on how to use this is available [here](https://strimzi.io/docs/bridge/latest/#con-requests-http-bridge-bridge)