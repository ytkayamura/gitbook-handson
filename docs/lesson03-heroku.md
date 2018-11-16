# Lesson 3: Herokuへのデプロイ
`Lesson 2`で作成した`webapp-handson`はすでにHerokuにデプロイして公開できる状態になっています。  
`yarn start`(`npm start`)でビルド->起動できるようになっていることとExpressの`listen()`の引数のポートに`process.env.PORT`を指定してあるのがポイントです。  
ではHerokuでアプリケーションを公開してみましょう。

## Herokuアカウントの作成
`Log In`ボタンの下の`Sign Up`リンクからアカウントを作成してください。
https://id.heroku.com/login

## Herokuアプリケーション(の枠)を作成
作成したアカウントでログインすると、下記URLに移動するかと思います。  
https://dashboard.heroku.com/apps  

右上の`New`->`Create new app`でアプリを作成します。  
`app-name`はユーザー間で重複できません。  
`webapp-handson-(ユーザ名)`とでもしておきましょうか。  

## Heroku CLIのインストール
ダウンロードしてインストールしてください。
https://devcenter.heroku.com/articles/heroku-cli#download-and-install

## CLIログイン

## アプリケーションのデプロイ
インストールが終わったらターミナルを開き直して、`webapp-handson`ディレクトリに移動して、CLIでのログインを行います。
```
$ heorku login
```

作成したHerokuアプリケーションを`webapp-handson`のgit設定でリモートリポジトリとして設定します。
```
$ heroku git:remote -a `webapp-handson-(ユーザ名)`
```
`.git/config`を開くと`[remote "heroku"]`というセクションが追加されています。

`webapp-handson`をHerokuにデプロイしましょう。
```
$ git push heroku master
```
