# Self Hosted Kafka

We expose all events emitted by our client apps, primarily mobile apps. All internal team members can consume this for access to raw events.

## Details

- **Endpoint:** `https://kafka-bridge.yral.com`
- **Auth:** Bearer token via `X-Bearer-Token` header
- **Token:** Get from [Vault](https://vault.yral.com/ui/vault/secrets/secret/kv/SAIKAT_KAFKA_BRIDGE_BEARER_TOKEN)
- **Topic:** `snowplow-enriched`
- **Consumer group prefix:** `bridge-`
- **Data format:** TSV (Snowplow canonical enriched format, 130+ tab-separated fields)

## Quick Start

### 1. Create a consumer

```bash
TOKEN="<from_vault>"

curl -X POST "https://kafka-bridge.yral.com/consumers/bridge-my-app" \
  -H "X-Bearer-Token: $TOKEN" \
  -H "Content-Type: application/vnd.kafka.v2+json" \
  -d '{"format":"binary","auto.offset.reset":"latest"}'
```

Response:
```json
{
  "instance_id": "kafka-bridge-abc123-...",
  "base_uri": "https://kafka-bridge.yral.com/consumers/bridge-my-app/instances/kafka-bridge-abc123-..."
}
```

### 2. Subscribe to the topic

```bash
INSTANCE_ID="kafka-bridge-abc123-..."

curl -X POST "https://kafka-bridge.yral.com/consumers/bridge-my-app/instances/$INSTANCE_ID/subscription" \
  -H "X-Bearer-Token: $TOKEN" \
  -H "Content-Type: application/vnd.kafka.v2+json" \
  -d '{"topics":["snowplow-enriched"]}'
```

### 3. Poll for records

```bash
curl -H "X-Bearer-Token: $TOKEN" \
  -H "Accept: application/vnd.kafka.binary.v2+json" \
  "https://kafka-bridge.yral.com/consumers/bridge-my-app/instances/$INSTANCE_ID/records?timeout=10000"
```

Response (array of records, base64-encoded values):
```json
[
  {
    "topic": "snowplow-enriched",
    "partition": 0,
    "offset": 12345,
    "key": null,
    "value": "eXJhbC1tb2JpbGUgICAgbW9iICAgIDIwMjYtMDYtMjMgMTU6MTY6NTMuMzM2IC4uLg=="
  }
]
```

Decode the value:
```bash
echo "eXJhbC1tb2JpbGUg..." | base64 -d
```

## API Reference

Full Kafka Bridge API documentation: https://strimzi.io/docs/bridge/latest/#con-requests-http-bridge-bridge

### Key endpoints

| Method   | Path                                                | Content-Type                                   |
| -------- | --------------------------------------------------- | ---------------------------------------------- |
| `POST`   | `/consumers/<group>`                                | `application/vnd.kafka.v2+json`                |
| `POST`   | `/consumers/<group>/instances/<id>/subscription`    | `application/vnd.kafka.v2+json`                |
| `GET`    | `/consumers/<group>/instances/<id>/records`         | Accept: `application/vnd.kafka.binary.v2+json` |
| `POST`   | `/consumers/<group>/instances/<id>/commit-as-group` | `application/vnd.kafka.v2+json`                |
| `DELETE` | `/consumers/<group>/instances/<id>`                 | —                                              |

### Notes

- **Consumer instances are in-memory** — if the bridge pod restarts, recreate the consumer
- **Single bridge replica** — all consumer requests hit the same pod
- **Consumer group must start with `bridge-`** — ACL restriction
- **`auto.offset.reset: latest`** — start from newest events; use `earliest` for historical
- **`max.poll.records: 500`** — up to 500 records per poll