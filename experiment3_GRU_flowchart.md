```mermaid
graph TD
    A[输入时间序列数据 X<br>Shape: batch_size, 24, 1] --> B(初始化隐藏状态 h0)
    B --> C{GRU 层<br>Hidden Dim: 256, Layers: 2}
    C --> D[提取最后一个时间步的输出<br>out: -1, :]
    D --> E(全连接层 Linear<br>In: 256, Out: 1)
    E --> F[输出预测值 Y<br>Shape: batch_size, 1]
