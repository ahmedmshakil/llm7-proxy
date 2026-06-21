# llm7-proxy

A proxy for [LLM7.io](https://github.com/chigwell/llm7.io) — an OpenAI-compatible API provider. This proxy exposes a local OpenAI-compatible endpoint that forwards requests to LLM7 via the OpenAI Python SDK.

It uses the OpenAI Python SDK with `base_url` pointed at LLM7:

```txt
Codex app -> /v1/responses -> local proxy -> OpenAI SDK -> LLM7
```

## Setup

Requires Python 3.10+.

1. Install requirements:

```bat
python -m pip install -r requirements.txt
```

2. Add this to your Codex `config.toml`:

```toml
model_provider = "llm7proxy"
model = "gpt-5.5"

[model_providers.llm7proxy]
name = "LLM7 Python Proxy"
base_url = "http://127.0.0.1:5011/v1"
env_key = "LLM7_API_KEY"
wire_api = "responses"
request_max_retries = 2
stream_max_retries = 2
stream_idle_timeout_ms = 300000
```
On Linux/macOS, the config is usually:

```txt
~/.codex/config.toml
```
On Windows, the config is usually:

```txt
C:\Users\YOUR_USERNAME\.codex\config.toml
```


The same config block is also saved in `llm7-proxy.config.toml`.

3. Start the proxy and keep this terminal open:


**Linux / macOS:**

```sh
export LLM7_API_KEY=unused
python llm7_proxy.py
```

**Windows:**

```bat
set LLM7_API_KEY=unused
python llm7_proxy.py
```

Use a real LLM7 key for better limits:


**Linux / macOS:**

```sh
export LLM7_API_KEY=your_real_key_here
python llm7_proxy.py
```

**Windows:**

```bat
set LLM7_API_KEY=your_real_key_here
python llm7_proxy.py
```

Get a key from:

```txt
https://dash.llm7.io/
```

4. Launch or restart the Codex app.

You are ready to use Codex through the LLM7 proxy.

## Endpoints

```txt
GET  /health
GET  /v1/models
POST /v1/chat/completions
POST /v1/responses
```

The local server runs at:

```txt
http://127.0.0.1:5011
```

## Author

**Shakil Ahmed**

* LinkedIn: [@ahmedmshakil](https://www.linkedin.com/in/ahmedmshakil/)
* GitHub: [@ahmedmshakil](https://github.com/ahmedmshakil)
