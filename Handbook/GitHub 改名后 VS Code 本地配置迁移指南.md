# GitHub 改名后 VS Code 本地配置迁移指南

当你修改了 GitHub 用户名（Username）之后，为了确保你能正常推送代码（Push）、拉取代码（Pull）以及保证提交记录（Commits）显示正确的名字，请按以下步骤操作。

------

## 第一步：更新 Git 全局用户信息

这一步是为了确保你以后提交的代码，作者名字（Author）显示的是你的新 ID。

1. 在 VS Code 中按下 `Ctrl + ~` 打开 **终端 (Terminal)**。

2. 输入以下命令查看当前配置：

   Bash

   ```
   git config --global --list
   ```

3. **修改用户名**：

   Bash

   ```
   # 将 "NewUsername" 替换为你修改后的新名字
   git config --global user.name "NewUsername"
   ```

4. **检查邮箱**（非常重要）：

   - 如果你使用的是普通邮箱（如 `qq.com`, `gmail.com`），**不需要修改**。
   - 如果你使用的是 GitHub 提供的 **隐私保护邮箱**（格式如 `id+旧名字@users.noreply.github.com`），你需要去 GitHub 设置里查看新的隐私邮箱地址，然后更新：

   Bash

   ```
   git config --global user.email "id+新名字@users.noreply.github.com"
   ```

------

## 第二步：更新项目的远程仓库地址 (Remote URL)

这是最关键的一步。虽然 GitHub 会对旧链接进行重定向，但为了保险起见，建议把本地项目的远程地址改为新地址。

**注意：你需要对每一个正在开发的本地项目（比如你的雨伞项目）都执行一次这个操作。**

1. 在 VS Code 打开你的项目文件夹。

2. 在终端输入以下命令，查看当前的远程仓库地址：

   Bash

   ```
   git remote -v
   ```

   *你应该会看到类似：`origin https://github.com/旧名字/项目名.git`*

3. **设置新地址**：

   Bash

   ```
   # 格式：git remote set-url origin https://github.com/新名字/项目名.git
   
   # 示例：
   git remote set-url origin https://github.com/NewUsername/CampusRainHub.git
   ```

4. 再次输入 `git remote -v` 确认地址已更新。

------

## 第三步：在 VS Code 中重新登录账号

VS Code 会缓存你的 GitHub 登录凭证。改名后，有时会导致推送代码时出现 `403` 权限错误，重新登录可以刷新 Token。

1. 查看 VS Code 左下角的 **“账号”图标**（一个小人的形状）。
2. 点击它，选择你的 GitHub 账号，点击 **Sign Out (注销)**。
3. 点击左侧侧边栏的 **源代码管理 (Source Control)** 图标（Git 图标）。
4. 试着点一下“同步更改”或“拉取/推送”，VS Code 会提示你需要登录。
5. 点击 **Sign In**，浏览器会弹窗，授权登录即可。

------

## 💡 常见问题 (Q&A)

**Q: 我以前提交的代码（Old Commits）作者名会自动变吗？**

- **A:** 不会。Git 的提交记录是永久的。以前的提交还是会显示旧的名字，只有从今天开始的新提交才会显示新名字。这不影响代码运行。

**Q: 如果我不更新 Remote URL 会怎样？**

- **A:** GitHub 暂时会帮你重定向，你依然可以 Push/Pull。但是，一旦有人注册了你用过的“旧名字”并建立了同名仓库，你的推送就会出错。**强烈建议更新。**

**Q: 我的 GitHub Pages (主页) 链接变了吗？**


- **A:** 变了。如果你有部署静态网页，现在的访问地址变成了 `https://新名字.github.io`。
