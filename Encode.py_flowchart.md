```mermaid
graph TD
    %% 样式定义 (保持不变)
    classDef startend fill:#f9f,stroke:#333,stroke-width:2px,rx:10,ry:10;
    classDef process fill:#e1f5fe,stroke:#0277bd,stroke-width:1px;
    classDef subproc fill:#e0f2f1,stroke:#00695c,stroke-width:1px,stroke-dasharray: 5 5;

    %% 节点定义 (已移除 HTML 标签，使用 \n 换行)
    Start([Encode 模块开始]) --> RecvData[接收机器加工时间矩阵和工件信息];
    
    RecvData --> CalcLen[计算染色体长度 Len_Chromo];
    
    CalcLen --> ParallelInit{并行生成三种初始子种群};

    %% 并行初始化的三个分支
    ParallelInit -->|分支 1| GlobalInit[全局初始化 Global_initial\n保证所有机器工作负荷尽量平衡];
    
    ParallelInit -->|分支 2| LocalInit[局部初始化 Local_initial\n保证单个工件选择机器负荷最小];
    
    ParallelInit -->|分支 3| RandomInit[随机初始化 Random_initial\n保证初始种群多样性，随机分配机器];

    %% 合并分支
    GlobalInit --> StackPop[拼接成完整初始种群 np.vstack\n整合 MS部分 + OS部分];
    LocalInit --> StackPop;
    RandomInit --> StackPop;
    
    StackPop --> End([返回初始种群 CHS]);
