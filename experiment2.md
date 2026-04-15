```mermaid
graph TD
    A[开始 Start] --> B(load_data_FD001: 加载训练集, 测试集和真实RUL)
    B --> C(get_info: 提取传感器数据, 剔除无用列)
    C --> D(train_val_prepare: 数据归一化, 滑动窗口构建时序特征序列及RUL标签)
    D --> E(构建模型: model = CNN1)
    E --> F(train: 划分批次, 定义优化器与Loss, 前向传播计算损失并反向更新参数)
    F --> G(保存最优模型)
    G --> H(test_prediction: 加载测试集, 模型推理, 计算RMSE/Score)
    H --> I(结果可视化: 绘制真实值与预测值对比曲线)
    I --> J[结束 End]

    %% 自定义样式（可选，让图形更美观）
    style A fill:#f9f,stroke:#333,stroke-width:2px
    style J fill:#f9f,stroke:#333,stroke-width:2px
    style E fill:#bbf,stroke:#333,stroke-width:2px
    style F fill:#dfd,stroke:#333,stroke-width:2px
