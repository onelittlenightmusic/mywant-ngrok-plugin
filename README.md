# mywant-ngrok

A [MyWant](https://github.com/onelittlenightmusic/mywant) plugin that adds the `ngrok` want type.

Manages an ngrok tunnel lifecycle to expose a local service via a public URL.
Automatically starts the ngrok process, parses the forwarding URL from stdout, and stores it in state.

## Requirements

- [MyWant](https://github.com/onelittlenightmusic/mywant) installed and running
- [ngrok](https://ngrok.com/download) installed and available in `PATH`

## Installation

```sh
mkdir -p ~/.mywant/custom-types
curl -o ~/.mywant/custom-types/ngrok.yaml \
  https://raw.githubusercontent.com/onelittlenightmusic/mywant-ngrok-plugin/main/ngrok.yaml
```

Or manually copy `ngrok.yaml` to `~/.mywant/custom-types/`.
The type is loaded automatically on next server start, or register it without restart:

```sh
mywant types create -f ~/.mywant/custom-types/ngrok.yaml
```

## Usage

```yaml
metadata:
  name: my-tunnel
  type: ngrok
spec:
  params:
    port: "3000"
```

```sh
mywant wants create -f my-tunnel.yaml
```

## Parameters

| Name | Type | Default | Description |
|------|------|---------|-------------|
| `port` | string | `"8080"` | Local port to expose |
| `protocol` | string | `"http"` | Protocol (http, tcp, tls) |
| `command` | string | `"ngrok"` | Path to ngrok binary |
| `args` | string | `'["http","8080","--log","stdout"]'` | CLI arguments (JSON array) |
| `max_retries` | int | `30` | Max retries waiting for URL |
| `log_file` | string | `""` | Path to capture stdout (auto if empty) |
