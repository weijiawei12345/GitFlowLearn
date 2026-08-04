## 一、仓库初始化与远程连接
git init                                                  # 初始化本地仓库
git remote add origin https://github.com/weijiawei12345/GitFlow-.git   # 连接远程仓库

## 二、首次提交与推送（master 分支）
git add "gitflow学习.md"                                  # 添加文件到暂存区
git commit -m "初始化：添加 gitflow 学习笔记"              # 提交到本地仓库
git push -u origin master                                 # 首次推送 master 分支（-u 建立跟踪）

## 三、创建并推送 develop 分支
git branch develop                                        # 创建 develop 分支（基于当前 HEAD）
git push -u origin develop                                # 推送 develop 分支到远程

## 四、获取远程最新信息
git fetch origin                                          # 拉取远程所有分支的最新状态

## 五、切换分支
git checkout develop                                      # 切换到 develop 分支
git checkout master                                       # 切换到 master 分支
git checkout -b some-feature develop                      # 创建并切换到新分支（基于 develop）

## 六、查看状态与历史
git status                                                # 查看当前工作区状态
git branch                                                # 查看本地所有分支
git branch -a                                             # 查看所有分支（含远程）
git log --oneline --graph --all                           # 查看分支图谱（简洁版）
git ls -la                                                # 查看目录文件（Shell 命令）

## 七、功能分支完整流程
git add .                                                 # 添加所有修改到暂存区
git commit -m "feat: 更新学习gitflow笔记并添加按钮流程分析"  # 提交
git push -u origin some-feature                           # 首次推送功能分支
git pull origin develop                                   # 拉取 develop 最新代码（保持同步）
git checkout develop                                      # 切回 develop
git merge some-feature                                    # 合并功能分支（Fast-forward）
git push                                                  # 推送 develop 到远程
git branch -d some-feature                                # 删除本地功能分支

## 八、发布分支完整流程
git checkout -b release-0.1 develop                       # 创建发布分支
git push -u origin release-0.1                            # 推送发布分支
git checkout master                                       # 切换到 master
git merge release-0.1                                     # 合并发布分支到 master
git push                                                  # 推送 master
git checkout develop                                      # 切回 develop
git merge release-0.1                                     # 合并发布分支到 develop（同步修复）
git push                                                  # 推送 develop
git branch -d release-0.1                                 # 删除本地发布分支

## 九、打版本标签
git tag -a 0.1 -m "Initial public release" master         # 在 master 上打带注释标签
git push --tags                                           # 推送所有标签到远程
git push origin v0.1.1                                    # 推送指定标签

## 十、热修复分支完整流程
git checkout -b issue-#001 master                         # 创建热修复分支（基于 master）
git add hotfix.md                                         # 添加修复文件
git commit -m "fix: 添加 hotfix 记录文档"                  # 提交修复
git push -u origin issue-#001                             # 推送热修复分支
git checkout master                                       # 切回 master
git pull origin master                                    # 拉取最新 master（保持同步）
git merge issue-#001                                      # 合并热修复分支到 master
git tag -a v0.1.1 -m "热修复 issue-#001"                   # 打补丁版本标签
git push origin master                                    # 推送 master
git push origin v0.1.1                                    # 推送标签
git checkout develop                                      # 切回 develop
git merge issue-#001                                      # 合并热修复到 develop（同步）
git push origin develop                                   # 推送 develop
git branch -d issue-#001                                  # 删除本地热修复分支