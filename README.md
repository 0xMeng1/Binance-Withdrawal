# Binance-Withdraw/币安批量提币脚本

## 功能

本脚本使用 Python 编写，通过币安（Binance）API 实现批量提币功能。脚本从指定文件读取钱包地址，自动向多个地址提币，并将提币记录保存到 Excel 文件中。主要功能如下：

- **批量提币**：从 `wallets.txt` 文件中读取钱包地址，依次向每个地址提币。
- **随机金额和时间间隔**：提币金额在 0.01 至 0.02 ETH 之间随机生成，提币间隔时间在 10 至 30 秒之间随机，避免规律性操作。
- **API 签名**：使用 HMAC-SHA256 算法生成币安 API 签名，确保请求安全。
- **价格查询**：通过币安 API 查询提币币种的当前价格，计算提币价值（以 USDT 计），USDT 价格固定为 1.00。
- **说明**：**提币币种、提币金额、提币目标链以及提币时间间隔均可自行修改**

- ## 环境依赖

运行本脚本需要安装以下 Python 库：

```bash
pip install requests openpyxl
```


## 使用说明

- **前置说明**：需提前去币安官网-个人中心-账户-API管理界面创建一个API
- **获取自己的IP地址并填入“只访问受信任的IP(推荐)”内**：打开[网站](https://checkip.amazonaws.com)把查询到的IP地址填入
- ![image](https://github.com/user-attachments/assets/5ca587af-42c4-4c96-b3f2-2d99c50dc848)

1. **配置 API 密钥**
在脚本中填入您的币安 API 密钥和密钥信息，例如：

```bash
API_KEY = "API密钥"
API_SECRET = "API密钥"
```

2. **准备钱包地址文件**
脚本从 wallets.txt 文件中读取钱包地址，每行一个地址。示例格式如下：
```plaintext
0x1234567890abcdeff1234567890abcdeff12345678
0xabcdeff1234567890abcdeff1234567890abcdeff12
0x7890abcdeff1234567890abcdeff1234567890abcd
```

3. **配置提币参数**
脚本默认提币币种为 ETH，网络为 OPTIMISM，提币金额和时间间隔如下：
```bash
AMOUNT_MIN = 0.01  # 最小提币金额
AMOUNT_MAX = 0.03  # 最大提币金额
DELAY_MIN = 10  # 最小延迟时间（秒）
DELAY_MAX = 30  # 最大延迟时间（秒）

COIN = "ETH"  # 提币币种
NETWORK = "OPTIMISM"  # 提币网络
```
根据需求修改以上参数，例如更改币种为 BNB 或网络为 BSC。
如不知提币币种及提币网络格式，可下载**币安提币市种详细.txt**自行搜索并将关键信息填入
- 关键信息为**COIN**、**NETWORK**
- ![image](https://github.com/user-attachments/assets/c6840645-6502-49e2-8466-bf088f9933ae)


- **提币数量需大于币安规定的最小提现金额**
- ![image](https://github.com/user-attachments/assets/3dbb2172-03a3-42d5-b822-2e8519fc7a68)

4. **执行脚本**
在终端中运行脚本：
```bash
python main.py
```
运行过程
脚本读取 wallets.txt 文件中的钱包地址。

依次向每个地址提币，金额在 0.01 至 0.02 ETH 之间随机生成。

每次提币后，脚本会随机等待 10 至 30 秒（倒计时显示在终端）。

提币成功后，打印提币信息（金额、地址、ID、价值、网络），并记录到 transaction_records 列表。

所有提币完成后，记录保存到 withdrawal_records.xlsx 文件。


- ## 注意事项

API 权限：确保您的 API 密钥具有提币权限，已将运行脚本的 IP 加入白名单。

网络匹配：提币网络（如 OPTIMISM）必须与目标地址和币种支持的网络匹配，否则提币会失败。

余额检查：脚本不会自动检查账户余额，请确保账户有足够的余额（包括提币手续费）。

风险提示：提币操作不可撤销，务必谨慎使用，建议先小额测试。

错误处理：如果提币失败，脚本会打印错误信息（如余额不足、网络错误等），请根据提示排查问题。


- ## 特别声明
本项目仅供学习与研究，因使用本脚本造成的任何资产损失，由使用者自行承担风险。







