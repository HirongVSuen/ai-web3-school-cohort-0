# 学习任务 - 链感知上下文 Chain-aware Context

## 今日学习路径

**来源**: https://aiweb3.school/zh/handbook/bridge/chain-aware-context/

### Recommended Path（最小路径）

阅读并理解以下核心知识节点：

1. **On-chain Data** — 链上数据如何进入 Agent 上下文
   - 关键字段：chain id、block number、contract address、method、返回值、读取时间
   - 常见来源：RPC、区块浏览器、索引器、协议 API

2. **Contract Docs** — 合约文档如何补足 ABI 的语义缺口
   - ABI 只有函数签名，NatSpec/README/审计报告解释业务语义
   - 文档可能过期，需用链上数据验证

3. **ABI / Event** — 合约可调用能力和历史行为
   - 能调用 ≠ 应该调用，写交易前需权限/余额/slippage/simulation 检查

### Hands-on 建议

- 打开 Etherscan 找一个合约，查看其 ABI 和事件日志
- 用 curl 或 viem 读取一个地址的 ETH 余额和交易历史
- 写一个简单脚本，把 chain id + block number + 余额数据格式化成 Agent 可读的 context block

### 挑战路径

- 实现一个函数，自动从链上获取合约 owner 并验证合约版本是否匹配文档描述

## 完成记录

- [ ] 已阅读 Chain-aware Context 全文
- [ ] 已完成链上数据读取练习
- [ ] 已将学习心得写入 daily note
- [ ] 已打卡

## 2026-05-19 进展

今日计划：阅读 Chain-aware Context 全部知识节点 + 完成最小实践。
