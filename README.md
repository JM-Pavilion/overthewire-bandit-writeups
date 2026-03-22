# 🏴‍☠️ OverTheWire Bandit: Linux & Security Cheat Sheet
> **Note**: This repository records my journey through the Bandit wargame, focusing on DevOps automation and Linux security. (本仓库记录了我的 Bandit 闯关之旅，侧重于 DevOps 自动化与 Linux 安全。)

---

## 🎯 Level 32: Shell Escape via $0
**Challenge**: Trapped in a restricted shell that only allows uppercase commands.
**Solution**: Use the positional parameter `$0` to spawn a new, unrestricted Bash session.

* **Command**: `>> $0`
* **Result**: Successfully "escaped" to a normal shell.

---

## 🛠️ Core Command Cheat Sheet (核心命令速查表)

### 📂 Scenario 1: Probing and Opening the Door (文件系统导航)
* `ls`: Check the contents of the current folder. (查看当前文件夹内容)
* `ls -a`: View all files, including hidden ones starting with `.`. (查看所有文件，包括隐藏文件)
* `cd <dir>`: Enter the specified folder. (进入指定文件夹)
* `file ./*`: Use "X-ray" on all files to distinguish data from human-readable ASCII text. (给文件夹里的所有文件“照X光”，分辨数据与文本)

### 📖 Scenario 2: Violent Reading (处理奇葩文件名)
* **Spaces in filenames**: Type the first few letters, then press `Tab` to autocomplete, or use `cat *` with an asterisk. (带空格的文件：输入前几个字母按 Tab 键补全，或用星号全选)
* **Files starting with `-`**: You must add `./` to tell the system this is a path (e.g., `cat ./-file01`). (以 - 开头的文件：必须加 ./ 告诉系统这是路径)

### 🔍 Scenario 3: Sea Fishing for Needles (神级搜索工具)
* `find . -size 1033c`: Find files by exact size. (按大小全盘雷达搜索)
* `find / -user bandit7 -group bandit6`: Search by permission/owner. (按权限/主人搜索)
* `grep "millionth" data.txt`: "Text Microscope" to extract specific lines from a file. (文本显微镜：精准提取特定词的行)

### ⚙️ Scenario 4: Data Cleaning Assembly Line (数据清洗流水线)
1. `sort <file>`: Sort in alphabetical order. (按字母顺序排序)
2. `uniq -u`: Delete duplicate lines and leave only unique ones. (删除重复行，只留独一无二的行)
3. **Golden Combination**: `sort data.txt | uniq -u` (sort first, then find the only one). (黄金组合技：先排序，再找唯一)

---

## 🧙 Scenario 5: Hacker's "Magic Symbols" (黑客的“魔法符号”)

| Symbol | Function (作用) | Advanced Usage (进阶用法) |
| :--- | :--- | :--- |
| `\|` | **Pipe**: Feed output to the next command. (管道符：传递结果) | Complex interaction with `mkfifo`. |
| `>` | **Overwrite**: Replace the original file. (覆盖写) | Use `tee` to read while writing. |
| `>>` | **Append**: Add to the end without destroying content. (追加写) | `tee -a` is also applicable. |
| `2>/dev/null` | **Error Black Hole**: Block unauthorized error reports. (错误黑洞) | A must-have for penetration searches. |
| `&` | **Background Operation**: Don't occupy the current screen. (后台运行) | Use `tmux` or `bg/fg` for advanced use. |
| `$( )` | **Command Replacement**: Execute inner command first. (命令替换) | Modern and readable alternative to backticks. |

---

## 🛡️ Advanced Penetration Scenes (进阶渗透场景)
* **Encrypted Communication (Level 15-16)**: Ordinary `nc` can't read encrypted data; use `openssl s_client -connect [host]:[port]` to add a "translator" layer.
* **Bypass Shell Limit (Level 18)**: When `.bashrc` kicks people, follow the command directly after SSH: `ssh user@host 'cat readme'`.
* **Git Archaeology**: Use `git log -p` to view historical differences, and `git branch -a` to find leaked keys. (Git 考古：查看历史差异与分叉支寻找密钥)

## 🐳 Cloud & DevOps Lab (云与 DevOps实验室)
- **My First Container (我的第一个容器)**: Successfully deployed and managed an Nginx web server using Docker.  (使用 Docker 成功部署并管理了Nginx Web服务器)
- **Key Commands Mastered (掌握关键命令)**: `docker run`, `docker ps`, `docker stop`.

## 🐳 Docker & Cloud Deployment (Docker 与云端部署实战)

* **Custom Image Iteration (自定义镜像迭代):** Containerized my Bandit Cheat Sheet with version control. (将速查表容器化并实现版本迭代管理)
* **v1.0:** Initial deployment using standard Nginx. (基于标准 Nginx 的初步部署)
* **v2.0:** Enhanced "Hacker Style" UI with lightweight Alpine base. (采用“黑客风格” UI 及轻量级 Alpine 镜像优化)
* **DevOps Workflow (DevOps 工作流):** Mastered `Dockerfile` crafting, image tagging, and public hosting on Docker Hub. (掌握了 Dockerfile 编写、镜像标签管理及 Docker Hub 公开托管)

### 🌐 Live Demo (实时演示)
Run my latest "Hacker Style" cheat sheet with one command:
(通过以下命令直接运行我最新的“黑客风”速查表：)
```bash```
docker run -d -p 8888:80 jminng/jm-bandit-web:v2

## 🏗️ Docker Compose & Orchestration (容器编排实战)

* **Infrastructure as Code (基础设施即代码):** Orchestrated a multi-container environment using `docker-compose`. (利用 Docker Compose 实现了多容器环境的一键编排与部署。)
* **Service Coordination (服务协同):** Successfully deployed a dual-service stack (Web App + Hello Service) with isolated networking. (成功部署了包含 Web 应用和欢迎服务的双机编队，并实现了独立的容器网络连接。)
* **Resilience (韧性能力):** Demonstrated the ability to troubleshoot network timeouts and pivot to lightweight images. (展现了排查网络超时并快速切换轻量化镜像的实战应对能力。)

### 🚀 One-Click Deployment (一键部署)
To spin up my full environment, simply run:
(只需一行命令即可启动我的完整环境：)
```bash```
docker-compose up -d


