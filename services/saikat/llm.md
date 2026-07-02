# Self hosted LLM

## Details
URL: https://saikat-llm-general.yral.com
Model: Qwen/Qwen3.6-35B-A3B-FP8
Bearer Token: `Bearer <secret_value>`. Secret available in vault [here](https://vault.yral.com/ui/vault/secrets/secret/kv/SAIKAT_LLM_GENERAL)

The server supports
- completion API
- responses API
- messages API

Choose what you need:

## APIs available

GET
/load
Get Server Load Metrics


GET
/version
Show Version


GET
/health
Health


GET
/metrics
Metrics


POST
/tokenize
Tokenize


POST
/detokenize
Detokenize


GET
/v1/models
Show Available Models


GET
/ping
Ping


POST
/ping
Ping


POST
/invocations
Decorated Func


POST
/v1/chat/completions
Create Chat Completion


POST
/v1/chat/completions/batch
Create Batch Chat Completion


POST
/v1/responses
Create Responses


GET
/v1/responses/{response_id}
Retrieve Responses


POST
/v1/responses/{response_id}/cancel
Cancel Responses


POST
/v1/completions
Create Completion


POST
/v1/messages
Create Messages


POST
/v1/messages/count_tokens
Count Tokens


POST
/generative_scoring
Create Generative Scoring


POST
/inference/v1/generate
Generate


POST
/scale_elastic_ep
Scale Elastic Ep


POST
/is_scaling_elastic_ep
Is Scaling Elastic Ep


POST
/v1/chat/completions/render
Render Chat Completion


POST
/v1/completions/render
Render Completion 