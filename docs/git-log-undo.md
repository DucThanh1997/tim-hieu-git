# GIT LOG VÀ UNDO COMMIT
---
## Xem lịch sử với git log
__Xem lịch sử commit:__
```shell
lacoski@lacoski-PC:~/GitTest/example$ git log
commit 9c002a6352b11e6873cdb7bd4cff768ba7b96674
Author: thanh1996 <123xuzu@gmail.com>
Date:   Mon Mar 26 11:35:39 2018 +0700

    demo

commit 8fcb6a81e33bf0f2162d8547a2baf6d7415d6d4d
Author: thanh1996 <123xuzu@gmail.com>
Date:   Mon Mar 26 11:35:06 2018 +0700

    demo
```

> Mỗi 1 trường sẽ có check sum riêng, thời gian commit

__Xem lịch sử commit chi tiết__

```
lacoski@lacoski-PC:~/GitTest/example$ git log -p
commit 9c002a6352b11e6873cdb7bd4cff768ba7b96674
Author: thanh1996 <123xuzu@gmail.com>
Date:   Mon Mar 26 11:35:39 2018 +0700

    demo

diff --git a/test.txt b/test.txt
index e69de29..9daeafb 100644
--- a/test.txt
+++ b/test.txt
@@ -0,0 +1 @@
+test

commit 8fcb6a81e33bf0f2162d8547a2baf6d7415d6d4d
Author: thanh1996 <123xuzu@gmail.com>
Date:   Mon Mar 26 11:35:06 2018 +0700

    demo

diff --git a/test.txt b/test.txt
new file mode 100644
index 0000000..e69de29
```

## Các thủ thuật
(Tìm hiểu thêm)

## Undo Commit
__Reset__

Nhảy HEAD về vị trí trước khi commit sai bằng `git reset`
```shell
git reset --hard HEAD^
```
Lưu ý:
- `HEAD^` có ý nghĩa giống với `HEAD~` hay `@^`, nghĩa là quay về trước 1 commit
- Muốn quay về trước n commit, VD 5 commit thì có thể thay bằng `HEAD~5`.
- `--hard` có nghĩa là bỏ commit đi và bỏ cả những thay đổi chưa được commit trong working space. Khi này môi trường sẽ hoàn toàn "sạch sẽ" như thời điểm trước khi commit.
- `--soft` có nghĩa là bỏ commit đi nhưng giữ nguyên những thay đổi chưa được commit trong working space. `--soft` hữu dụng khi bạn muốn giữ lại những thay đổi chưa commit cho lần commit tiếp theo

__--amend__

Ghi đè lại commit mới nhất bằng option --amend của git commit

```shell
lacoski@lacoski-PC:~/GitTest/example$ git status
On branch master
You are currently reverting commit 8fcb6a8.
  (fix conflicts and run "git revert --continue")
  (use "git revert --abort" to cancel the revert operation)

Unmerged paths:
  (use "git reset HEAD <file>..." to unstage)
  (use "git add/rm <file>..." as appropriate to mark resolution)

	deleted by them: test.txt

Untracked files:
  (use "git add <file>..." to include in what will be committed)

	demo123.txt

no changes added to commit (use "git add" and/or "git commit -a")
lacoski@lacoski-PC:~/GitTest/example$ git add .
lacoski@lacoski-PC:~/GitTest/example$ ls
demo123.txt  test1.txt  test.txt
lacoski@lacoski-PC:~/GitTest/example$ git status
On branch master
You are currently reverting commit 8fcb6a8.
  (all conflicts fixed: run "git revert --continue")
  (use "git revert --abort" to cancel the revert operation)

Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

	new file:   demo123.txt

lacoski@lacoski-PC:~/GitTest/example$ git commit --amend --no-edit
[master fbdce07] demo1
 Date: Mon Mar 26 12:00:51 2018 +0700
 2 files changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 demo123.txt
 create mode 100644 test1.txt
```

Xem lịch sử commit
```
lacoski@lacoski-PC:~/GitTest/example$ git log
commit fbdce07b4da4f1af3fc05e085c449bdbc5d20c55
Author: thanh1996 <123xuzu@gmail.com>
Date:   Mon Mar 26 12:00:51 2018 +0700

    demo1

commit 9c002a6352b11e6873cdb7bd4cff768ba7b96674
Author: thanh1996 <123xuzu@gmail.com>
Date:   Mon Mar 26 11:35:39 2018 +0700

    demo

commit 8fcb6a81e33bf0f2162d8547a2baf6d7415d6d4d
Author: thanh1996 <123xuzu@gmail.com>
Date:   Mon Mar 26 11:35:06 2018 +0700

    demo

```
