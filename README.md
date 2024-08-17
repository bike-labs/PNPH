# PNPH

![GitHub commit activity (branch)](https://img.shields.io/github/commit-activity/w/bike-labs/PNPH/main?style=flat-square)
![GitHub Repo stars](https://img.shields.io/github/stars/bike-labs/PNPH?style=flat-square)

## 项目概述

此项目介绍了一种新的去中心化 prover market 机制，旨在让 layer2 上的用户可以用更低的费用去提交 transactions。这个新机制最大优点是，每个 user 的 tx 都会被尽可能的生成相应的证明。而不会因为 bid 价钱不够而被无限期延后。

### 1. =Nil;

- **机制简介**：
  - **订单簿机制**：=Nil; 提供了一个市场，用户可以通过订单簿提交他们对特定电路的证明需求，而证明者则提交提供这些证明的报价。当需求和报价匹配时，交易达成，用户支付费用，证明者生成并提交证明。
- **优缺点**：
  - **优点**：订单簿机制能够灵活适应不同用户的需求和不同证明者的报价，使价格发现过程透明且市场化。
  - **缺点**：复杂的订单簿机制对用户和证明者都可能有一定的理解和操作门槛，市场可能需要高频率的参与才能保持流动性。
- **是否涉及 Prover 市场**：是，=Nil;通过订单簿机制直接涉及并管理证明者市场，调节用户需求和证明者供给。

### 2. Mina

- **机制简介**：
  - **证明生成与交易**：Mina 的区块生产者可以选择自己生成交易的证明，或者从市场中的 SNARK 工作者（证明者）购买证明。交易费用由用户在交易时设定，区块生产者选择交易并支付相应的费用给证明者。
- **优缺点**：
  - **优点**：Mina 通过 ZK-SNARK 大大减小了区块链的存储和验证负担，使得全节点的成本极低。
  - **缺点**：Mina 并没有详细描述如何形成一个有效的证明者市场，尤其是在证明者之间的竞争和价格发现方面缺乏机制设计。
- **是否涉及 Prover 市场**：部分涉及，虽然 Mina 有证明者参与，但缺乏明确的市场机制设计，证明者市场未被充分开发。

### 3. Aztec

- **机制简介**：
  - **并行证明与聚合**：Aztec 允许不同的证明者同时生成多个证明，最终这些证明会被聚合并提交到 Layer 1。Aztec 还提议通过 Sidecar 机制来协调证明者的工作，Sequencer 可以选择自己生成证明或将证明任务外包给其他证明者。
- **优缺点**：
  - **优点**：通过并行证明和聚合机制，Aztec 提升了系统的效率，允许处理更多的交易。
  - **缺点**：并行处理和聚合的复杂性可能增加协调的难度，特别是在不同证明者的证明时间和质量不一致时。
- **是否涉及 Prover 市场**：是，Aztec 通过 Sidecar 机制和并行处理直接涉及 Prover 市场，并努力创建一个去中心化的证明者市场。

### 4. Taiko

- **机制简介**：
  - **PoS 与随机选择**：Taiko 通过 PoS（权益证明）协议和随机选择机制来选择证明者。证明者根据其提供的每单位 gas 的价格、证明能力和抵押金额来确定其被选中的概率。选中的证明者负责处理分配的区块，并在规定时间内完成证明生成。
- **优缺点**：
  - **优点**：通过 PoS 和随机选择机制，Taiko 减少了中心化的风险，并通过 EIP-1559 类机制平衡了用户费用和证明者奖励。
  - **缺点**：证明者的选择过程较为复杂，可能导致不公平的费用分配，特别是当不同证明者的成本和能力差异较大时。
- **是否涉及 Prover 市场**：是，Taiko 的机制直接涉及并管理 Prover 市场，通过复杂的选择和激励机制维持市场的竞争性和公平性。

### 5. Scroll

- **机制简介**：
  - **PSS（证明者-排序器分离）**：Scroll 提出了 PSS 机制，将证明者和 Sequencer 的角色分离。一个 PoS 协议在证明者之间运行，并在每个区块中选择一个证明者。Sequencers 负责构建区块并最大化交易价值。用户支付的费用通过第一价格拍卖决定，证明者根据自己的竞价获得任务。
- **优缺点**：
  - **优点**：Scroll 通过 PSS 机制确保了更公平的证明者选择，并允许 Sequencer 优化区块构建，同时第一价格拍卖机制提高了市场的效率。
  - **缺点**：PSS 机制和支付拍卖的复杂性可能增加实现难度，同时也存在证明者和 Sequencer 合谋的风险。
- **是否涉及 Prover 市场**：是，Scroll 明确涉及 Prover 市场，通过第一价格拍卖和 PSS 机制管理证明者的选择和激励。

### 6. Starknet

- **机制简介**：
  - **费用机制与去中心化探索**：Starknet 的当前交易费用是基于 Layer 1 的成本估算，交易按先到先得的顺序处理。Starknet 正在探索去中心化 Sequencer 和证明者网络，虽然还没有具体的协议，但方向上正在逐步完善。
- **优缺点**：
  - **优点**：ZK-STARK 技术提供了更高的效率和可扩展性，Starknet 也在努力推动网络的去中心化。
  - **缺点**：现有的费用机制相对简单，未能充分反映 Layer 2 的复杂市场需求，去中心化尝试还处于初步阶段。
- **是否涉及 Prover 市场**：部分涉及，虽然 Starknet 有去中心化探索的意图，但其机制设计还未深入涉及如何管理和激励 Prover 市场。

### 7. Gevulot

- **机制简介**：
  - **去中心化与随机分配**：Gevulot 是一个完全去中心化的区块链，其证明者通过 VRF（可验证随机函数）随机分配证明任务。证明者需要通过抵押和完成工作量证明任务来加入网络。Gevulot 还设计了计算返利机制，激励证明者尽快提交证明。
- **优缺点**：
  - **优点**：Gevulot 通过去中心化和随机分配机制，确保了公平性，计算返利机制也有效激励了证明者的高效工作。
  - **缺点**：计算返利机制增加了系统复杂性，随机分配可能在某些情况下影响效率，特别是在需要快速响应时。
- **是否涉及 Prover 市场**：是，Gevulot 深入涉及了 Prover 市场，通过随机分配和计算返利机制管理和激励证明者。

## [OP4] 证明者市场设计

- 比较并选择证明者市场框架的设计目标。
- 设计具体的证明者市场，即如何找到
  `<InputSet, OutputSet, Input, Output, Usage>`
- 你可以参考 Web2 广告竞拍算法。
- 分析不同证明者市场的理想特性。这些特性是否无法同时满足？
  - 效率
  - 激励兼容性
  - 证明者的合谋抵抗性
  - 链下协议的防范性

| 机制            | 用户支付方式                | 证明者选择方式     | 支付给证明者的费用             |
| --------------- | --------------------------- | ------------------ | ------------------------------ |
| Prooφ           | 第一价格拍卖                | 张贴价格和彩票机制 | 平均用户费用 × 分配的容量      |
| =Nil;           | 订单簿                      | 订单簿             | 订单簿价格                     |
| Mina            | 第一价格拍卖                | 与 Sequencer 相同  | 未明确规定，由区块生产者决定   |
| Aztec (Sidecar) | 未明确说明                  | 与 Sequencer 相同  | 未明确规定                     |
| Taiko           | 类似 EIP-1559 机制          | PoS 和加权随机选择 | 证明者自行决定的价格           |
| Scroll          | 第一价格拍卖                | PoS 协议选择       | Sequencer 通过第一价格拍卖决定 |
| Starknet        | 基于 Layer 1 发布的估算费用 | 未明确说明         | 未明确说明                     |
| Gevulot         | 预先支付                    | VRF 随机选择       | 预先支付费用，附带折扣返还     |
|                 |                             |                    |                                |

## 用户支付方式的优缺点

- 第一价格拍卖
  - 卖方主导，买方出价，有损买方利益。
- order book
  - 存在压单，执行不了的问题，是双方自主博弈价格。
- EIP1559
  - burn 费用，不合适

## 证明者激励机制优缺点

- PoS 机制
  - PoS 机制要求你质押一定的代币，才能成为证明者，质押的越多，被选中成为证明者的概率越大
  - 这能防止恶意证明者，但是不应该是质押的越多，被选中的概率越大，而是质押一定数额就获得名额。同时 PoS 是会存在提高用户成本，以及富者恒富

## 我们的目标

设计目标，用户是傻子。

- 价格因素
  - 用户 sequencer
    - Circut size （demand）电路门大小，复杂度
    - tips 紧急度 加钱。
  - Prover
    - minUnitPrice 报价，最低算力单价 → 网络抖动问题
    - averageUnitPrice 报价，平均报价 → 解决网络抖动，平均报价是根据，目前有空闲的最活跃的 n 个节点的历史报价给出平均费率。

      $\text{TotalPrice} = (\text{averageUnitPrice}+ \text{tips}) \times \text{circutSize}$

      问题：单个 prover 价格过低，吃掉太多的利润
      
      p1: power 1, money1;
      
      p2:power2, money2;
      
      **算力=单位时间内能解决的问题数**
- 匹配机制
  - 算力剩余要满足 User 需要的算力

    $\text{Power} _ \text{Prover} > \text{Demand} _ \text{User}$

  - 用户报价，从高到低，高的优先处理，低的会根据 first in first serve，在截止时间前会强行派单。
  - prover 排序，按照报价从低到高排序，低的优先接单。
  - **第二优先级是价格，可以作为启动因素。**
- 冷却机制/惩罚机制
  - prover 需要质押/交保证金来成为 prover。质押的金额要根据你的算力。根据你的算力大小成正比。 $\text{stakedPrice} = k \cdot \text{Capability}$
  - 每次没按时完成任务，会扣一部分押金，暂定 $\frac{1}{5}$ 押金。类似于扣信用分。
- 优先级排序
