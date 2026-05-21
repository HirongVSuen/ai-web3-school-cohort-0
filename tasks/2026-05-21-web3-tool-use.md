# 学习任务 - Web3 工具调用（Web3 Tool Use）

## 学习来源

- **Handbook**: https://aiweb3.school/zh/handbook/bridge/web3-tool-use/
- **前置**: https://aiweb3.school/zh/handbook/bridge/chain-aware-context/

## 学习路径

### 最小路径

阅读并理解以下知识节点：

1. **RPC Tool** — 只读 RPC vs 写入 RPC 隔离
   - 返回值需包含 chain id, RPC provider, block number, method, result, error
   - 写入能力必须拆成独立工具

2. **Contract Read** — view/pure 函数调用
   - 低风险但注意：网络错误、合约地址错误、ABI 不匹配、RPC 数据滞后
   
3. **Contract Write** — 改变链上状态
   - 前置检查：chain id, address, method, params, value, native balance, allowance, simulation
   - 限制在白名单合约 + 白名单方法

4. **Wallet Tool** — 连接/签名/发交易/授权
   - 分拆成独立动作，不混在"万能钱包工具"里

5. **Tool Permission** — 最小权限原则

### 实操映射（Rust/Rig）

| Handbook 概念 | Rig 实现 |
|---------------|----------|
| RPC Tool | Rig Tool trait → `get_eth_balance` |
| Contract Read | Rig Tool → `read_contract(address, abi, method, args)` |
| Contract Write | Rig Tool + human-in-the-loop |
| Wallet Tool | `rig-onchain-kit` + alloy 签名 |
| Tool Permission | 每个 Tool 独立 struct + 白名单校验 |

## 完成记录

- [ ] 已阅读 Web3 Tool Use 全文
- [ ] 已理解 RPC/Read/Write/Wallet/Defi Tool 的风险边界
- [ ] 已将概念映射到 Rig Tool trait 设计
- [ ] 已完成 Phase 0 环境验证
- [ ] 已编写 Rig Agent + 自定义 Tool
- [ ] 已打卡
