## GIT

---

### 基本 Command 指令

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

## 更改檔名

### Git 指令操作

- git init

在目前的資料夾建立本地端檔案庫

- git config user.name "tommy"

設定當前檔案庫使用者名稱

- git config user.email "tommy@gmail.com"

設定當前檔案庫電子信箱

- git config --list

列出目前有效的設定

- git status

查看目前`暫存區`的狀態

- git add .

加入所有檔案到`暫存區`

- git add \*.js index.css

加入任何.js 檔案和 index.css 到`暫存區`(用空白串接)

- git reset (index.html)

取消加入`暫存區`的(index.html ＝>可以不加)目前在`暫存區`的狀態

- git commit -m "add index.html"

將`暫存區`的檔案 commit 到本地檔案庫("add index.html"=>紀錄)

- git add -u

只加入修改過被`追蹤`的檔案到暫存區不包含新增的檔案(追蹤=>commit 過)

- git commit -am "update"

被`追蹤`修改過的檔案 commit 到本地檔案庫不包含新增的檔案(追蹤=>commit 過且不用在 add .)

- git commit --amend -m "modify"

修改最後一次 commit 的紀錄名稱

- git rm test.html

移除檔案(commit 後退回暫存區)

- git log
  查詢 commit 紀錄
  `
  commit 153fb25d4a6f16efd42ab9e7590bfbca66433d2b (HEAD -> master)
  Date: Tue Jan 7 14:37:18 2020 +0800

      add-git=>(紀錄名稱)

commit 11a102fbd13cda23d0edccdb404fc2af41561396 (origin/master)
Date: Mon Dec 23 17:14:43 2019 +0800

      add=>(紀錄名稱)

`

- HEAD:工作目錄比對的基準
- master:預設的分支名稱，類似變數指向 commit

commit 發生了什麼事?
`HEAD和目前分支(master)都會移到最新的commit上`

- git cat-file -p HashID

查看 hash id 的內容 hash id 最少 4 碼以上
`
\$ git cat-file -p 153f=>153f 至少要 4 碼以上 id(commit 153f...)
tree 40cdfe118b87ef7d56095382afa33392cdbd9ec1
parent 11a102fbd13cda23d0edccdb404fc2af41561396=>(前個 commit 點)

add-git=>(紀錄名稱)
`

- git cat-file -p HashID=>(HashID 換成上面 tree:40cd)

`100644 blob 85e880b7d920929b3bccf6c5dedf5ab6c8d822c3 gitignor.md=>(檔案名稱)`

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

## git push error

---

- git init
- git add README.md
- git commit -m "first commit name"
- git remote add origin `<url>`
- git push -u origin master

---

- git push -u origin `<branch name>`

gh-pages

參考資料

[git push 出错](https://www.crifan.com/git_push_error_failed_to_push_some_refs_to/)

[初用 git 和 github](https://noootown.wordpress.com/2015/06/19/git-first-use/)

[簡單介紹 Git 版本控制-2](https://slides.com/yi-tailin/git#/)
