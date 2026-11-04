# mermaid

https://www.runoob.com/markdown/md-draw.html

https://mermaid.js.org/syntax/flowchart.html#an-open-link

```mermaid
sequenceDiagram
autonumber
    participant A as 用户
    participant B as 系统
    participant C as 数据库

    A->>B: 登录请求
    B->>C: 验证用户信息
    C-->>B: 返回验证结果
    B-->>A: 登录成功/失败
```

```mermaid
graph TD
    A((开始)) --> B{条件判断}
    B -->|Yes| C[执行操作A]
    B -->|No| D(执行操作B)
    C --> E((结束))
    D --> E
```

```mermaid
flowchart LR
    A-->B
    C---D
    E-- This is the text! ---F
    G-->|text|H
    I-- text -->J
    K-.->L
    M-. text .-> N
    O ==> P
    Q == text ==> R
    S ~~~ T
    X -- text --> Y -- text2 --> Z
    a --> b & c--> d
    e & f--> g & h
    i e1@==> j
    e1@{ animate: true }
    k e2@--> l
    e2@{ animation: fast }
    m e3@-->n
    classDef animate stroke-dasharray: 9,5,stroke-dashoffset: 900,animation: dash 25s linear infinite;
    class e3 animate

    A1 --o B1
    A2 --x B2
    A3["A double quote:#quot;"] --> B3["A dec char:#9829;"]
```

```mermaid
---
config:
  flowchart:
    curve: linear
---
flowchart TD
    A[Start] --> B{Is it?}
    B -->|Yes| C[OK]
    C --> D[Rethink]
    D --> B
    B ---->|No| E[End]

```

```mermaid
flowchart TD
    A[Start] --> B{Is it?}
    B -- Yes --> C[OK]
    C --> D[Rethink]
    D --> B
    B -- No ----> E[End]

```

## 形状

```mermaid
flowchart
%% 矩形
A[方形]
%% 圆角矩形
B(圆角矩形)
%%菱形（决策）
C{菱形}
%%圆形
D((圆形))
%%旗帜形
E>旗帜形]
```

## 流程图方向

TD 或 TB：从上到下
BT：从下到上
RL：从右到左
LR：从左到右

## 虚线直线

| Length            |   1    |    2    |    3     |
| :---------------- | :----: | :-----: | :------: |
| Normal            | `---`  | `----`  | `-----`  |
| Normal with arrow | `-->`  | `--->`  | `---->`  |
| Thick             | `===`  | `====`  | `=====`  |
| Thick with arrow  | `==>`  | `===>`  | `====>`  |
| Dotted            | `-.-`  | `-..-`  | `-...-`  |
| Dotted with arrow | `-.->` | `-..->` | `-...->` |

```mermaid
flowchart LR
  subgraph TOP
    direction TB
    subgraph B1
        direction RL
        i1 -->f1
    end
    subgraph B2
        direction BT
        i2 -->f2
    end
  end
  A --> TOP --> B
  B1 --> B2

```

## 直线曲线

| 值                         | 效果         |
| -------------------------- | ------------ |
| `linear`                   | 直线         |
| `stepAfter` / `stepBefore` | 直角折线     |
| `basis`                    | 平滑曲线     |
| `cardinal`                 | 更柔和的曲线 |

```mermaid
---
config:
  flowchart:
    curve: linear
---
flowchart LR
    subgraph subgraph1
        direction TB
        top1[top] --> bottom1[bottom]
    end
    subgraph subgraph2
        direction TB
        top2[top] --> bottom2[bottom]
    end
    %% ^ These subgraphs are identical, except for the links to them:

    %% Link *to* subgraph1: subgraph1 direction is maintained
    outside --> subgraph1
    %% Link *within* subgraph2:
    %% subgraph2 inherits the direction of the top-level graph (LR)
    outside ---> top2

```

```mermaid
---
config:
  flowchart:
    curve: stepBefore
---
graph LR
A e1@==> B
    A e2@--> C
    e1@{ curve: linear }
    e2@{ curve: natural }
```

```mermaid
flowchart LR
    A:::someclass --> B
    classDef someclass fill:#f96

     A1:::foo & B1:::bar --> C1:::foobar
    classDef foo stroke:#f00
    classDef bar stroke:#0f0
    classDef foobar stroke:#00f
```

# 实例

```mermaid
---
config:
  flowchart:
    curve: linear
---
flowchart TB
A("患者")
B("医生")
C("管理员")
E("查看问诊记录")
F("维护药品")
Case1("1")
Case2("2")
Case3("3")
Case4("4")
Case5("5")
Case6("6")
Case7("7")
Case8("8")
A --> Case1 & Case2 & Case3 & E
Case2 -.9.-> E
B --> Case4 & Case5 & Case6 & F
Case4 -.10.-> Case5
Case4 -.11.-> F
C --> Case7 & Case8
```

```mermaid
sequenceDiagram
  autonumber
  participant A as 患者
  participant B as 问诊界面
  participant C as 诊断控制
  participant D as 医生服务
  participant E as 医生
  participant F as 患者App
  participant G as 消息队列
  participant H as 汇总程序
  A->>B: 选择医生
  B->>C: 提交选医请求
  C->>D: 查询医生信息
  D-->>C: 返回医生列表
  C-->>B: 显示医生详情
  A->>B: 提交病情描述
  B->>C: 创建问诊单
  C->>D: 发送问诊请求
  D->>E: 推送问诊通知
  E->>D: 接诊
  D->>C: 确认接诊
  C->>E: 转发患者病情
  E->>C: 开具处方与医嘱
  C->>F: 通知患者
  C->>G: 发送诊断完成事件
```

```mermaid
---
config:
  htmlLabels: false
---
flowchart TB
  subgraph AA["输入/记忆"]
    A["目标输入(Gloal)"]
    B["记忆模型(Memory)"]
  end
  subgraph CC["智能体核心(AI Agent)"]
    C["`大语言模型
    规划与推理中心`"]
    D["工具调用(Tool Use/API)"]
    E["反思机制(Reflection)"]
  end
  F["最终响应(Response)"]
  subgraph GG["外部工具与资源(Tools)"]
    G["`**知识库(Knowledge)**
    网络搜索/数据库`"]
    H["`**外部软件(Software)**
    代码执行/计算器`"]
  end
  A & B --> C
  G & H --> D
  E -.->B
  E -. "迭代优化循环" .-> C
  C --> D
  D --> E
  E --> F
```

```mermaid
flowchart LR
subgraph "用户"
A["`用户1
主语言`"]
A1["`用户2
主语言`"]
A2["`用户3
主语言`"]
A3["`用户1
主语言`"]
A4["`用户2
主语言`"]
A5["`用户3
主语言`"]
end
subgraph "1"
B1["外部视图A"]
B2["外部视图B"]
end
subgraph "2"
C1["概念视图"]
end
subgraph "3"
D1["数据库"]
D2["数据库"]
end
A & A1 & A2 <--> B1
A3 & A4 & A5 <--> B2
B1 <--->|4| C1
B2 <--->|5| C1
C1 <--->|6| D1
```
