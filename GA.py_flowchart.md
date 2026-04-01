```mermaid
graph TD
    %% 样式定义
    classDef startend fill:#f9f,stroke:#333,stroke-width:2px,rx:10,ry:10;
    classDef process fill:#e1f5fe,stroke:#0277bd,stroke-width:1px;
    classDef decision fill:#fff9c4,stroke:#fbc02d,stroke-width:1px;
    classDef container fill:#fff3e0,stroke:#ff9800,stroke-width:2px,stroke-dasharray: 5 5;

    %% 节点定义
    Start([GA 模块开始]) --> GetParents[获取父代染色体\n针对机器 MS 和工序 OS 两部分];
    
    GetParents --> CrossStart{<b>交 叉\nCross</b>};

    %% 交叉部分的并行分支
    CrossStart -->|MS部分| MachineCross[机器部分交叉 machine_cross\n- 随机产生若干位置 r\n- 交换父代 P1 和 P2 在 r 位置的基因];
    CrossStart -->|OS部分| OpCross[工序部分交叉 operation_cross\n- 随机划分工件集 Jobset1/Jobset2\n- 复制集合内基因，按顺序填补剩余基因];

    %% 汇聚交叉结果
    MachineCross --> VariationStart{<b>变 异\nVariation</b>};
    OpCross --> VariationStart;

    %% 变异部分的并行分支
    VariationStart -->|MS部分| MachineVar[机器部分变异 machine_variation\n- 随机选择变异位置 r\n- 贪婪选择：改为加工时间最短的机器];
    VariationStart -->|OS部分| OpVar[工序部分变异 operation_variation\n- 随机选择 r 个不同基因\n- 生成其排序的所有邻域排列\n- 评估邻域适应度，选出最优个体];

    %% 汇聚变异结果
    MachineVar --> OutputNew[输出进化后的新染色体用于下一代];
    OpVar --> OutputNew;
    
    OutputNew --> End([GA 模块结束]);
