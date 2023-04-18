---
title: "[Hexo] 本地部屬後，網頁卻沒有更新文章"
date: 2023-04-18 23:48:26
tags:
categories:
- [Hexo 筆記]
---

# 我的環境
我除了開設 repo 就有的 master 之外，還有將其他檔案備份至另一個分支(這個 branch 我取名叫 other)
因此在同一個repo底下，我有兩個分支。
(將其他檔案備份到另一個分支，可參考：https://guiblogs.com/hexo30-11/)

# 遇到的問題
在架設這個部落格，遇到說更新本地的內容後，部署到github，也看到 github page 有更新了，但伺服器中的網頁卻沒有更新
實際操作如下：

<!-- more -->

```
cd <hexo資料夾路徑>   # 資料夾路徑右側會顯示 master branch
hexo cl              # 清除站存檔案
hexo g               # 將內容變成 HTML
hexo d               # 部署 Hexo
```
部署到hexo之後，看到 github repo頁面右欄位最下面的 github-pages更新了
![github-pages更新了](file:///D:\awan_blog\photo\hexo-branch-update\git_page.jpg)

但網頁並沒有更新，這是遇到的問題

# 解決方案
因為目前將文章、圖片等等編輯檔案都上傳到 other 這個分支，因此也要在這個分支底下推送，才能完整更新 github 的內容
操作步驟如下：

```
git checkout other             # 切換到 other 這個 branch
                               # 這時原本的路徑旁邊原本是 (master) 應該就會變成 (other)

git add .                      # 準備推送更新過後的文章
git commit -m "更新文章標題"    # 提交推送
git push origin other          # 將推送提交上去
```

此時網頁就完全更新了，成功 ~

TBD : 我想可能是因為把文章那些都和另一個分支串起來了，因此才要額外到 other 這個分支裡面去推送更新過後的內容。