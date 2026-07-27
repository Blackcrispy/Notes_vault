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

##### 步骤 1：在本地生成 SSH 密钥对

- 打开 PowerShell（或终端），执行：
  ```bash
  ssh-keygen -t ed25519 -C "your_email@example.com"
  ```
- 一路回车，接受默认路径和空密码。
- 生成的文件：
  - `~/.ssh/id_ed25519` —— **私钥**（妥善保管，绝不外传）
  - `~/.ssh/id_ed25519.pub` —— **公钥**（可以公开）

##### 步骤 2：将公钥添加到 GitHub

- 复制公钥内容：
  ```bash
  clip < ~/.ssh/id_ed25519.pub
  ```
- 登录 GitHub → 右上角头像 → **Settings** → **SSH and GPG keys** → **New SSH key**
- 填写标题（如“我的 Windows 电脑”），粘贴公钥，保存。

##### 步骤 3：测试 SSH 连接

- 在终端中执行：
  ```bash
  ssh -T git@github.com
  ```
- 首次连接会提示确认主机指纹，输入 `yes`。
- 看到 `Hi 用户名! You've successfully authenticated...` 即表示成功。

##### 步骤 4：修改 Obsidian 仓库的远程地址

- **方法一（推荐）**：在 Obsidian Git 插件设置中，将 Remote URL 从：
  ```
  https://github.com/用户名/仓库名.git
  ```
  改为：
  ```
  git@github.com:用户名/仓库名.git
  ```
- **方法二**：命令行操作：
  ```bash
  git remote set-url origin git@github.com:用户名/仓库名.git
  ```

##### 步骤 5：验证同步功能

- 在 Obsidian 中点击 Git 插件的同步按钮，确认 push/pull 正常。

---
