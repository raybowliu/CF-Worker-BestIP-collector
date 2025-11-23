# Cloudflare 优选IP 收集器
由于GitHub版的被官方以滥用资源为理由封禁了项目，特推出基于Cloudflare worker版的优选IP，更快，更高效，更直观！抛弃github Action~

一个基于 Cloudflare Workers 的现代化 IP 地址收集与测速工具，自动从多个公开来源收集 Cloudflare IP 地址，并提供可视化界面和测速功能。

## 🌟 功能特点

- **自动收集**：定时从多个公开来源自动收集 Cloudflare IP 地址
- **智能测速**：内置一键测速功能，支持批量测试 IP 延迟
- **多种格式**：支持 TXT 格式下载和原始数据获取
- **ITDog 集成**：支持导出 IP 列表到 ITDog 进行批量 TCPing 测试
- **现代化界面**：简洁美观的 Web 界面，支持响应式设计
- **实时排序**：测速完成后自动按延迟排序，快速找到最优 IP

## 🚀 快速开始

### 前置要求

- Cloudflare 账户
- Workers 权限
- KV 命名空间（用于存储 IP 数据）

### 部署步骤

1. **克隆项目**
   ```bash
   git clone https://github.com/your-username/cloudflare-ip-collector.git
   cd cloudflare-ip-collector
   ```

2. **创建 KV 命名空间**
   - 在 Cloudflare Dashboard 中进入 Workers & Pages
   - 创建新的 KV 命名空间，名称建议为 `IP_STORAGE`
   - 记录下命名空间的 ID

3. **配置 Wrangler**
   - 复制 `wrangler.toml.example` 为 `wrangler.toml`
   - 更新 `wrangler.toml` 中的 KV 命名空间 ID：

   ```toml
   [[kv_namespaces]]
   binding = "IP_STORAGE"
   id = "your_kv_namespace_id_here"
   ```

4. **部署到 Cloudflare**
   ```bash
   npm install
   npx wrangler deploy
   ```

5. **配置定时任务**（可选）
   - 在 Cloudflare Dashboard 中为 Worker 添加定时触发器
   - 建议设置为每 12 小时运行一次

## 📖 使用方法

### Web 界面

访问部署后的 Worker 地址即可使用完整功能：

- **查看 IP 列表**：浏览所有收集到的 Cloudflare IP 地址
- **一键测速**：批量测试所有 IP 的延迟，自动排序
- **导出数据**：下载 TXT 格式的 IP 列表
- **ITDog 集成**：复制 IP 列表到 ITDog 进行更详细的测试

### API 接口

- `GET /` - 主页面
- `GET /ips` 或 `GET /ip.txt` - 获取纯文本 IP 列表
- `GET /raw` - 获取原始 JSON 数据
- `POST /update` - 手动触发 IP 更新
- `GET /speedtest?ip=<ip>` - 测试指定 IP 的速度
- `GET /itdog-data` - 获取 ITDog 格式数据

## ⚙️ 配置说明

### 数据来源

项目从多个公开的 Cloudflare IP 数据源自动收集，包括：

- ip.164746.xyz
- ip.haogege.xyz
- stock.hostmonit.com/CloudFlareYes
- api.uouin.com/cloudflare.html
- addressesapi.090227.xyz
- www.wetest.vip

### 环境变量

无需额外环境变量，所有配置通过代码管理。

## 🛠️ 开发

### 本地开发

```bash
# 安装依赖
npm install

# 启动本地开发服务器
npx wrangler dev

# 部署到生产环境
npx wrangler deploy
```

### 项目结构

```
├── cfip.js              # 主 Worker 代码
├── wrangler.toml        # Wrangler 配置
├── package.json         # 项目依赖
└── README.md           # 项目说明
```

## 📊 技术栈

- **运行时**：Cloudflare Workers
- **存储**：Cloudflare KV
- **前端**：原生 HTML/CSS/JavaScript
- **部署**：Wrangler

## 🤝 贡献

欢迎提交 Issue 和 Pull Request！

1. Fork 本项目
2. 创建特性分支 (`git checkout -b feature/AmazingFeature`)
3. 提交更改 (`git commit -m 'Add some AmazingFeature'`)
4. 推送到分支 (`git push origin feature/AmazingFeature`)
5. 创建 Pull Request

## 📄 开源协议

本项目基于 MIT 协议开源，详见 [LICENSE](LICENSE) 文件。

## ⚠️ 免责声明

本项目仅用于学习和研究目的，请勿用于商业用途或违反相关服务条款。使用者需自行承担相关风险。

## 📞 联系方式

<div align="center">

[![YouTube](https://img.shields.io/badge/YouTube-%23FF0000.svg?style=for-the-badge&logo=YouTube&logoColor=white)](https://www.youtube.com/@%E5%A5%BD%E8%BD%AF%E6%8E%A8%E8%8D%90)
[![GitHub](https://img.shields.io/badge/github-%23121011.svg?style=for-the-badge&logo=github&logoColor=white)](https://github.com/ethgan)
[![Telegram](https://img.shields.io/badge/Telegram-2CA5E0?style=for-the-badge&logo=telegram&logoColor=white)](https://t.me/yt_hytj)

</div>

或者直接点击图标：

<p align="center">
  <a href="https://www.youtube.com/@%E5%A5%BD%E8%BD%AF%E6%8E%A8%E8%8D%90" target="_blank">
    <img src="https://img.icons8.com/color/48/000000/youtube-play.png" alt="YouTube" width="40" height="40"/>
  </a>
  &nbsp;&nbsp;
  <a href="https://github.com/ethgan" target="_blank">
    <img src="https://img.icons8.com/ios-glyphs/48/000000/github.png" alt="GitHub" width="40" height="40"/>
  </a>
  &nbsp;&nbsp;
  <a href="https://t.me/yt_hytj" target="_blank">
    <img src="https://img.icons8.com/color/48/000000/telegram-app--v1.png" alt="Telegram" width="40" height="40"/>
  </a>
</p>

---

如果这个项目对你有帮助，请给个 ⭐️ 支持一下！

如果这个项目对你有帮助，请给个 ⭐️ 支持一下！
