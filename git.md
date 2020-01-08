## 基本 Command 指令

先介紹 command 指令如下：

- dir
  列出目前資料夾裡面的檔案和資料夾

- cd
  切換資料夾

- cd..
  回到上層

* cd\
  回到磁碟機最上層

- md
  建立資料夾

- rd
  刪除資料夾

- Mac 有 rm -rf /
- Windows 有 rd \ /s/q
  磁碟刪除

* type nul>file.txt
  產生完全空白檔案

- del
  刪除檔案

- move
  移動檔案

- copy
  複製檔案

- ren
  更改檔名

## Git 設定

- git init
  在目前的資料夾建立本地端檔案庫

- git config user.name "tommy"
  設定當前檔案庫使用者名稱

- git config user.email "tommy@gmail.com"
  設定當前檔案庫電子信箱

- git config --list
  列出目前有效的設定

## GIT 本地檔案庫指令

- git status
  查看目前**暫存區**的狀態

- git add .
  加入所有檔案到**暫存區**

- git add \*.js index.css
  加入任何.js 檔案和 index.css 到**暫存區**(用空白串接)

- git reset (index.html)
  取消加入**暫存區**的(index.html ＝>可以不加)目前在**暫存區**的狀態

- git commit -m "add index.html"
  將**暫存區**的檔案 commit 到本地檔案庫("add index.html"=>紀錄)

- git add -u
  只加入修改過被**追蹤**的檔案到暫存區不包含新增的檔案(**追蹤**=>commit 過)

- git commit -am "update"
  被**追蹤**修改過的檔案 commit 到本地檔案庫不包含新增的檔案(**追蹤**=>commit 過且不用在 add .)

- git commit --amend -m "modify"
  修改最後一次 commit 的紀錄名稱

- git rm test.html
  移除檔案(commit 後退回暫存區)

- git log
  查詢 commit 紀錄

  ```
  commit 153fb25d4a6f16efd42ab9e7590bfbca66433d2b (HEAD -> master)
  Date: Tue Jan 7 14:37:18 2020 +0800

      add-git=>(紀錄名稱)
  ```

commit 11a102fbd13cda23d0edccdb404fc2af41561396 (origin/master)
Date: Mon Dec 23 17:14:43 2019 +0800

      add=>(紀錄名稱)```

## GIT 記錄

- HEAD:工作目錄比對的基準
- master:預設的分支名稱，類似變數指向 commit

**commit 發生了什麼事?**
HEAD 和目前分支(master)都會移到最新的 commit 上

- git cat-file -p HashID
  查看 hash id 的內容 hash id 最少 4 碼以上

```
\$ git cat-file -p 153f=>153f 至少要 4 碼以上 id(commit 153f...)
tree 40cdfe118b87ef7d56095382afa33392cdbd9ec1
parent 11a102fbd13cda23d0edccdb404fc2af41561396=>(前個 commit 點)

