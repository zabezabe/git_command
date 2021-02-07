# git コマンド

## メイン
### ソースコード取得
- clone
```bash
git clone [リポジトリURL]
```
### ブランチの確認・作成・変更
- branch
```bash
# ブランチ確認
git branch -a
# ブランチ作成
git branch -b [ブランチ名]
# ブランチ変更
git branch [ブランチ名]
```
### ローカルブランチ削除
```bash
#ブランチ削除
git branch -d [ブランチ名]
```
### ソースコードをgitにアップ 
- add
```bash
# 変更確認
git status
# 変更を個別で追加
git add ${変更ファイル}
# 変更を一括で追加
git add -A
# addしたファイルを外す
git rm --cached
```
- commit 
```bash
# メッセージなしコミット
git commit --allow-empty-massage -m ''
# メッセージ付きコミット
git commit -m 'メッセージ'
# 直前のコミット取り消し
git commit --amend
# 変更内容を表示してコミット
git commit -v
# 複数行メッセージ
git commit -F- << EOM
$ [＃タスクの番号など] 修正の概要
$ 
$ 修正の内容
$ EOM
```
- push
```bash
git push -u ${ローカルブランチ}
```
- stash
```bash
# 変更の一時退避
git stash
# 戻す
git stash pop
# 退避した一蘭
git stash list
# 退避の消去
git stash clear
```
- tag
```bash
#　タグ一蘭
git tag
# パターン一致
git tag -l 'v1.*'
# タグ打ち
git tag ${タグ名}
# タグプッシュ
git push origin ${タグ名}
```
- cherry-pick
※コンフリクトがあるとcherry-pickできない
```bash
# 別ブランチの特定コミットのみ取り込む
git cherry-pick ${コミットID}
# 複数コミット取り込む
git cherry-pick [コミットID1]..[コミットID2]
# 空コミットの取り込み
git cherry-pick --allow-emptybgit [空コミットID]
# 取り込み済みのコミットを再度取り込み
git cherry-pick --keep-reduntant-commit [コミットID]
```
マージコミットのcherry-pick
```bash
# マージコミットの親コミットIDを調べる
git log
# Marge欄のコミットIDの内親コミットIDが2番目にある場合
# マージコミットをcherry-pick
git cherry-pick -m 2 [マージコミットID]
```
## おまけ
### たまに使う
- log
```bash
# コミットのログ
 git log
 # カスタム
 git log --graph --name-status --pretty=format:"%C(red)%h %C(green)%an %Creset%s %C(yellow)%d%Creset"
```
- commit
```bash
# コミットメッセージ修正(2件前までのメッセージ修正)
git rebase -i HEAD~2
```
コマンド実行するとVimでコミットが表示される
> pick {commit_id} {commit_message} // 2件目
> pick {commit_id} {commit_message} // 1件目
`pick`の部分を`edit`に変更して保存して下記2つのコマンドを実行
```bash
git commit --amend
git rebase --continue
```
- diff
```bash
# 最終コミットからの差分
git diff HEAD^
# 差分ファイルのみ表示
git diff --name-only HEAD^
# ファイル差分
git diff file1.txt file2.txt
# コミット差分
git diff {commit_id1} {commit_id2}
# ブランチ差分
git diff [ブランチ名]
```
### あまり使わない
- init
```bash
# git初期化(.gitファイル作成)
git init
```
- add
```bash
# 追加されるファイル確認
git add -n
# 変更ファイルの追加
git add -u
```