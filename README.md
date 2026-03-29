# mywant-ngrok

A [MyWant](https://github.com/onelittlenightmusic/MyWant) plugin that adds the **Ngrok Tunnel** want type.

Exposes a local service via a public URL using ngrok.
Uses the built-in `live_server_management` agent under the hood.

## Requirements

- [MyWant](https://github.com/onelittlenightmusic/MyWant) installed and running
- [ngrok](https://ngrok.com/download) installed and available in `PATH`

## Installation

```sh
git clone https://github.com/onelittlenightmusic/mywant-ngrok-plugin \
  ~/.mywant/custom-types/mywant-ngrok-plugin
```

Then restart MyWant (`make restart-all` or `./bin/mywant stop && ./bin/mywant start -D`).

## Usage

```sh
# List available want types (confirm "ngrok" appears)
mywant types list

# Deploy with default port 8080
mywant wants create -t ngrok

# Deploy with custom args
mywant wants create -t ngrok -p args='["http","3000","--log","stdout"]'
```

## Parameters

| Name | Default | Description |
|------|---------|-------------|
| `port` | `"8080"` | Local port to expose |
| `args` | `'["http","8080","--log","stdout"]'` | CLI arguments (JSON array) |
| `command` | `"ngrok"` | Path to ngrok binary |
| `url_regex` | `(?:Forwarding\s+\|url=)(https?://\S+)` | Regex to extract forwarding URL |
| `max_retries` | `30` | Max retries waiting for URL |
| `log_file` | `""` | Path to capture output (auto if empty) |

## State

After the want is achieved, the tunnel URL is available as:

- `current.server_url` — the forwarding URL
- `final_result` — same value, for use with `using` selectors
