# このソフトウェアについて

GitHubアップローダのアカウント登録コマンドでSSH通信確認をする。

`ssh-keygen -l`コマンドを使って。

# 前回まで

* https://github.com/ytyaru/GitHub.Upload.SSH.key.gen.201704031547
* https://github.com/ytyaru/GitHub.DB.Accounts.Create.Table.SshKeys.201704031424
* https://github.com/ytyaru/GitHub.Upload.UserRegister.Insert.Token.201704031122
* https://github.com/ytyaru/GitHub.Upload.UserRegister.CUI.201703311858
* https://github.com/ytyaru/GitHub.Upload.CUI.Account.SubCommand.201703302040
* https://github.com/ytyaru/GitHub.Upload.Headers.License.201703301853
* https://github.com/ytyaru/GitHub.Upload.Http.Response.201703301533
* https://github.com/ytyaru/GitHub.Upload.Response.201703291452
* https://github.com/ytyaru/GitHub.Upload.Delete.CommentAndFile.201703281815
* https://github.com/ytyaru/GitHub.Upload.Add.CUI.Directory.201703281703
* https://github.com/ytyaru/GitHub.Upload.ByPython.Add.Database.Create.refactoring.GitHubApi.201703280740
* https://github.com/ytyaru/GitHub.Upload.ByPython.Add.Database.Create.refactoring.Pagenation.201703271311
* https://github.com/ytyaru/GitHub.Upload.ByPython.Add.Database.Create.refactoring.Response.201703270700
* https://github.com/ytyaru/GitHub.Upload.ByPython.Add.Database.Create.refactoring.Data.201703261947
* https://github.com/ytyaru/GitHub.Upload.ByPython.Add.Database.Create.Callable.refactoring.201703261352

# 開発環境

* Linux Mint 17.3 MATE 32bit
* [Python 3.4.3](https://www.python.org/downloads/release/python-343/)
* [SQLite](https://www.sqlite.org/) 3.8.2

## WebService

* [GitHub](https://github.com/)
    * [アカウント](https://github.com/join?source=header-home)
    * [AccessToken](https://github.com/settings/tokens)
    * [Two-Factor認証](https://github.com/settings/two_factor_authentication/intro)
    * [API v3](https://developer.github.com/v3/)

# 実行コマンド

* python3 GitHubUploader.py upload -u username -d "説明" -l http://aaa
* python3 GitHubUserRegister.py insert -u username -p pass

# 実行

```sh
python3 GitHubUserRegister.py insert -u username -p pass -m mail@com
```

* GitHubに登録し、メール確認済みの、ユーザ名、パスワード、メールアドレスを使う
* DBに登録されていないアカウントであること

# 結果

TokenとSSHを自動で作成＆設定する。

* AccessTokenを生成する
* SSH鍵を作成する(`ssh-keygen`コマンドで以下2ファイル作成)
    * `~/.ssh/github/rsa_4096_{user}`
    * `~/.ssh/github/rsa_4096_{user}.pub`
* `~/.ssh/config`ファイルに追記する
* APIでGitHubにSSH鍵を設定する
* TokenとSSHをDBへ登録する

# 課題

* 起動引数で渡さないとエラーになる
    * メールアドレスをAPIから取得できるようにしたい
* 同一Hostが`~/.ssh/config`内に定義済みでも追記されてしまう
    * Hostが既存の場合、追記しないようにしたい
        * SSHのconfigファイル編集ツールを作りたい
* 利用中アカウントでもDB登録するときに新規生成してしまう。既存のものを使いたいときはどうするか
    * すでにTokenを生成してあるアカウントの場合でも、TokenがDBに存在しないなら作成されてしまう
    * すでにSSH鍵を生成してあるアカウントの場合でも、SSH鍵がDBに存在しないなら作成されてしまう

# ライセンス #

このソフトウェアはCC0ライセンスである。

[![CC0](http://i.creativecommons.org/p/zero/1.0/88x31.png "CC0")](http://creativecommons.org/publicdomain/zero/1.0/deed.ja)

Library|License|Copyright
-------|-------|---------
[requests](http://requests-docs-ja.readthedocs.io/en/latest/)|[Apache-2.0](https://opensource.org/licenses/Apache-2.0)|[Copyright 2012 Kenneth Reitz](http://requests-docs-ja.readthedocs.io/en/latest/user/intro/#requests)
[dataset](https://dataset.readthedocs.io/en/latest/)|[MIT](https://opensource.org/licenses/MIT)|[Copyright (c) 2013, Open Knowledge Foundation, Friedrich Lindenberg, Gregor Aisch](https://github.com/pudo/dataset/blob/master/LICENSE.txt)
[bs4](https://www.crummy.com/software/BeautifulSoup/bs4/doc/)|[MIT](https://opensource.org/licenses/MIT)|[Copyright © 1996-2011 Leonard Richardson](https://pypi.python.org/pypi/beautifulsoup4),[参考](http://tdoc.info/beautifulsoup/)
[pytz](https://github.com/newvem/pytz)|[MIT](https://opensource.org/licenses/MIT)|[Copyright (c) 2003-2005 Stuart Bishop <stuart@stuartbishop.net>](https://github.com/newvem/pytz/blob/master/LICENSE.txt)
[furl](https://github.com/gruns/furl)|[Unlicense](http://unlicense.org/)|[gruns/furl](https://github.com/gruns/furl/blob/master/LICENSE.md)
[PyYAML](https://github.com/yaml/pyyaml)|[MIT](https://opensource.org/licenses/MIT)|[Copyright (c) 2006 Kirill Simonov](https://github.com/yaml/pyyaml/blob/master/LICENSE)

