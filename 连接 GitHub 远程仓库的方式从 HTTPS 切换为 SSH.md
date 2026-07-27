***
### 一、需要进行切换的原因  

- **遇到的问题**：使用 Obsidian Git 插件通过 HTTPS 方式同步时，频繁出现 `Failed to connect to github.com:443` 报错。
	
- **原因分析**：
    - HTTPS 走的是 **443 端口**，流量特征明显，在国内网络环境下容易被干扰或限制。
    - SSH 走的是 **22 端口**，相对“低调”，受限制较少，连接更稳定。
    
- **结论**：从 HTTPS 切换到 SSH 方式，可以有效解决网络连接问题，实现稳定、免密的 Git 同步。
***
### 二、SSH 基础知识

- **SSH 是什么**：Secure Shell 的缩写，一种加密网络协议，用于在不安全网络上安全地执行远程命令和传输数据。
	
- **非对称加密**：
    - **公钥（Public Key）**：相当于“锁”，可以公开，放在 GitHub 服务器上。
    - **私钥（Private Key）**：相当于“钥匙”，必须保密，保存在本地电脑。
    
- **工作流程**：GitHub 用公钥加密“挑战码”发给客户端，客户端用私钥解密并返回，验证通过即确认身份。
	
- **加密算法**：我使用的是 **ED25519**，是目前最安全、高效的 SSH 密钥算法，优于 RSA（速度慢）、DSA（已弃用）、ECDSA（有争议）。
***
### 三、操作步骤

##### 1. 在本地生成 SSH 密钥对

- 在 PowerShell 窗口中，复制并粘贴以下命令，然后把 `"your_email@example.com"` 换成你在 GitHub 上注册的邮箱地址，按回车执行。
  ```bash
  ssh-keygen -t ed25519 -C "your_email@example.com"
  ```
- 如果遇到系统不支持的提示，可以改用这个命令：
```Bash
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```

- 系统会问你要把密钥文件保存在哪里，直接按 **回车键** 接受默认位置 `C:\Users\你的用户名\.ssh\id_ed25519` 就可以了，这样最简单。

- 接下来会提示你输入一个密码（passphrase）。为了同步时更方便（尤其是在 Obsidian 插件里），**建议直接按两次回车键跳过**，不设置密码。

- 完成后，系统会显示一个类似`Your identification has been saved...`的提示，说明密钥生成成功了。
	- 生成的文件：
	  - `~/.ssh/id_ed25519` —— **私钥**（妥善保管，绝不外传）
	  - `~/.ssh/id_ed25519.pub` —— **公钥**（可以公开）

##### 2. 将公钥添加到 GitHub

- 复制公钥内容：
	- 若使用PowerShell
  ```bash
  Get-Content ~/.ssh/id_ed25519.pub | CLIP
  ```
	- 或是cmd终端
```	bash
CLIP < %USERPROFILE%\.ssh\id_ed25519.pub
```

- 登录 GitHub → 右上角头像 → **Settings** → **SSH and GPG keys** → **New SSH key**

- 填写标题标明设备（如“我的 Windows 电脑”），粘贴公钥，保存。

##### 3. 测试 SSH 连接

- 在终端中执行：
  ```bash
  ssh -T git@github.com
  ```
- 首次连接会提示确认主机指纹`Are you sure you want to continue connecting (yes/no/[fingerprint])?`，输入 `yes`。
- 看到 `Hi 用户名! You've successfully authenticated...` 即表示成功。

##### 4. 修改本地仓库的远程地址

- 此处选择直接在命令行中修改，打开你电脑上的 **命令提示符（CMD）** 或 **PowerShell**。

- 先切换到你的 Obsidian 笔记仓库目录。比如你的仓库在 `D:\Notes_vault`，就输入：
```bash
cd D:\Notes_vault
```

- 输入以下命令查看当前远程仓库地址，确认是 HTTPS：
```bash
git remote -v
```
- 你会看到类似 `origin https://github.com/...` 的输出。输入以下命令修改远程地址为 SSH 格式：
```bash
git remote set-url origin git@github.com:用户名/仓库名.git
```

- 再次输入 `git remote -v` 确认地址已经更新成功。

- 进行测试
---
