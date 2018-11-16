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

## Herokou CLIログイン
インストールが終わったらターミナルを開き直し、`webapp-handson`ディレクトリに移動して、CLIでのログインを行います。
```
$ heorku login
```

## gitリモートの設定

作成したHerokuアプリケーションを`webapp-handson`のgit設定でリモートリポジトリとして設定します。
```
$ heroku git:remote -a `webapp-handson-(ユーザ名)`
```
`.git/config`を開くと`[remote "heroku"]`というセクションが追加されています。

## アプリケーションのデプロイ
`webapp-handson`をHerokuにデプロイする前に、アプリケーションのログをリアルタイム表示しておきます。
```
$ heroku logs --tail
```

別のターミナルを開き、`webapp-handson`ディレクトリに移動して、アプリケーションをデプロイします。

```
$ git push heroku master
```
ターミナル上で
```
　：
remote: Verifying deploy... done.
To https://git.heroku.com/webapp-handson-xxx.git
   0abe2f6..26c2c8e  master -> master
```
のように表示されたらデプロイは成功です。

デプロイが完了するとHeroku上で`npm start`が実行されます。  
`package.json`に記述してあるビルドが実行され、`heroku logs --tail`したターミナルのログが流れ出します。  
ログの流れが止まったら、Web上に公開されたアプリを確認してみましょう。
```
$ heroku open
```
ブラウザでアプリケーションのURLが開き、`Hello Express!`と表示されたでしょうか。  
上手くいかない場合はログを確認してみてください。
