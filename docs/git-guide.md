# Git 使用说明书

## 基本配置
```bash
# 设置用户名和邮箱
git config --global user.name "你的用户名"
git config --global user.email "你的邮箱"

# 查看配置
git config --list
```

## 仓库操作
```bash
# 初始化新仓库
git init

# 克隆远程仓库
git clone 仓库地址

# 添加远程仓库
git remote add origin 仓库地址
```

## 基本操作
```bash
# 查看仓库状态
git status

# 添加文件到暂存区
git add 文件名    # 添加指定文件
git add .        # 添加所有文件

# 提交更改
git commit -m "提交说明"

# 推送到远程仓库
git push        # 推送到当前分支
git push -u origin 分支名  # 首次推送新分支
```

## 分支操作
```bash
# 查看分支
git branch            # 查看本地分支
git branch -r         # 查看远程分支
git branch -a         # 查看所有分支

# 创建分支
git branch 分支名              # 创建分支
git checkout -b 分支名         # 创建并切换到新分支

# 切换分支
git checkout 分支名

# 合并分支
git merge 分支名      # 将指定分支合并到当前分支

# 删除分支
git branch -d 分支名           # 删除本地分支
git push origin --delete 分支名 # 删除远程分支
```

## 历史记录
```bash
# 查看提交历史
git log              # 查看详细历史
git log --oneline    # 查看简洁历史
git log -p           # 查看详细更改内容

# 查看指定文件的历史
git log 文件名
```

## 撤销操作
```bash
# 撤销工作区的修改
git checkout -- 文件名

# 撤销暂存区的修改
git reset HEAD 文件名

# 撤销提交
git reset --soft HEAD^    # 撤销提交但保留更改
git reset --hard HEAD^    # 撤销提交并删除更改
```

## 标签管理
```bash
# 创建标签
git tag 标签名
git tag -a 标签名 -m "标签说明"

# 查看标签
git tag

# 删除标签
git tag -d 标签名
```

## 其他常用命令
```bash
# 查看差异
git diff              # 查看未暂存的更改
git diff --staged     # 查看已暂存的更改

# 临时保存工作区
git stash            # 保存当前工作区
git stash list       # 查看保存列表
git stash pop        # 恢复并删除最近的保存
git stash apply      # 恢复但不删除保存

# 更新本地仓库
git fetch            # 获取远程更新
git pull             # 获取并合并远程更新
```

## 常见问题解决
```bash
# 解决冲突
1. 手动编辑冲突文件
2. git add 冲突文件
3. git commit 完成合并

# 取消合并
git merge --abort

# 查看远程仓库信息
git remote -v
```

## 最佳实践
1. 经常提交，保持提交粒度适中
2. 提交说明要清晰明了
3. 定期从远程仓库更新代码
4. 重要功能开发使用独立分支
5. 合并前先更新主分支
6. 定期清理不需要的分支
``` 