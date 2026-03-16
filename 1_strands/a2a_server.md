## StrandsのA2Aサーバー最小サンプルコード

### 1. 基本的な最小サンプル

```python
import logging
from strands import Agent
from strands.multiagent.a2a import A2AServer

# ログ設定
logging.basicConfig(level=logging.INFO)

# Strandsエージェントを作成
agent = Agent(
    name="Hello Agent",
    description="シンプルな挨拶エージェント",
    callback_handler=None
)

# A2Aサーバーを作成
a2a_server = A2AServer(agent=agent)

# サーバーを開始
a2a_server.serve()
```

### 2. ツールを使った実用的なサンプル

```python
import logging
from strands_tools.calculator import calculator
from strands import Agent
from strands.multiagent.a2a import A2AServer

# ログ設定
logging.basicConfig(level=logging.INFO)

# 計算機能を持つStrandsエージェントを作成
strands_agent = Agent(
    name="Calculator Agent",
    description="基本的な算術演算を実行できる計算エージェント",
    tools=[calculator],
    callback_handler=None
)

# A2Aサーバーを作成（デフォルトでストリーミング有効）
a2a_server = A2AServer(agent=strands_agent)

# サーバーを開始
a2a_server.serve()
```

### 3. カスタム設定付きサンプル

```python
import logging
from strands import Agent
from strands.multiagent.a2a import A2AServer

logging.basicConfig(level=logging.INFO)

# エージェントを作成
agent = Agent(
    name="My Custom Agent",
    description="カスタマイズされたエージェント",
    callback_handler=None
)

# カスタム設定でA2Aサーバーを作成
a2a_server = A2AServer(
    agent=agent,
    host="0.0.0.0",  # すべてのインターフェースでリッスン
    port=8080,       # カスタムポート
    version="1.0.0"  # バージョン指定
)

# サーバーを開始
a2a_server.serve(app_type="fastapi")  # FastAPIを使用
```

### 4. 実行方法

1. **必要なパッケージをインストール:**
```bash
pip install strands-agents[a2a]
pip install strands-agents-tools  # ツールを使用する場合
```

2. **上記のコードをファイル（例：`a2a_server.py`）に保存**

3. **サーバーを実行:**
```bash
python a2a_server.py
```

### 主な特徴

- **デフォルト設定**: `host="127.0.0.1"`, `port=9000`
- **自動ストリーミング対応**: `SendMessageRequest`と`SendStreamingMessageRequest`の両方をサポート
- **A2A準拠**: Agent-to-Agentプロトコル標準に完全対応
- **簡単な設定**: 最小限のコードでA2Aサーバーを立ち上げ可能

このサンプルコードを使って、他のA2A対応エージェントと通信できるサーバーを簡単に作成できます