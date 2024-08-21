* 仮想環境
    * [venv](https://code-graffiti.com/virtual-environment-on-mac-with-venv-in-python/#toc2)
        * 適当なディレクトリで以下のコードを実行 <br> python -m venv {環境名}
            * python -m venv -p /Users/komoriakira/.pyenv/3.11.7 {環境名}
        * 有効化 : source {環境名]/bin/activat}
        * 無効化 : deactivate
        * パッケージのインストール : pip install -r requirements.txt
    * [pyenv](https://qiita.com/tomtsutom0122/items/52487730001247fdc2c5)
        * 環境設定
        * arch -arch x86_64 env PATH=${PATH/\/opt\/homebrew\/bin:/} pyenv install {version}
        * pyenv global {version}

* docker
    * Docker Compose Watch
        * [参考](https://zenn.dev/maybe_dog/articles/bfeeee3b6650a1)
        * ざっくり要約すると、コードを監視して変更を検知するとComposeで動いてるコンテナ(or Dockerイメージ)を更新するもの
        
* github
    * git init
    * git add
    * git status
    * git commit -m ""
    * git remote add origin https://github.com/ユーザ/{作成したリポジトリ}.git
    * git branch
    * git push origin main/master
    * rm -rf .git
    * git update-ref -d HEAD
    * git log
    * git reset --soft HEAD~1
    * git pull origin
    * git lfs install
    * git lfs track ""
    * git lfs ls-files
    * git lfs checkout