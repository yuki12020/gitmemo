# （１）ローカルリポジトリの作成
初期化して、現在あるファイルを追加して、コミットすればOK
ファイルがなければgit initのみでOK

git使いますよ宣言
git init

gitのファイルアップロード
git add *

アップロードするファイルの名前を作成
git commit -m "initial commit"


（２）リモートリポジトリからプロジェクトをコピー
ターミナルでローカルリポジトリに移動して以下のコマンド
cd [ローカルリポジトリのパス]
git clone [リモートリポリトジパス]　(例： https://github.com/jquery/jquery.git)


（３）ファイル更新までの基本手順
ざっくりは以下の様な流れ

ファイルを追加
ファイルをコミット
ファイルを更新
git add [ファイル名] //追加
git commit -a -m "任意のコメント"  //コミット (-aオプションは変更を自動検出してくれる)
git push origin master  //masterを更新


（４）git addの使用例
git add . //すべてのファイル・ディレクトリ
git add *.css //すべてのCSSファイル
git add -n //追加されるファイルを調べる
git add -u //変更されたファイルを追加する
git rm --cached //addしてしまったファイルを除外


（５）git commitの使用例
git commit -a //変更のあったファイルすべて
git commit --amend //直前のコミットを取り消す
git commit -v //変更点を表示してコミット


（６）コミットの取り消し
git reset --soft HEAD~2 // 最新のコミットから2件分をワークディレクトリの内容を保持し取り消す
git reset --hard HEAD~2 // 最新のコミットから2件分のワークディレクトリの内容とコミットを取り消


（７）コミットメッセージの修正
git rebase -i HEAD~2 // HEADから2件のコミットメッセージ
上記のコマンドを実行するとVimが起動し、最新から過去2件のコミットが表示されます。
※ Vimのコマンドはこちらを参考に → Vimコマンドまとめ

pick {commit_id} {commit_meessage} // 2件目
pick {commit_id} {commit_meessage} // 1件目(最新コミット)
pickの部分をeditもしくはeに変更後ファイルを保存し、
修正が完了したら--amendオプションを付けてコミットする。

git commit --amend
最後に下記のコマンドを実行し完了。

git rebase --continue


（８）ランチの作成/移動/削除/変更/一覧/
ブランチは変更履歴を記録できる。

ブランチとは

ブランチとは? サルでも分かるGit入門

git branch [branch_name]  //ブランチの作成
git checkout [branch_name]  //ブランチの移動
git branch -d [branch_name]  //ブランチの削除
git branch -m [branch_name]  //現在のブランチ名の変更

git branch // ローカルブランチの一覧
	
	（使い方例）
	ren2はブランチ名　rensyuuはリポリトジ名
	[root@localhost www]# git branch
	  master
	  * ren2
	[root@localhost www]# git push rensyuu ren2
	Username for 'https://github.com': yuki12020
	Password for 'https://yuki12020@github.com':




git branch -a //リモートとローカルのブランチの一覧
git branch -r //リモートブランチの一覧
git checkout -b branch_name origin/branch_name //リモートブランチへチェックアウト



（９）編集をマージ
master以外のブランチで編集した箇所をmasterに反映させる

git checkout [branch_name]  //ブランチに移動
git commit -a -m "コメント"  //変更ファイルをコミット

git checkout master  //masterに移動
git merge [branch_name]  //差分をマージ
git push origin master  //ファイルの更新


（１０）マージを取り消す
コンフリクトが発生して一旦戻したい場合
git merge --abort


（１１）差分を確認する
git diff
git diff HEAD^ //最後のコミットからの差分を表示
git diff --name-only HEAD^ //差分ファイルを表示
git diff file1.txt file2.txt //特定フィイルの差分
git diff commit1 commit2 //コミットの差分


（１１）ログの表示
git log //コミットのログが見れる
git reflog //いろいろ見れる
git reflog origin/branch_name //pushのログが見れる
ログには色々なオプションがあるけど、おすすめは以下のコマンド。
git log --graph --name-status --pretty=format:"%C(red)%h %C(green)%an %Creset%s %C(yellow)%d%Creset"


（１２）ファイルの名前変更
git mv [変更前のファイル名] [変更後のファイル名]
git commit -a -m "rename"
git push origin master


（１３）特定ファイルを特定のコミットに戻す
特定のコミットに戻してmasterに反映したい場合は以下のコマンドで。

git checkout [commit_id] [file_name]  //特定ファイルの指定
git commit -a -m "return" //戻した内容をコミット
git push origin master //変更をプッシュ


（１４）今やってる作業を一時退避する
git stash
git stash pop //戻す場合
git stash list //退避の一覧
git stash clear //退避の消去


（１５）タグ
git tag // タグの一覧表示
git tag -l 'v1.*' // パターンでタグを検索
git tag -a v0.0.0 -m 'version 0.0.0' // タグの作成
git push origin v0.0.0 // タグの共有


（１６）ファイルの削除
git rm [name]  //特定のファイルorディレクトリの削除
git rm *  //全ファイルorディレクトリ
git commit -a -m "remove"  //削除をコミット
chgit push origin master  //削除を反映


（１７）addの取り消し
間違えてgit addしてしまった場合はresetでキャンセルできる。
git reset HEAD 
git reset HEAD {file_name}


（１８）コンフリクトの解消
手動で解決する場合
コンフリクトを解消しファイルを保存後、下記のコマンドを実行

git add {file_name}
git commit {file_name} -m "コミットメッセージ"
自動で解決する場合
現在のブランチを正とする

git checkout --ours {fime_name}
マージで指定したブランチを正とする

git checkout --theirs {fime_name}
また、mergetoolを使って解決することもできます。

（１９）現在のリポジトリのzipファイルを作成
git archive --format=zip HEAD -o ./hoge.zip


（２０）コミット間の差分を取得する
1つ前のコミットから差分を取得し、hoge.zipを作成する例
git archive --format=zip --prefix=root/ HEAD `git diff --diff-filter=D --name-only HEAD HEAD^` -o hoge.zip


（２１）無視するファイルの指定方法
.gitignoreファイルを使用する

#Directory
node_modules/
styleguide/

#一致するファイルすべて
*.txt

#aaa.cacheは除く
*.cache
!aaa.cache


（２２）git管理しているファイルをあえて無視する
git update-index --skip-worktree [ファイル名]
取り消す場合

git update-index --no-skip-worktree [ファイル名]


（２３）gitignoreに記述されているファイルを管理対象から外す
git rm --cached `git ls-files --full-name -i --exclude-from=.gitignore`


（２４）リモートリポジトリのコミットバージョンを戻す
念の為バックアップを作成

git push origin master:master_bk
一つ前に戻す場合

git push -f origin HEAD^:master
特定のコミットバージョンに戻す場合

git push -f origin ハッシュ値:master
バックアップを削除

git push origin :master_bk
