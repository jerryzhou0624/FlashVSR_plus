# Fork 指南 - 如何创建自己的 FlashVSR_plus Fork

## 方法 1: GitHub 在线 Fork（推荐用于贡献代码）

### 步骤：

1. **访问原仓库**
   - 打开浏览器访问：https://github.com/lihaoyun6/FlashVSR_plus

2. **点击 Fork 按钮**
   - 在页面右上角点击 "Fork" 按钮
   - 选择你的 GitHub 账户作为 fork 目标

3. **配置本地仓库指向你的 Fork**
   ```bash
   # 查看当前远程仓库
   git remote -v
   
   # 添加你的 fork 作为 origin（如果还没有）
   git remote set-url origin https://github.com/你的用户名/FlashVSR_plus.git
   
   # 可选：保留原仓库作为 upstream（方便同步更新）
   git remote add upstream https://github.com/lihaoyun6/FlashVSR_plus.git
   ```

4. **提交你的修改**
   ```bash
   # 添加修改的文件
   git add run.py
   git add src/pipelines/flashvsr_full.py
   git add src/pipelines/flashvsr_tiny.py
   git add src/pipelines/flashvsr_tiny_long.py
   git add requirements.txt
   
   # 提交修改
   git commit -m "添加时间统计功能：DiT Inference 和 VAE Decode 分离计时"
   
   # 推送到你的 fork
   git push origin main
   ```

---

## 方法 2: 本地创建分支（用于保存修改）

如果你想在本地保留修改而不影响 main 分支：

```bash
# 1. 创建并切换到新分支
git checkout -b my-features

# 2. 提交当前修改
git add run.py
git add src/pipelines/flashvsr_full.py
git add src/pipelines/flashvsr_tiny.py
git add src/pipelines/flashvsr_tiny_long.py
git add requirements.txt

git commit -m "添加时间统计功能：DiT Inference 和 VAE Decode 分离计时"

# 3. 如果需要推送到远程（先要在 GitHub 上创建 fork）
git push origin my-features
```

---

## 方法 3: 完全独立的仓库（从零开始）

如果你想创建一个完全独立的项目：

```bash
# 1. 在 GitHub 上创建一个新的空仓库

# 2. 移除现有的远程仓库
git remote remove origin

# 3. 添加你的新仓库地址
git remote add origin https://github.com/你的用户名/你的仓库名.git

# 4. 推送所有代码
git push -u origin main
```

---

## 当前未提交的修改

根据 `git status`，你有以下修改：

**已修改的文件：**
- `requirements.txt`
- `run.py` - 添加了时间统计功能
- `src/pipelines/flashvsr_full.py` - 添加了 DiT Inference 计时
- `src/pipelines/flashvsr_tiny.py` - 添加了 DiT Inference 计时
- `src/pipelines/flashvsr_tiny_long.py` - 添加了 DiT Inference 计时

**未跟踪的文件/目录：**
- `.flash/` - Python 虚拟环境（建议添加到 .gitignore）
- `FlashVSR_tiny_example*.mp4` - 输出视频（建议添加到 .gitignore）
- `bin/` - FFmpeg 二进制文件（建议添加到 .gitignore）
- `models/FlashVSR/` - 模型文件（通常很大，建议添加到 .gitignore）

---

## 建议的 .gitignore 配置

创建或更新 `.gitignore` 文件：

```
# 虚拟环境
.flash/
venv/
env/

# 输出视频
*.mp4
FlashVSR_*.mp4

# 二进制文件
bin/
*.exe

# 模型文件（通常很大）
models/FlashVSR/
*.pth
*.ckpt
*.safetensors

# 临时文件
_temp/
*.tmp
```

---

## 同步上游更新（如果使用 upstream）

```bash
# 获取上游更新
git fetch upstream

# 合并到你的分支
git checkout main
git merge upstream/main

# 解决可能的冲突后推送
git push origin main
```

---

## 注意事项

1. **模型文件很大**：不要提交模型文件到 Git，它们通常几 GB 大小
2. **输出视频**：输出文件也不应该提交
3. **许可证**：如果修改了原项目的代码，请遵守原项目的许可证要求
4. **贡献**：如果你想向原项目贡献代码，使用 Pull Request 方式

