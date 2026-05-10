---
title: "从 0 到 1 的进阶：我的 Hugo + GitHub Pages 博客搭建实录"
date: 2026-05-10
draft: false
tags: ["Hugo", "GitHub Pages", "环境配置"]
categories: ["技术笔记"]
---

拥有一个个人技术博客不仅是记录成长的空间，更是理解 Web 部署、版本控制和自动化流程的绝佳实践。今天，我完成了从本地环境搭建到 GitHub 全球发布的全部流程。

## 1. 核心流程总结

整个工作流可以概括为：**本地撰写 -> Git 提交 -> GitHub Actions 自动编译 -> GitHub Pages 发布。**

- **环境构建**：安装 Hugo Extended 版（确保支持高级 CSS 处理）和 Git 环境。
- **本地起步**：使用 `hugo new site` 初始化项目结构，并引入 **PaperMod** 极简主题。
- **内容创作**：在 VS Code 中利用 Markdown 编写文章，通过 `hugo server` 进行本地实时预览（`localhost:1313`）。
- **自动化部署 (CI/CD)**：在 GitHub 建立 `username.github.io` 仓库，通过 GitHub Actions 脚本实现自动化。

## 2. 博客更新工作流
现在，我只需三步即可更新博客：

- 写文章：hugo new posts/article-name.md
- 预览：hugo server -D（在本地 localhost:1313 实时查看效果）
- 发布：
```Bash
git add .
git commit -m "Add new post"
git push
```
## 3. 踩坑与避坑指南

在搭建过程中，我遇到了几个非常具有代表性的问题：

### 🛑 坑一：Git 网络代理冲突
- **现象**：克隆主题时报错 `Failed to connect to 127.0.0.1 port 7890: Connection refused`。
- **原因**：Git 配置文件中残留了旧的代理设置。
- **对策**：使用 `git config --global --unset http.proxy` 清理，或使用 `https://ghp.ci/` 等镜像源加速。

### 🛑 坑二：VSCode 终端识别失败
- **现象**：系统已装 Hugo，但 VS Code 终端提示“找不到命令”。
- **原因**：环境变量修改后，VS Code 的终端 Session 未刷新。
- **对策**：彻底重启 VS Code，或在设置中检查 `PATH` 变量。

### 🛑 坑三：Actions 部署报错
- **现象**：GitHub Actions 显示红色叉叉，报错 `Unable to resolve action`。
- **原因**：引用的第三方部署组件失效。
- **对策**：更新 `hugo.yaml`，使用更稳定的 `peaceiris/actions-hugo@v3`。


## 4. 结语

搭建博客的过程其实就是一次微型的软件工程实践。从解决环境冲突到配置自动化流水线，这些经验比单纯写文章本身更有价值。

**Happy Coding!**