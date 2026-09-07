<p align="center">
  <a href="https://github.com/runapi-ai/glm">
    <h3 align="center">GLM API Skill for RunAPI</h3>
  </a>
</p>

<p align="center">
  Configure OpenAI-compatible clients to use GLM models on RunAPI.
</p>

<p align="center">
  <a href="https://runapi.ai/models/glm"><strong>Model Reference</strong></a> | <a href="https://github.com/runapi-ai/glm"><strong>Skill Repo</strong></a> | <a href="https://runapi.ai/models"><strong>All Models</strong></a>
</p>

<div align="center">

[![skills.sh](https://www.skills.sh/b/runapi-ai/glm)](https://www.skills.sh/runapi-ai/glm/glm)
[![ClawHub](https://img.shields.io/badge/ClawHub-runapi--glm-111827)](https://clawhub.ai/runapi-ai/runapi-glm)
[![License](https://img.shields.io/github/license/runapi-ai/glm)](https://github.com/runapi-ai/glm/blob/main/LICENSE)

</div>
<br/>

Call the GLM API through RunAPI with the official OpenAI SDK or any
OpenAI-compatible client. Point clients at `https://runapi.ai/v1`, send
`glm-5.3`, `glm-5.2`, `glm-5.1`, `glm-5-turbo`, `glm-5`, `glm-4.7`, `glm-4.6`,
`glm-4.5`, or `glm-4.5-air`, and pay through one RunAPI balance. This skill
teaches Claude Code, Codex, Gemini CLI, Cursor, and 50+ agents how to wire GLM
requests through RunAPI.

The canonical agent file is `skills/glm/SKILL.md`.

## Install the skill

```bash
npx skills add runapi-ai/glm -g
```

Or paste this prompt to your AI agent:

```text
Install the glm skill for me:

1. Clone https://github.com/runapi-ai/glm
2. Copy the skills/glm/ directory into your
   user-level skills directory (e.g. ~/.claude/skills/
   for Claude Code, ~/.codex/skills/ for Codex).
3. Verify that SKILL.md is present.
4. Confirm the install path when done.
```

## Use GLM on RunAPI

```python
from openai import OpenAI

client = OpenAI(
    api_key="YOUR_RUNAPI_TOKEN",
    base_url="https://runapi.ai/v1",
)

response = client.chat.completions.create(
    model="glm-5.3",
    messages=[{"role": "user", "content": "Hello, GLM!"}],
)
print(response.choices[0].message.content)
```

```javascript
import OpenAI from "openai";

const client = new OpenAI({
  apiKey: "YOUR_RUNAPI_TOKEN",
  baseURL: "https://runapi.ai/v1",
});

const response = await client.chat.completions.create({
  model: "glm-4.6",
  messages: [{ role: "user", content: "Hello, GLM!" }],
});
console.log(response.choices[0].message.content);
```

Get a RunAPI API Key at <https://runapi.ai/api_keys>.

## Supported GLM models

| Model ID | Notes |
|---|---|
| `glm-5.3` | Latest text workloads through Chat Completions |
| `glm-5.2` | Cross-protocol flagship text workloads |
| `glm-5.1` | Latest GLM chat workloads |
| `glm-5-turbo` | Faster GLM chat |
| `glm-5` | General GLM 5 requests |
| `glm-4.7` | GLM 4.7 compatibility |
| `glm-4.6` | Stable GLM 4.6 requests |
| `glm-4.5` | GLM 4.5 compatibility |
| `glm-4.5-air` | Lightweight GLM 4.5 requests |

## GLM-5.3 capability contract

| Capability | Current behavior |
|---|---|
| Text history, sync, streaming | Supported through OpenAI-compatible Chat Completions |
| OpenAI Responses, Anthropic Messages, Gemini contents | Not supported for `glm-5.3` |
| Tools, reasoning controls, structured output, multimodal input | Not declared pending model-specific evidence |
| Usage | Returned input, output, and cache token details are preserved and never inferred |

## GLM-5.2 capability contract

| Capability | Current behavior |
|---|---|
| Text history, sync, streaming | Supported across Chat, Responses, Messages, and Gemini-compatible requests |
| Default thinking | Disabled for consistent cross-protocol output |
| Reasoning controls/content, function tools/history, structured output | Rejected with `unsupported_model_capability` pending model readiness |
| Hosted tools, explicit cache controls, stateful continuation, protocol-specific controls | Rejected; RunAPI does not currently expose the required protocol surface |
| Cache/reasoning Usage | Preserved when returned and never inferred; Messages does not expose a caller-visible reasoning-token breakdown |
| Context window | Estimated input above 1000000 tokens returns `model_limit_exceeded`; full-window execution remains readiness-gated |
| Maximum output | Values up to 131072 are accepted; larger values return `model_limit_exceeded` before request execution |
| Multimodal input | Rejected with `unsupported_model_capability` |

The model's 1M context envelope is not a RunAPI execution guarantee. Full-window
execution remains subject to published readiness.

## Routing

- GLM API on RunAPI: <https://runapi.ai/models/glm>
- Provider page: <https://runapi.ai/providers/z-ai>
- Browse the full RunAPI catalog: <https://runapi.ai/models>
- Skill repository: <https://github.com/runapi-ai/glm>

## Agent rules

- Keep API keys in `OPENAI_API_KEY` or your secret manager; never inline them in
  commits or shell history.
- Stream long responses (`stream: true`) so the agent can release the
  terminal/IO loop early.
- Keep `glm-5.3` requests on OpenAI-compatible Chat Completions with text
  history. Use an advanced feature or another protocol only when the
  model-specific capability table marks it ready.
- Treat cache and reasoning Usage as response facts. Never infer missing token
  details or assume a cache discount.
- For pricing, rate-limit, and commercial-usage answers, link to
  <https://runapi.ai/models/glm> rather than this README.

## License

Licensed under the Apache License, Version 2.0.
