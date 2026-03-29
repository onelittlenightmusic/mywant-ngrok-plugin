# mywant-ngrok

A [MyWant](https://github.com/onelittlenightmusic/mywant) plugin that adds the **Ngrok Tunnel** recipe.

Exposes a local service via a public URL using ngrok.
Uses the built-in `managed_process` want type under the hood.

## Requirements

- [MyWant](https://github.com/onelittlenightmusic/mywant) installed and running
- [ngrok](https://ngrok.com/download) installed and available in `PATH`

## Installation

```sh
cd ~/.mywant/recipes
git clone https://github.com/onelittlenightmusic/mywant-ngrok-plugin
```

The recipe is loaded automatically on next server start, or register it without restart:

```sh
mywant recipes create -f ~/.mywant/recipes/mywant-ngrok-plugin/ngrok.yaml
```

## Usage

```sh
# List available recipes (confirm "Ngrok Tunnel" appears)
mywant recipes list

# Deploy with default port 8080
mywant wants create --recipe "Ngrok Tunnel"

# Deploy with custom port
mywant wants create --recipe "Ngrok Tunnel" -p port=3000
```

## Update

```sh
cd ~/.mywant/recipes/mywant-ngrok-plugin && git pull
```

## Parameters

| Name | Default | Description |
|------|---------|-------------|
| `port` | `"8080"` | Local port to expose |
| `protocol` | `"http"` | Protocol (http, tcp, tls) |
| `command` | `"ngrok"` | Path to ngrok binary |
| `args` | `'["http","8080","--log","stdout"]'` | CLI arguments (JSON array) |
| `max_retries` | `30` | Max retries waiting for URL |
| `log_file` | `""` | Path to capture stdout (auto if empty) |
