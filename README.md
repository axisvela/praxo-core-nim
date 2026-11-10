# PRAXO-CORE for Nim

Native Nim Core for the PRAXO-CORE agent framework. This repository is the
Nimble/nimpkgs source package; the main contract and cross-language sources live
in [axisvela/praxo-core](https://github.com/axisvela/praxo-core).

- `SPEC_VERSION`: `0.2.0`
- Core version: `0.1.1`
- Package: `praxo_core`
- Import: `import praxo`
- License: MIT

## Install

```bash
nimble install praxo_core
```

## Scope

The Core implements all eleven conformance vector groups: toolcall, JSON Schema,
plugin, memory, event, stream, checkpoint, policy, context, middleware, and the
agent loop. It includes the native agent loop, context compaction, memory store,
path policy, checkpoint allowlist, tool-call parsing, and opt-in tool selection,
PII redaction, structured output, and call limits.

The Core does not call Go or another language runtime. It includes an optional
OpenAI-compatible model adapter; other provider adapters and plugin hosts remain
outside the declared Core scope.

## OpenAI-Compatible Model

```nim
let adapter = newOpenAICompatible(
  baseUrl = "https://api.openai.com/v1",
  model = "gpt-4o-mini",
  apiKey = getEnv("PRAXO_API_KEY"),
)
let model = openaiModel(adapter)
let result = runAgent(newAgentOptions(model), newSession("s1"), "Hi")
```

The adapter uses non-streaming `POST /chat/completions`, maps tool calls and
usage, and accepts an injected transport for deterministic tests.

## API

```nim
import praxo

let call = parseToolCall("""<tool_call name="echo">{"text":"hi"}</tool_call>""")
assert call.isSome
assert call.get().name == "echo"
```

## Links

- Main repository: https://github.com/axisvela/praxo-core
- Nim documentation: https://axisvela.github.io/praxo-core/languages/nim/
