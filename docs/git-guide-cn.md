# Git 使用说明书（中文版）

## 入门设置
```bash
# 设置你的身份信息
git config --global user.name "你的名字"    # 设置你的用户名
git config --global user.email "你的邮箱"   # 设置你的邮箱

# 检查设置
git config --list    # 查看所有配置
```

## 新建或获取项目
```bash
# 新建项目
git init    # 在当前文件夹创建新的 Git 仓库

# 获取项目
git clone 项目网址    # 从网上下载项目到本地
```

## 日常工作流程
```bash
# 1. 查看当前状态
git status    # 查看哪些文件被修改了

# 2. 添加文件
git add 文件名     # 添加指定文件
git add .         # 添加所有更改的文件

# 3. 保存更改
git commit -m "说明这次更改了什么"    # 保存更改并说明原因

# 4. 上传到网上
git push         # 上传更改到网上
```

## 分支管理
```bash
# 查看分支
git branch       # 查看所有本地分支
git branch -a    # 查看所有分支（包括远程的）

# 使用分支
git checkout -b 分支名    # 创建并切换到新分支
git checkout 分支名       # 切换到已有的分支
git merge 分支名          # 合并指定分支到当前分支

# 删除分支
git branch -d 分支名                # 删除本地分支
git push origin --delete 分支名     # 删除远程分支
```

## 撤销更改
```bash
# 撤销未保存的更改
git checkout -- 文件名    # 撤销对文件的修改

# 撤销已暂存的更改
git reset HEAD 文件名     # 取消暂存

# 撤销提交
git reset --soft HEAD^   # 撤销上一次提交（保留更改）
git reset --hard HEAD^   # 完全撤销上一次提交（删除更改）
```

## 查看历史
```bash
# 查看提交历史
git log              # 查看详细历史
git log --oneline    # 查看简短历史
```

## 同步更新
```bash
# 获取最新代码
git pull    # 从网上获取最新更改并合并到本地

# 临时保存工作
git stash        # 临时保存当前工作
git stash pop    # 恢复之前保存的工作
```

## 常见问题处理
```bash
# 解决冲突
1. 打开有冲突的文件
2. 找到并解决冲突的地方（<<<<<<< 和 >>>>>>> 之间的内容）
3. 保存文件
4. git add 文件名
5. git commit 完成合并

# 网络问题
git config --global http.proxy http://代理服务器:端口    # 设置代理
git config --global --unset http.proxy                  # 取消代理
```

## 使用建议
1. 经常提交代码，每次提交只做一件事
2. 提交说明要写清楚做了什么改动
3. 重要功能开发时使用新分支
4. 定期从远程更新代码
5. 遇到不懂的问题多查文档和搜索 