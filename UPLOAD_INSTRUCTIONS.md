# 把站点 push 到 GitHub(在 Mac 终端执行)

我没法在沙箱里直接 push(GitHub 需要你的认证凭据),而且这个文件夹在 Dropbox 里、`.git` 内部锁文件会和 Dropbox 同步打架。所以推荐做法是 **先把文件复制出 Dropbox**,再从那里 push。

---

## ✅ 一键脚本(推荐)

打开 Mac 上的 **终端 (Terminal)**,把整段直接粘贴回车:

```bash
# 1. 把站点文件复制到桌面(脱离 Dropbox)
mkdir -p ~/Desktop/marginal-token-allocators
cp "/Users/siqizhu/Library/CloudStorage/Dropbox/应用/Overleaf/Token Economics arxiv version/github_page/index.html" ~/Desktop/marginal-token-allocators/
cp "/Users/siqizhu/Library/CloudStorage/Dropbox/应用/Overleaf/Token Economics arxiv version/github_page/README.md" ~/Desktop/marginal-token-allocators/
cp "/Users/siqizhu/Library/CloudStorage/Dropbox/应用/Overleaf/Token Economics arxiv version/github_page/paper.pdf" ~/Desktop/marginal-token-allocators/

# 2. 进入该目录、初始化 git
cd ~/Desktop/marginal-token-allocators
git init -b main
git add index.html README.md paper.pdf
git commit -m "Initial GitHub Pages site for the Marginal Token Allocators position paper"

# 3. 关联远端并 push
git remote add origin https://github.com/zhusq20/Agentic-AI-Systems-Should-Be-Designed-as-Marginal-Token-Allocators.git
git push -u origin main
```

第 3 步 `git push` 会弹出认证。两种处理方式:

### 方式 A:用 Personal Access Token (HTTPS,简单)

1. 打开 <https://github.com/settings/tokens> → `Generate new token (classic)` → 勾选 `repo` 权限 → 生成,复制 token(`ghp_...`)。
2. 终端弹出 `Username:` 时输入 GitHub 用户名 `zhusq20`。
3. 弹出 `Password:` 时**粘贴 token**(不是 GitHub 登录密码)。

如果 Mac 已装 [GitHub CLI](https://cli.github.com/),更快:`gh auth login` 一次后,以后 `git push` 自动通过。

### 方式 B:用 SSH key

如果你已经把 SSH key 加到 GitHub,把第 3 步的 remote 换成:
```bash
git remote set-url origin git@github.com:zhusq20/Agentic-AI-Systems-Should-Be-Designed-as-Marginal-Token-Allocators.git
git push -u origin main
```

---

## 🌐 启用 GitHub Pages(让网页能被访问)

push 成功后:

1. 打开 <https://github.com/zhusq20/Agentic-AI-Systems-Should-Be-Designed-as-Marginal-Token-Allocators>
2. 点 **Settings** → 左侧 **Pages**
3. **Build and deployment** 区:
   - Source: `Deploy from a branch`
   - Branch: `main` / `(root)` → `Save`
4. 等 1–2 分钟刷新页面,会看到:
   > Your site is live at `https://zhusq20.github.io/Agentic-AI-Systems-Should-Be-Designed-as-Marginal-Token-Allocators/`

访问该地址即可看到你的论文主页;PDF 链接也会直接生效。

---

## 🛠 常见问题

| 现象 | 处理 |
|---|---|
| `remote: Repository not found` | 仓库名是不是这串拼写?访问 <https://github.com/zhusq20/Agentic-AI-Systems-Should-Be-Designed-as-Marginal-Token-Allocators> 确认 |
| `! [rejected] main -> main (fetch first)` | 远端已经有内容(比如刚才用 `echo > README.md` 提交过)。先 `git pull origin main --rebase` 再 push |
| 弹密码框反复失败 | HTTPS 不接受账户密码,必须用 token |
| GitHub Pages 404 | 等 1–2 分钟,Pages 首次构建有延迟;或检查 Settings → Pages 是否选了 main 分支 |

---

## 📦 文件清单

`~/Desktop/marginal-token-allocators/` 里应该有:
- `index.html` — 网站首页(已用 MathJax 渲染公式)
- `README.md` — GitHub 仓库首页展示
- `paper.pdf` — 论文 PDF,网页里"📄 Paper (PDF)"按钮指向它
