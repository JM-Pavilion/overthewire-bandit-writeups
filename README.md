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
