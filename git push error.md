## GIT

---

### 基本 Command 指令

先介紹 command 指令如下：

- dir

  _列出目前資料夾裡面的檔案和資料夾_

- cd

  _切換資料夾_

- cd..

  _回到上層_

* cd\

  _回到磁碟機最上層_

- md

_建立資料夾_

- rd

_刪除資料夾_

- Mac 有 rm -rf /
- Windows 有 rd \ /s/q
  _磁碟刪除_

* type nul>file.txt

_產生完全空白檔案_

- del

_刪除檔案_

- move

_移動檔案_

- copy

_複製檔案_

- ren

## _更改檔名_

### Git 指令操作

- git init

_在目前的資料夾建立本地端檔案庫_

- git config user.name "tommy"

_設定當前檔案庫使用者名稱_

- git config user.email "tommy@gmail.com"

_設定當前檔案庫電子信箱_

- git config --list

_列出目前有效的設定_

- git status

_查看目前`暫存區`的狀態_

- git add .

_加入所有檔案到`暫存區`_

- git add \*.js index.css

_加入任何.js 檔案和 index.css 到`暫存區`(用空白串接)_

- git reset (index.html)

_取消加入`暫存區`的(index.html ＝>可以不加)目前在`暫存區`的狀態_

- git commit -m "add index.html"

_將`暫存區`的檔案 commit 到本地檔案庫("add index.html"=>紀錄)_

- git add -u

_只加入修改過被`追蹤`的檔案到暫存區不包含新增的檔案(追蹤=>commit 過)_

- git commit -am "update"

_被`追蹤`修改過的檔案 commit 到本地檔案庫不包含新增的檔案(追蹤=>commit 過且不用在 add .)_

- git commit --amend -m "modify"

_修改最後一次 commit 的紀錄名稱_

- git rm test.html

_移除檔案(commit 後退回暫存區)_

- git log
  _查詢 commit 紀錄_

* HEAD:工作目錄比對的基準
* master:預設的分支名稱，類似變數指向 commit

_commit 發生了什麼事?_
`HEAD和目前分支(master)都會移到最新的commit上`

- git cat-file -p HashID

_查看 hash id 的內容 hash id 最少 4 碼以上_

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
