# ターミナルの設定まとめ

## $前の表示を現在ディレクトリ名だけに変更する

- PS1：プロンプトの表示形式を定める環境変数
- %~：作業ディレクトリ
- %n：ユーザー名

  ```bash
  #/users/へ移動
  $cd

  #.zshrcファイルを開く
  $open .zshrc

  #以下入力し保存
  export PS1="%~ $ "

  #読み込む
  source ~/.zshrc
  ```

- 参考にした記事
  ターミナルに毎回表示される長ったらしい表示を短くする
  <https://qiita.com/tonkotsuboy_com/items/b752a86cee7eaedf28da>

  ターミナルジェネレータ
  <http://ezprompt.net/>

---

## lsコマンドに色をつける

```bash
#/users/へ移動
$cd

#.zshrcファイルを開く
$open .zshrc

#以下入力し保存
export CLICOLOR=1

#読み込む
source ~/.zshrc
```

- 参考にした記事
ターミナルのカラースキームを変更しても色が変わらない時の対処法
<https://qiita.com/harashoo/items/e63b8b60fad1cfd7ff2b>

---

### .ファイルをGitHubで管理する

- GitHubにてusername/dotfilesという名前でリポジトリを作成する

- GitHubにリポジトリを作る
  
  ```bash
  #ユーザーに移動
  $cd
  
  #クローンを作成
  $git clone https://github.com/Rie-Naoi/dotfiles.git
  ```

- dotfileを移動

  ```bash
  mv ~/.bash_profile ~/dotfiles
  mv ~/.bashrc ~/dotfiles
  mv ~/.gitconfig ~/dotfiles
  mv ~/.zshrc ~/dotfiles
  ```

- スクリプトの作成と実行
  - setup.shを作成する

    ```bash
    $cd ~/dotfiles
    $touch setup.sh
    ```

  - setup.shの編集

    ```bash
    #setup.shファイルを開く
    $open setup.sh

    #以下内容をコピペし保存
    #!/bin/bash
    DOTFILES_PATH=~/dotfiles

    #リンクを貼らないディレクトリやファイルは以下のコードで除きます
    for f in .??*
    do
    [ "$f" = ".git" ] && continue
    [ "$f" = ".DS_Store" ] && continue

    ln -snfv "$DOTFILES_PATH/$f" "$HOME/$f"
    done
    ```

  - setup.shの権限変更

    ```bash
    $chmod 755 setup.sh
    ```

  - setup.shの実行

    ```bash
    $./setup.sh
    ```

- dotfileの変更をGitHubに反映

  いつものやつ

  ```bash
  $git push origin master
  ```

- 参考にした記事
ターミナルに色を付ける！ついでにbashの設定ファイルをgitで管理する（初心者向け）
<https://techracho.bpsinc.jp/wingdoor/2019_10_11/80430>

---
