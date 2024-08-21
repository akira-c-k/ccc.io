* ARNとは
    * [参考1:Qiita](https://qiita.com/miyuki_samitani/items/4bcfa6343d710f4f9354)
    * [参考2:公式](https://docs.aws.amazon.com/ja_jp/IAM/latest/UserGuide/reference-arns.html#genref-aws-service-namespaces)
    * 概要
        * Amazon Resource Nameの略称形で、AWSサービスのリソースを一意に識別するための命名規則を指す

* AWS Lambdaで外部ライブラリを使う方法
    * LayerにARNを挿入
        * [参考:Qiita](https://qiita.com/takuma-1234/items/3f23af1994acfb1c0d00)
        * [参考:Github](https://github.com/keithrozario/Klayers?tab=readme-ov-file)
    * zip形式でlambda_function.pyとライブラリをアップロードする方法
        * [参考:公式](https://docs.aws.amazon.com/ja_jp/lambda/latest/dg/python-package.html)
        * [参考:Qiita](https://qiita.com/noyoikw/items/e67bf061c6dbca0ee7b7)
            * [参考:github](https://github.com/noyoikw/mecab-python3-lambda)
        * zipファイルは50MB以内、解凍後は250MB以内という制限がある為、pandasやnumpyなどの適用は難しい
        * もし研究で構築しているBounds-Lessのように自然言語処理を行うpyファイルを導入するなら、別のLambdaを構築した方が安牌だと思える
    * Docker imageからbuildする方法
        * [参考:Qiita](https://qiita.com/kyamamoto9120/items/f1cda89ffc7cb5254f17)
        * [参考:Qiita](https://qiita.com/sasaco/items/b65ce36c05c50a74ac3e)
        * [参考:Zenn](https://zenn.dev/kou_pg_0131/articles/lambda-container-image)
        * [参考:AWS](https://docs.aws.amazon.com/ja_jp/lambda/latest/dg/python-image.html)
        * [参考:Zenn](https://zenn.dev/ovrsa/articles/4db3a7f206616b)
        * タスク
            * step0: AWS CLIをinstallする => done: 230102
            * step1: pandasをinstallした処理をつくってみる => done: 230102
                * ~~step1-1: step1が実行できなかった場合は外部ライブラリなしの処理をつくってみる~~
            * step2: gensimを使った処理をつくってみる => done: 230102
                * [参考:tmpディレクトリの利用](https://seiri-blog.github.io/posts/aws-lambda-by-s3-file-tmp-directory-save/)
            * step3: mecabを使った処理をつくってみる => done: 230106

* Step function
    * [参考](https://dev.classmethod.jp/articles/apigateway-stepfunctions-asynchronous/)
    * タムアウト回避に利用
    
    * [AWS](https://docs.aws.amazon.com/ja_jp/step-functions/latest/dg/tutorial-api-gateway.html)
        * 現状ここでつっかえている、ここをクリアしてもどうやってフロントエンドから呼び出せばいいのやら。。
            * 少なくともroleはAPIGatewayと同一にすべきか？ => 関係ないらしい、Lambdaの権限ないからと思われる。
            * FEからはLambda叩くだけでいいか？それともLambdaからStep Functionsに繋げばいいか？

* EC2
    * [参考:Qiita](https://qiita.com/Bashi50/items/d5bc47eeb9668304aaa2)

* 仮想環境
    * [venv](https://code-graffiti.com/virtual-environment-on-mac-with-venv-in-python/#toc2)
        * 適当なディレクトリで以下のコードを実行 <br> python -m venv [環境名]
            * python -m venv -p /Users/komoriakira/.pyenv/3.11.7 [環境名]
        * 有効化 : source [環境名]/bin/activate
        * 無効化 : deactivate
        * パッケージのインストール : pip install -r requirements.txt
    * [pyenv](https://qiita.com/tomtsutom0122/items/52487730001247fdc2c5)
        * 環境設定
            """
            # setting for pyenv
            export PYENV_ROOT="$HOME/.pyenv"
            export PATH="$PYENV_ROOT/bin:$PATH" 
            eval "$(pyenv init -)"
            export LDFLAGS="-L/usr/local/opt/zlib/lib -L/usr/local/opt/bzip2/lib"
            export CPPFLAGS="-I/usr/local/opt/zlib/include -I/usr/local/opt/bzip2/include"
            """
        * arch -arch x86_64 env PATH=${PATH/\/opt\/homebrew\/bin:/} pyenv install [version]
        * pyenv global [version]

* CORS
    * cross-origin-resource-sharing
    * バックエンド側ではoriginの制御をしなくてはならない
        * テスト時には問題ないが、実際にフロントエンドから飛ばすには設定が必要
    * バックエンド側から送信するデータはjson.dumps()している必要がある

* Djangoアプリの構築
    * フォルダ作成 : django-admin startproject [django_app]
    * アプリ作成 : python manage.py startapp [boundsless]
    * マイグレーション : python manage.py makemigrations [boundsless] --> python manage.py migrate
    * 管理者作成 : python manage.py createsuperuser

* docker
    * Docker Compose Watch
        * [参考](https://zenn.dev/maybe_dog/articles/bfeeee3b6650a1)
        * ざっくり要約すると、コードを監視して変更を検知するとComposeで動いてるコンテナ(or Dockerイメージ)を更新するもの
        
* linux commands
    * vi
        * [参考](https://qiita.com/hide/items/5bfe5b322872c61a6896)
        * insert mode
            * i: shift to insert mode
        * command mode
            * カーソル移動
                * w: 次の単語 (Word)
                * b: 前の単語
                * f(文字): カーソルがある行の(文字)に移動 (Find)
                * F(文字): カーソルがある行の(文字)に移動(逆向き)
                * 0: 行頭
                * ＾: 行頭
                * $: 行末
                * %: 対応する括弧に移動
                * Ctrl + u: 半画面上 (Up)
                * Ctrl + d: 半画面下 (Down)
                * zz: カーソルが画面中央になるようにスクロール
                * Ctrl + o: 古いカーソル位置に戻る。 (Old)
                * Ctrl + i: 新しいカーソル位置に進む。
    * ls
        * -la: 隠しファイルを参照する
    * cp
        * [ファイル] [ディレクト/ファイル]
    * mv
        * [A]/ [B]/: AをBに移動する
        * [A] [B]: AをBという名称に変更する
    * sudo
        * -su: 別のユーザーでシェルを実行するコマンド

* openssl
    ```
    ERROR: Could not find a version that satisfies the requirement ssl (from versions: none)
    ERROR: No matching distribution found for ssl
    WARNING: pip is configured with locations that require TLS/SSL, however the ssl module in Python is not available.
    Could not fetch URL https://pypi.org/simple/pip/: There was a problem confirming the ssl certificate: HTTPSConnectionPool(host='pypi.org', port=443): Max retries exceeded with url: /simple/pip/ (Caused by SSLError("Can't connect to HTTPS URL because the SSL module is not available.")) - skipping
    ```
    * 上記エラーはbrew install openssl@1.1で解消したようだ
    * 念の為、openssl@3.2もインストールしたがopenssl@3としてインストールされた
    * pathが切れていた可能性あり

* github
    * git init
        * This means initialize
    * git add
        * This means preparing for adding files to repository
    * git status
    * git commit -m ""
        * This means making files committed to repository
        * -m means I can write the message
            * like; "first_commit", "add", "fix", "update", "change", etc.
            * [reference](https://suwaru.tokyo/%E3%80%90%E5%BF%85%E9%A0%88%E3%80%91git%E3%82%B3%E3%83%9F%E3%83%83%E3%83%88%E3%81%AE%E6%9B%B8%E3%81%8D%E6%96%B9%E3%83%BB%E4%BD%9C%E6%B3%95%E3%80%90prefix-emoji%E3%80%91/#anc_23)
    * git remote add origin https://github.com/ユーザ/[作成したリポジトリ].git
    * git branch
    * git push origin main/master
        * abstract ver. -> git push <> <>
    * rm -rf .git
        * This means remove git folder
    * git update-ref -d HEAD
        * return before first commit
    * git log
    * git reset --soft HEAD~1
        * git push <> <> --force
    <br> ~ This means resetting the head commit
    * git pull origin
        * reference : https://qiita.com/ikmski/items/5cc8b8832336b8d85429
    * git lfs install
    * git lfs track ""
    * git lfs ls-files
    * Even after managing lfs, errors happens..
        <br> ~ Try below.
        * git lfs migrate info : dangerous...
        * git lfs migrate import : dangerous...
        * git lfs checkout
        <br> ~ This means return to the original code
        
* pythonanywhere
    * reference : https://qiita.com/Toshi6216/items/7496ed5de1acdb1a291f
    * pa_autoconfigure_django.py --branch=master --python=3.8 https://github.com/akira-c-k/IdeaSolitia.git
        * pa_autoconfigure_django.py --nuke --branch=master --python=3.8 https://github.com/akira-c-k/IdeaSolitia.git
    * how to update
        * [Bash]cd moriaki.pythonanywhere.com/
        * [Bash]workon moriaki.pythonanywhere.com
        * [Bash]git pull origin
            * if conflict happens.
                * [Bash]git stash
                * [Bash]git pull origin
                * [Bash]git stash apply
    * check empty disk
        * du -s -B 1 /tmp ~/.[!.]* ~/* | awk '{s+=$1}END{print s}'
    * delete cashe
        * rm -rf /tmp/*
        * rm -rf ~/.cache/*