add-git=>(commit 記錄名稱)
```

- git cat-file -p HashID=>(HashID 換成上面 tree:40cd)

```
100644 blob 85e880b7d920929b3bccf6c5dedf5ab6c8d822c3 gitignor.md=>(檔案名稱)
```

- git show
  查看最新(最後)commit 修改的 log 包含異動內容

### 比較:git show vs git log

`git show`
列出最後一個 commit 包含異動內容

`git log`
列出所有的 commit 不包含異動內容

- git show CommitID
  查看 commit id 與上一版的差異

- git show CommitID:abc.txt
  查看 commit id 版的完整檔案內容

- git diff
  比對暫存區和工作目錄的差異

- git diff HEAD
  比對 HEAD 和工作目錄的差異(HEAD=>master 上 commit 後)

- git diff --cached
  比對暫存區(add)和 HEAD(commit)之間的差異

- git diff CommitID CommitID
  比對兩個 commit id 之間的差異

- git add -p
  選擇部分內容加入暫存區(需有 commit 過才有效)
  s :切割更小區塊
  y :加入這個區塊到暫存區
  n :取消這個區塊到暫存區

## 紀錄復原

- git checkout index.html
  復原 HEAD 的 index.html(修改過的檔案還原)但加入暫存區的部分不還原

- git checkout (commit id/HEAD) 檔名
  復原 commit id/HEAD 的(index.html)=>檔名
  (但比對還是 HEAD，預設加到暫存區，有修改還是要再次 add)

- git checkout commit id
  工作目錄和 HEAD 更新到這個 commit id，但會和 master 分開不同步
  (不重設暫存區，但異動這個 commit id 改過的檔案無法切換)
  `git log`只會顯示 HEAD 之前的紀錄，`git log --all`才可看到全部
  還原:`git checkout master`就會讓 HEAD 和 master 同步

- git revert commit id
  復原 commit id 做的事情，重做一個新的 commit id
  (會自動 commit id 喔)
  會進入編輯器要離開輸入`:q`

- git revert commit id -n
  復原 commit id 做的事情，不會重做一個新的 commit id
  (不會自動 commit 喔)

- git reset --hard
  重設(還原)目前 HEAD(commit)的工作目錄，清除暫存區

- git reset commit id --hard
  (重設 HEAD&工作目錄&目前分支)到 commit id，清除暫存區

- git reflog
  解決`git reset commit id --hard`，找回之前 commit 紀錄
  查看 HEAD 移動後的歷史紀錄
  `git log --all`只顯示一部分 commit 紀錄
  `git reflog`顯示全部紀錄

```
463ae16 (HEAD -> master) HEAD@{0}: commit: fix-git
a1902ec (origin/master) HEAD@{1}: commit: addgit
31fa29f HEAD@{2}: commit: fix-git
27c8c9a HEAD@{3}: commit: add-gitcommit
153fb25 HEAD@{4}: reset: moving to HEAD
153fb25 HEAD@{5}: commit: add-git
11a102f HEAD@{6}: commit (initial): add
```

- git reset --mixed
  保持工作目錄不變，清除暫存區

- git reset commit id --mixed
  保持工作目錄不變，清除不需要的 commit 紀錄(重設目前分支&HEAD)移到選取 commit id 上，清除暫存區
  用途：打散或合併 commit

- git reset commit id --soft
  重設(HEAD&目前分支)到 commit id，保留(工作目錄&暫存區)不變

## GIT 新增分支

- git branch
  列出所有分支

- git branch dev
  在目前 HEAD 位置建立 dev 分支

- git branch dev -d
  刪除 dev 分支(但現有分支不能在 dev 分支上)

- git checkout dev
  因為 checkout 會將 HEAD 移到 dev 分支(分支必須存在)

帶異動切換:

> HEAD=>master 時，但修改檔案未 commit 時切換 dev，修改檔案會跟過去

無法切換:

> HEAD=>master 時，但修改檔案未 commit 時切換 dev ，這檔案 dev 也有，切換時會發生錯誤

**無法切換之解決方法:**

> 1. reset 捨棄
> 2. commit 提交
> 3. stash 收藏

- git stash save temp
  將目前未 commit 的檔案收藏起來，取名叫 temp，就能切換

- git stash list
  列出所有收藏清單

- git stash pop
  取出最後一個收藏

- git checkout [commit id] -b dev
  在([commit id] or 目前)位置建立 dev 分支，並且立刻切換過去

- git log --all --graph
  顯示有線圖的 log 紀錄

## 合併分支

- git merge dev
  在目前的分支上使用快進(不保留 dev commit 節點)合併 dev 分支

- git merge --no-ff dev
  使用不快進(保留 dev commit 節點，master 另開 commit 節點)合併分支
  快進：只需移動分支(預設 merge 會使用快進)
  不快進：一定產生 commit(看線圖比較容易分辨是從主線還是分支)

## 衝突處裡

## GIT push 流程

- git init
- git add README.md
- git commit -m "first commit name"
- git remote add origin `<url>`
- git push -u origin master

- git push -u origin `<branch name>`

參考資料

[git push 出错](https://www.crifan.com/git_push_error_failed_to_push_some_refs_to/)

[初用 git 和 github](https://noootown.wordpress.com/2015/06/19/git-first-use/)

[簡單介紹 Git 版本控制-2](https://slides.com/yi-tailin/git#/)

[簡單介紹 Git 版本控制 Part3](https://slides.com/yi-tailin/git-21#/)
