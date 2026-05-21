# 学习计划（更新版）

> 基于学员画像 + Rust/Rig/Arbitrum 技术栈 + 个人 Solo 路线
> 更新于 2026-05-20

## 技术栈定位

```
Rig (Rust Agent 框架) → rig-onchain-kit (EVM) → Arbitrum (L2)
```

## 推荐选题方向（Solo 友好）

1. **Agentic Payment Bot** — Agent 根据自然语言指令自动在 Arbitrum 上执行转账/支付
2. **On-chain 收据验证器** — Agent 执行任务后生成链上可验证收据
3. **AI Agent Wallet 仪表盘** — Agent 权限管理 + 交易审批流

---

## Phase 0: 环境搭建（Day 1~2）

- [ ] 确认 Rust 工具链（`rustup update`）
- [ ] 安装 Foundry（`curl -L https://foundry.paradigm.xyz | bash`）
- [ ] 创建 Rig 项目：`cargo init rig-agent && cargo add rig rig-onchain-kit`
- [ ] 配置 Arbitrum Sepolia 测试网 RPC（alchemy/infura）
- [ ] 创建测试钱包 + 领测试 ETH（Arbitrum Sepolia faucet）
- [ ] 验证：`cast balance <地址> --rpc-url <ARB_SEPOLIA_RPC>` 返回非零

---

## Week 1：AI + Web3 基础（跟共学营同步）

| 共学营内容 | Rust/Rig 对应实践 |
|-----------|------------------|
| LLM/Prompt/Agent | Rig Agent 创建 + Preamble + Prompt |
| Tool Calling | Rig 的 `Tool` trait 实现自定义工具 |
| 钱包/签名 | 用 `alloy` 或 `ethers-rs` 管理私钥和签名 |
| 智能合约 | Foundry + Solidity 写个简单合约 |
| 测试网 | 在 Arbitrum Sepolia 部署合约 |

**Week 1 练习：**
1. 用 Rig Agent 调用以太坊 RPC 查地址余额 → ✅
2. 写一个 Rig `Tool`：`get_eth_balance(address)` → ✅
3. 在 Arbitrum Sepolia 部署一个简单合约（比如 Counter） → ✅

**参考代码片段：**

```rust
use rig::providers::openai;
use rig::tool::Tool;

// 自定义工具：查链上余额
struct BalanceTool {
    rpc_url: String,
}

#[async_trait]
impl Tool for BalanceTool {
    // ... 实现 call 方法，调用 RPC 返回余额
}
```

---

## Week 2：AI × Web3 交叉方向

| 共学营内容 | Rust/Rig 对应实践 |
|-----------|------------------|
| Agentic Commerce / Payment | rig-onchain-kit EVM 交易 |
| Dev Tooling | 用 Rig 写 Dev Tool（自动化合约验证等） |
| Agent Wallet | Agent 持有私钥发起交易 |

**Week 2 练习：**
1. 用 `rig-onchain-kit` 让 Agent 发起一笔 ETH 转账 → ✅
2. Agent 根据自然语言指令（"Send 0.01 ETH to 0x..."）解析参数 → ✅
3. 实现 human-in-the-loop：交易前要求人工确认 → ✅
4. 探索方向，确定 Hackathon 选题 → ✅

**关键实现链路：**

```
用户输入 → Rig Agent (LLM 解析意图)
         → Tool: send_eth(amount, to)
         → human-in-the-loop 确认
         → alloy 签名 + 发送交易
         → 返回 tx_hash
```

---

## Week 3：实践深化 + Hackathon 启动

| 共学营内容 | Rust/Rig 对应实践 |
|-----------|------------------|
| 链上收据 | 交易后生成链上可验证收据 |
| Agent Workflow | 多步骤 Agent 工作流 |
| 治理/Gov | （可选）DAO 提案自动分析 |

**Week 3 行动：**
1. 完善 Agent 工作流：多工具链式调用 → ✅
2. 链上收据：交易后返回 tx_hash + block_number + 状态 → ✅
3. 确定 Hackathon 项目题目 + 技术架构 → ✅
4. 提交项目 proposal → ✅

**Solo 项目架构模板：**

```
rig-agent/
├── src/
│   ├── main.rs          # Agent 入口 + CLI
│   ├── tools/
│   │   ├── balance.rs   # 查余额工具
│   │   ├── transfer.rs  # 转账工具
│   │   └── receipt.rs   # 收据生成工具
│   ├── wallet.rs        # 私钥管理 + 签名
│   └── workflow.rs      # 多步骤工作流编排
├── contracts/           # Foundry 合约
├── Cargo.toml
└── README.md
```

---

## Week 4：Hackathon 集中开发

### Solo 策略（不组队的关键）

| 原则 | 说明 |
|------|------|
| **砍 scope** | 只做 1 个核心闭环，不做大而全 |
| **CLI 优先** | Rust 天然适合 CLI，比前端省 80% 时间 |
| **复用 Rig** | 用 Rig 生态的 Provider + Vector Store 省掉自建 |
| **README 即 demo** | 清晰的 README + 录屏/交易截图就够了 |

### 产出清单

- [ ] 核心功能闭环（Agent → 解析意图 → 链上执行 → 返回结果）
- [ ] 项目仓库 + 清晰的 README（问题、架构、用法、截图）
- [ ] 在 Arbitrum Sepolia 上的测试交易记录（tx_hash 可查）
- [ ] Demo 录屏 / 终端录制
- [ ] 提交到 WCB + GitHub

---

## 每日节奏

```
早 → 查看 WCB Learning 确认当日课程
学习 → Handbook + Rig 文档对照看
晚 → 写 Rust 代码 + daily note 打卡
```

## 关键资源

| 资源 | 链接 |
|------|------|
| Rig 文档 | https://docs.rig.rs |
| Rig Onchain Kit | https://github.com/0xPlaygrounds/rig-onchain-kit |
| Alloy（Rust EVM） | https://github.com/alloy-rs/alloy |
| Foundry 文档 | https://book.getfoundry.sh |
| Arbitrum 文档 | https://docs.arbitrum.io |
| Arbitrum Sepolia Faucet | https://faucet.quicknode.com/arbitrum/sepolia |

## 避坑提醒

1. **Rig 还在快速迭代** — 锁版本号，不要追最新
2. **Solo 别做前端** — CLI 够用，Hackathon 评委看的是想法和执行
3. **测试网 token** — 多囤一点，避免做到一半没 Gas
4. **Foundry 的 `cast` + `forge`** — 是你调试合约的瑞士军刀
