<!-- omit in toc -->
# Helloworld - Github Pages with Jekyll

公開ページ:

- [https://kenkenpa198.github.io/helloworld-github-pages-with-jekyll/](https://kenkenpa198.github.io/helloworld-github-pages-with-jekyll/)

<!-- omit in toc -->
## 目次

- [1. 実行環境](#1-実行環境)
- [2. 実行したコマンド](#2-実行したコマンド)
- [3. 参考文献](#3-参考文献)

## 1. 実行環境

```powershell
# on Windows
PS > Get-WmiObject Win32_OperatingSystem
SystemDirectory : C:\WINDOWS\system32
Organization    :
BuildNumber     : 22631
RegisteredUser  : ****
SerialNumber    : ****
Version         : 10.0.22631

PS > wsl --version
WSL バージョン: 2.0.14.0
カーネル バージョン: 5.15.133.1-1
WSLg バージョン: 1.0.59
MSRDC バージョン: 1.2.4677
Direct3D バージョン: 1.611.1-81528511
DXCore バージョン: 10.0.25131.1002-220531-1700.rs-onecore-base2-hyp
Windows バージョン: 10.0.22631.3155
```

```shell
# on WSL
$ cat /etc/issue
Ubuntu 20.04.6 LTS \n \l

$ ruby --version
ruby 3.3.0 (2023-12-25 revision 5124f9ac75) [x86_64-linux]

$ gem --version
3.5.3

$ bundler --version
Bundler version 2.5.3
```

## 2. 実行したコマンド

ローカル環境で実行したコマンドのメモ。

1. プロジェクトのディレクトリを作成する。

    ```shell
    # make project directory
    $ mkdir helloworld-github-pages-with-jekyll
    $ cd helloworld-github-pages-with-jekyll
    $ git init
    Initialized empty Git repository in .../helloworld-github-pages-with-jekyll/.git/
    ```

2. 公開用ディレクトリを作成する。

    ```shell
    $ mkdir docs
    $ cd docs
    ```

3. Jekyll のサンプルを作成する。

    ```shell
    $ jekyll new --skip-bundle .
    Ignoring stringio-3.0.4 because its extensions are not built. Try: gem pristine stringio --version 3.0.4
    Ignoring stringio-3.0.4 because its extensions are not built. Try: gem pristine stringio --version 3.0.4
    New jekyll site installed in .../helloworld-github-pages-with-jekyll/docs.
    Bundle install skipped.
    ```

4. `Gemfile` , `_config.yml` を編集する。

    ```shell
    # Edit Gemfile, _config.yml
    $ git diff
    diff --git a/docs/Gemfile b/docs/Gemfile
    index f01211b..c93db50 100644
    --- a/docs/Gemfile
    +++ b/docs/Gemfile
    -gem "jekyll", "~> 4.3.3"
    +# gem "jekyll", "~> 4.3.3"

    -# gem "github-pages", group: :jekyll_plugins
    +gem "github-pages", "~> 231", group: :jekyll_plugins

    --- a/docs/_config.yml
    +++ b/docs/_config.yml
    -baseurl: "" # the subpath of your site, e.g. /blog
    +baseurl: /helloworld-github-pages-with-jekyll/ # the subpath of your site, e.g. /blog
    ```

5. `webrick` をインストールする [^1] 。

    ```shell
    $ bundle add webrick
    ```

6. `jekyll serve` を実行する。

    ```shell
    $ bundle exec jekyll serve
    ...
        Server address: http://127.0.0.1:4000/helloworld-github-pages-with-jekyll//
    Server running... press ctrl-c to stop.
    ```

7. `http://127.0.0.1:4000/helloworld-github-pages-with-jekyll/` へアクセスする。

    ![preview](./images/preview.png)

後は GitHub へプッシュ後、Pages の設定を行う。設定方法は参考文献を参照。

## 3. 参考文献

- [Jekyll を使用して GitHub Pages サイトを作成する - GitHub Enterprise Server 3.12 Docs](https://docs.github.com/ja/enterprise-server@3.12/pages/setting-up-a-github-pages-site-with-jekyll/creating-a-github-pages-site-with-jekyll?platform=linux)
- [Jekyll を使用して GitHub Pages サイトをローカルでテストする - GitHub Enterprise Server 3.12 Docs](https://docs.github.com/ja/enterprise-server@3.12/pages/setting-up-a-github-pages-site-with-jekyll/testing-your-github-pages-site-locally-with-jekyll)

[^1]: インストールしない場合、`bundle exec jekyll serve` 実行時にエラーが発生する。

    - [Jekyll を使用して GitHub Pages サイトをローカルでテストする - GitHub Enterprise Server 3.12 Docs](https://docs.github.com/ja/enterprise-server@3.12/pages/setting-up-a-github-pages-site-with-jekyll/testing-your-github-pages-site-locally-with-jekyll#building-your-site-locally)

    > メモ: Ruby 3.0 以降をインストールした場合 (Homebrew を使用して既定のバージョンをインストールした場合に発生することがあります)、この手順でエラーが発生するおそれがあります。 これは、これらのバージョンの Ruby には、`webrick` がインストールされなくなったためです。
    >
    > エラーを修正するには、`bundle add webrick` を実行してから `bundle exec jekyll serve` をもう一度実行します。
