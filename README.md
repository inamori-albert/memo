# ちょっとした事のメモ

## Python
- matplotliｂ.pyplotが使えないとき
http://qiita.com/Kodaira_/items/1a3b801c7a5a41c9ce49

## Atom

- ctrl+shift+M : Markdownのプレビュー



## Linux

### alternatives
- 以下のように登録しないとalternativesでは見えない  
$ alternatives --install /usr/bin/java java /opt/jdk1.7.0_79/bin/java 1
- http://www.task-notes.com/entry/20150530/1432954800

### ibusのキーマップ設定（日本語 109の場合）
$localectl set-keymap jp-OADG109A //設定
$localectl　//確認

### virtualboxで共有ファイルをマウント
1. (virtualboxを使っているならば)virtualboxから共有フォルダを設定する（今回はshareというフォルダ名にする）
1. sudo mount -t vboxsf share /mnt/shareを実行。（/etc/fstabや/etc/rc.localに記述してもなぜか起動時にマウントしてくれない）

### sudoユーザーを追加する
- sudoユーザを追加していないと、sudo実行時に「ユーザ名 is not in the sudoers file.  This incident will be reported.」みたいに怒られる。
- 以下のようにrootユーザでvisioを実行し、以下の場所にユーザを追加するように編集すればok  
> \# visio  
\#\# The COMMANDS section may have other options added to it.  
\#\#  
\#\# Allow root to run any commands anywhere
root    ALL=(ALL)       ALL  
ユーザ名    ALL=(ALL)       ALL   <ここを追加

## CentOS

### ネットワーク関連設定まとめ
http://d.hatena.ne.jp/kanonji/20090130/1233334665

### CentOSへのSymantec Endpoint Protectionのインストール方法
-参考ページ:  
http://mytracking.hatenablog.com/entry/2016/07/20/005256#インストールするLinuxのOS情報

1. SymantecEndpointProtection.zipを作成し、適当なところに解凍（/tmp/sepとか）

1. ↑のinstall.shの権限変更
$chmod u+x install.sh

1. oracle javaをインストール（ただインストールするだけではだめで、alternativesとかでしっかり指定すること）
※alternativesとはhttp://www.task-notes.com/entry/20150530/1432954800

1. glicなどのインストール
 $yum install glibc.i686 libgcc.i686 libX11.i686

1. oracle javaのjceを入れ替える(/usr/java/jdk1.7.0.80/jre/lib/security/以下だった)
http://www.symantec.com/connect/articles/how-install-symantec-endpoint-protection-1215-ru5-linux-operating-system

1. install.shの実行

## AWS
### mfa認証
google authenticator的なものを使うのが便利（コードは３０秒に一回書き換わる）

##R
### R専門の検索エンジン
http://seekr.jp/

### R Studio ServerでPosgreSQLとつなぐ
- Rを起動し、DBIとRPostgreSQLというパッケージを入れる（以下はCentOSで試した）  
> \>install.packages("DBI")  
> \>install.packages("RPostgreSQL")
- RPostgreSQLが入らない場合はRを一旦終了し、postgresql-develをインストールしてから、RPostgreSQLを入れる。(RStudio Serverの場合はサービスの再起動が必要?)  
> $sudo yum install postgresql-devel
- 使い方  
\> require("DBI")  # 必須ではない  
\> require("RPostgreSQL")  
\> con <- dbConnect(PostgreSQL(), host="hostname", port=port, dbname="dev", user="user", password="password")  
\> dataset <- dbGetQuery(con,"SELECT * FROM users")  
\> print(dataset)  
http://qiita.com/junkonakajima/items/07ad8a227c6c586e1f99  
http://www.task-notes.com/entry/20150825/1440471600

* PostgreSQLへのコネクションを一気に切断する方法
> cons <- dbListConnections(PostgreSQL()) # すべてのコネクションのリストを取得
> for(con in cons){
>     results <- dbListResults(con) # コネクションに結びついたResultのリストを取得
>     if(length(results) > 0){
>         cat("remain\n")
>         for(r in results){
>             dbClearResult(r)　# Resultの消去
>         }
>     }
>     dbDisconnect(con) # コネクションの切断
> }

### WindowsでRStudioの環境構築
- Rの入手・インストール
https://cran.ism.ac.jp/bin/windows/base/
- RStudio Desktopの入手・インストール
https://www.rstudio.com/products/rstudio/download2/
- DBIとRPosgreSQLパッケージのインストール
- 日本語が文字化けしたときはiconv()を使う
http://overlap.hatenablog.jp/entry/2013/05/19/210432

- install.packages（）で入らないときは、直接パッケージを取ってきてインストールするしかなさそう   
\> install.packages("~/Inamori/partykit_1.1-0.tar.gz", repos = NULL, type = "source")  
https://cran.r-project.org/web/packages/available_packages_by_date.html

- 日本語の文字コード変換  
for文を使うと極端に遅くなるので、apply関数を使うこと（下の例だと、50分→0.7秒）  
\> adata <- data.frame(lapply(bdata[1], iconv, from="utf-8",to="cp932"))

## その他
- {RFinanceYJ}パッケージがうまく動かないとき
http://qiita.com/HirofumiYashima/items/5807f3236a52c35e4974
