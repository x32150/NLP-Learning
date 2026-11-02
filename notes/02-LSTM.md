# LSTM：长短期记忆网络

LSTM（Long Short-Term Memory）维护隐藏状态 $h_t$ 和记忆单元 $c_t$，利用门控控制信息如何保留、写入与输出。令 $[h_{t-1};x_t]$ 表示拼接，$\sigma$ 为 sigmoid，$\odot$ 为逐元素相乘。

$$f_t=\sigma(W_f[h_{t-1};x_t]+b_f)$$
$$i_t=\sigma(W_i[h_{t-1};x_t]+b_i),\quad \tilde c_t=\tanh(W_c[h_{t-1};x_t]+b_c)$$
$$c_t=f_t\odot c_{t-1}+i_t\odot\tilde c_t$$
$$o_t=\sigma(W_o[h_{t-1};x_t]+b_o),\quad h_t=o_t\odot\tanh(c_t)$$

- **遗忘门** $f_t$：控制旧记忆保留的比例。
- **输入门** $i_t$：控制候选记忆 $\tilde c_t$ 写入的比例。
- **输出门** $o_t$：控制当前记忆对隐藏状态的影响。

记忆单元的加法更新为跨时间传递信息提供了更直接的路径，但并不保证彻底消除梯度消失。多层 LSTM 沿深度堆叠；双向 LSTM 分别计算两个方向的状态，通常在对应位置拼接。两种结构也可以结合。
