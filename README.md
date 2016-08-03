# ちょっとした事のメモ

## Python
- matplotliｂ.pyplotが使えないとき
http://qiita.com/Kodaira_/items/1a3b801c7a5a41c9ce49

## Atom

- ctrl+shift+M : Markdownのプレビュー

## CentOSへのSymantec Endpoint Protectionのインストール方法
-
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

## Linux

### alternatives
- 以下のように登録しないとalternativesでは見えない  
$ alternatives --install /usr/bin/java java /opt/jdk1.7.0_79/bin/java 1
- http://www.task-notes.com/entry/20150530/1432954800

### ibusのキーマップ設定（日本語）
$setxkbmap -rules evdev -model jp106 -layout jp

### virtualboxで共有ファイルをマウント
1. (virtualboxを使っているならば)virtualboxから共有フォルダを設定する（今回はshareというフォルダ名にする）
1. sudo mount -t vboxsf share /mnt/shareを実行。（/etc/fstabや/etc/rc.localに記述してもなぜか起動時にマウントしてくれない）

## AWS
### mfa認証
google authenticator的なものを使うのが便利（コードは３０秒に一回書き換わる）
