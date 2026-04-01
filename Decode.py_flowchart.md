```mermaid
graph TD
    %% 样式定义
    classDef startend fill:#f9f,stroke:#333,stroke-width:2px,rx:10,ry:10;
    classDef process fill:#e1f5fe,stroke:#0277bd,stroke-width:1px;
    classDef decision fill:#fff9c4,stroke:#fbc02d,stroke-width:1px;
    classDef loop fill:#e0f2f1,stroke:#00695c,stroke-width:1px,stroke-dasharray: 5 5;

    %% 节点定义
    Start([Decode 模块开始\n传入单个染色体 CHS]) --> SplitChromo[拆分染色体\nCHS 分割为 MS 序列 和 OS 序列];
    
    SplitChromo --> GenOrderMatrix[生成顺序矩阵 Order_Matrix\n转换为机器顺序矩阵 JM 和时间顺序矩阵 T];
    
    %% 循环开始
    GenOrderMatrix --> LoopStart{遍历 OS 序列中的\n每一个工件代号};

    LoopStart -- 循环 --> GetProgress[获取当前工件加工进度\n确定该加工第几道工序 O_num];
    
    GetProgress --> IndexMachine[索引目标机器\n从 JM 矩阵查找对应的加工机器 Machine];
    
    IndexMachine --> CalcEarliest[计算最早开始时间 Earliest_Start\n对比机器空闲时间窗和工件上一工序结束时间\n寻找最早可插入的空位];
    
    CalcEarliest --> UpdateStatus[更新状态 _Input\n更新 Job 和 Machine 对象\n记录时间，计算完工时间];
    
    %% 循环回溯
    UpdateStatus --> LoopStart;

    %% 循环结束
    LoopStart -- 结束 --> CalcMakespan[计算最大完工时间\n所有工序结束时间的最大值];
    
    CalcMakespan --> End([返回适应度 Fitness]);

    %% 连接样式
    linkStyle 3 stroke:#00695c,stroke-width:2px,stroke-dasharray: 5 5;
    linkStyle 7 stroke:#00695c,stroke-width:2px,stroke-dasharray: 5 5;
