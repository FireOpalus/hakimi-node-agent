# hakimi-node-agent

哈基米境内独立执行节点代理（Python 3.12），部署于境内节点 `/opt/hakimi-node-agent/`，通过反向 WSS 专线连接境外主脑 `hakimi-surf`（`/ws/node/<path>`），提供：

- **B 站受控采集委派**（`bili_collector.py`）：公开接口读取、单请求态鉴权读取（零持久化 Cookie）、WBI 签名与 3×3 关键帧拼图兜底。
- **Minecraft 本地 WS 桥接槽**（`mc_bridge_slot.py`）：对接同私网 `hakimi-mc-agent`（`ws://hakimi-mc-agent:8791/ws`），双向转发快照、里程碑与目标指令。

## 本地测试与构建

```bash
uv sync
uv run ruff check .
uv run ruff format --check .
uv run pytest -q

docker build -t hakimi-node-agent:latest .
```

## 境内运行

```bash
cp .env.node.example .env.node
chmod 600 .env.node
docker compose -f compose.cn.yaml up -d
```
