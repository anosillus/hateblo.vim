hateblo.vim
===========

はてなブログAtomPub APIを用いて，エントリの投稿等の機能を提供するVimプラグインです

Getting started
---------------

1. `.hateblo.vim` というファイルをホームディレクトリに設置してください

        $ touch ~/.hateblo.vim

2. `.hateblo.vim` に以下のように設定を記述します (`.hateblo.vim` のサンプルは本リポジトリに含まれているので参考にして下さい)

 ```vim
 let g:hateblo_vim = {
       \ 'user':         'user_name',
       \ 'api_key':      'api_key',
       \ 'api_endpoint': 'http://.../atom',
       \ 'WYSIWYG_mode': 0 | 1,
       \ 'always_yes':   0 | 1,
       \ 'edit_command': 'tabnew'
 \ }
 ```

 以下は各項目の解説です

        user:         はてなのユーザID
        api_key:      はてなブログの設定画面で確認できるAPIキー
        api_endpoint: はてなブログの設定画面で確認できるルートエンドポイント
        WYSIWYG_mode: 見たままモードを利用している場合は1に．それ以外は0に (オプショナル, デフォルト値:0)
        always_yes:   確認プロンプトを出さずに常にyesにするときは1に (オプショナル，デフォルト値:0)
        edit_command: 記事を編集する際のファイルの開き方を指定 (デフォルト:edit)

3. 本モジュールの依存モジュールをインストールして下さい. もしもNeoBundleを利用しているなら, `.vimrc`に以下の記述を追加するとよいでしょう．

        NeoBundle 'mattn/webapi-vim'
        NeoBundle 'Shougo/unite.vim'

4. このモジュールをインストールしてください．もしもNeoBundleを利用しているなら，`.vimrc`に以下の記述を追加するとよいでしょう．

        NeoBundle 'moznion/hateblo.vim'

 あるいは手順3と手順4を組み合わせて以下のように書いてもよいでしょう．

        NeoBundle 'moznion/hateblo.vim', {
                \ 'depends': ['mattn/webapi-vim', 'Shougo/unite.vim']
        \ }

Provided commands
-----------------

- :HatebloCreate

新しいブログエントリを投稿します．
1行目に`@#@`から始まる文を記述すると，その行はタイトルとして扱われます．
もしも1行目でタイトルを指定しなかった場合は，インタラクティブにタイトルが要求されます．

また，タイトル入力後にカテゴリを入力を要求されます (もちろん入力しなくても大丈夫です．その場合はカテゴリは空として扱われます)．
カテゴリは半角カンマ (,) で区切ることにより複数個指定することが出来ます．

- :HatebloCreateDraft

新しいブログエントリを **「下書き」として** 投稿します．  
それ以外の機能は `:HatebloCreate` と同等の機能を提供しています．
本機能を利用する場合は [22261e094ad01faa433fe2c7219c6be14ce127cd](https://github.com/mattn/webapi-vim/commit/22261e094ad01faa433fe2c7219c6be14ce127cd) 以降の (つまり新しい) [webapi-vim](https://github.com/mattn/webapi-vim)がインストールされている必要があります。


- :HatebloList

ブログエントリのリストを unite source 形式で表示します．
エントリを選択すると，そのエントリを編集することができます．
後述する`HatebloUpdate`や`HatebloDelete`といったコマンドは，`HatebloList`で選択したエントリ上でしか実行することができません．

- :HatebloUpdate [new_entry_title]

ブログエントリを更新します．
引数の`new_entry_title`はオプショナルです．もしもタイトルを変更したい場合は指定してください．
引数が指定されなかった場合，タイトルは変更されません．
また，`HatebloCreate`とは異なり，1行目に`@#@`から始まる文を記述してもタイトルとしては扱われません．
なお，タグ指定時に`<nil>`というワードを指定すると設定されているタグをクリアできます．

- :HatebloDelete

ブログエントリを削除します．

Dependencies
------------

- [webapi-vim](https://github.com/mattn/webapi-vim)
- [unite.vim](https://github.com/Shougo/unite.vim)

License
-------

MIT
