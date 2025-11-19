原项目是https://github.com/ops-coffee/domain-cert-manager.git，我只是优化一下能windows系统docker正常使用并去除了MFA
# 🛡️ 域名证书管理系统  
企业级域名 & SSL/TLS 证书全生命周期管理平台。  
项目提供营销站点（`index.html`）、Docker 化的后端栈以及一键初始化脚本，可快速完成私有化部署与演示。

---

## 🌟 亮点功能

- **域名 & 证书全流程**：申请 → 审批 → 自动下发 → 定期盘点。
- **自动化运维**：内置工单、风险扫描、免费证书申请与续期。
- **可视化监控**：核心指标一屏总览，支持多云、多团队协作。
- **安全合规**：RBAC 权限、操作审计、密钥加密存储。

---

## 🗂️ 仓库结构

├── css / js # 官网静态资源
├── docker-compose.yaml # 一键编排 MySQL / Redis / 应用容器
├── init-*.sh | sql # 初始化脚本与数据库种子
├── index.html # 宣传落地页，可部署至任意静态托管
├── README.md # 说明文档（当前文件）
└── .gitignore / .dockerignore

yaml
复制代码

---

## ⚙️ 快速开始

### 1. 克隆项目

```bash
git clone https://github.com/ops-coffee/domain-cert-manager.git
cd domain-cert-manager
2. 启动 Docker 依赖
bash
复制代码
docker-compose up -d
ops-mysql / ops-redis 会自动挂载数据卷

ops-app 会执行 init-application.sh：迁移数据库、创建超级管理员、运行 supervisor

3. 首次登录
URL: http://{server-ip}:8001

账号：admin@ops-coffee.com

密码：ops-coffee.com

MFA 默认关闭，可在设置中开启

4. 查看日志 / 健康状态
bash
复制代码
docker-compose ps
docker-compose logs -f ops-app
5. 停止 / 清理
bash
复制代码
docker-compose down           # 保留数据卷
docker-compose down -v        # 连数据一起删除
📤 上传到 GitHub
GitHub 创建空仓库（不带 README/License）

本地执行：

bash
复制代码
git init
git add .
git commit -m "feat: initialize domain cert manager"
git remote add origin git@github.com:ops-coffee/domain-cert-manager.git
git push -u origin main
.gitignore / .dockerignore 已配置，无需担心推送临时数据。

🔧 常见运维操作
需求	命令
查看应用日志	docker logs -f ops-app
执行 Django 命令	docker exec -it ops-app bash -lc "cd /home/project/devops && python3 manage.py [cmd]"
登录数据库	docker exec -it ops-mysql mysql -ucode_devops -pops-coffee domain
重建静态资源	docker exec ops-app bash -lc "python3 manage.py collectstatic --noinput"
关闭 MFA	UPDATE accounts_user SET mfa_enable=0, otp_secret_key=NULL;

🙋 FAQ
1. 容器启动报端口占用？
修改 docker-compose.yaml 中的 ports 配置。

2. 初始化脚本失败？
确保：

换行符为 LF

文件可执行：chmod +x init-application.sh

3. 如何重新启用 MFA？
更新数据库字段或在 UI 手动启用。

4. 如何部署官网静态页？
index.html + css + js 可托管在：

GitHub Pages

Vercel

阿里云 OSS

腾讯 COS

🤝 贡献与反馈
Issue / PR：欢迎提交需求与 Bug

技术交流：ops_coffee@163.com / 微信 DREAM-FIRE-2024

如果觉得本项目有帮助，欢迎点个 ⭐️

