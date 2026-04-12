---
name: mywant-ngrok-plugin
description: ngrokを使ってローカルサービスをパブリックURLで公開するMyWant want typeプラグイン。ngrokが使える環境でローカルサービスを外部公開したいときに使用する。built-in live_server_management エージェントを使用するためスクリプトは不要。
compatibility:
  requires:
    - ngrok (in PATH)
    - MyWant server running
metadata:
  output-format: agent-based
  note: This plugin is agent-based and does not output JSON directly. It uses the MyWant live_server_management agent.
---

## 使い方

MyWant want typeとして使用する（直接スクリプト実行はなし）:

```yaml
metadata:
  name: expose-local-service
  type: ngrok
spec:
  params:
    port: 8080
```

または CLI で:

```bash
mywant wants create -t ngrok
```

> **Note**: このプラグインは `live_server_management` エージェントベースであり、
> `main.py` による JSON 出力は行わない。Machine Readable Skills の `main.py` 要件は非該当。

## 出力JSON形式

このプラグインはスクリプト実行ではなくエージェントベースのため、JSON stdout 出力なし。
MyWant の want state に公開URLが `public_url` として格納される。

### フィールド説明

| フィールド | 型 | 説明 |
|---|---|---|
| `public_url` | string | ngrokで発行されたパブリックURL（want stateに格納） |

### エラー時

```json
{ "error": "agent-based plugin — no script error output" }
```
