# ISHOCON2 の結果描画用のポータルページ (イベント用)

inspired from [iwashi/private-isu-portal](https://github.com/iwashi/private-isu-portal)

## 本リポジトリでできること

Firebaseをデータストアとして利用して、保存したデータを描画するためのポータルページです。  
ISHOCON2 を個人ではなく、社内ISUCONのように複数人で取り組む時に使用すると便利です。

### ログインページ
<img width="783" alt="screen shot 2018-08-26 at 23 00 01" src="https://user-images.githubusercontent.com/1732016/44628918-d25e3780-a983-11e8-8ef0-2f12dd42c8d9.png">


### ベンチマーカーの実行ログ
<img width="1531" alt="screen shot 2018-08-25 at 15 33 35" src="https://user-images.githubusercontent.com/1732016/44628902-988d3100-a983-11e8-8126-fdd03a92c864.png">


### リアルタイムな結果表示

![Portalイメージ](https://user-images.githubusercontent.com/1732016/44306652-5e91bd00-a3ce-11e8-91ae-24b93ea77632.png)

## 使い方

本リポジトリを `git clone` したのち、 `npm install` で関連モジュールをインストールしてください。
その後、 `src/app.js` と `src/index.html` にある以下の行をご自身のFirebaseアカウントに変更してください。

```
const baseUrl = 'https://XXXX.firebaseio.com/';
```

```
const FIREBASE_URL = "https://xxxx.firebaseio.com/";
```

ベンチマーカーのURLは `src/index.html` で設定してください。

```
const BENCHMARKER_URL = "http://xxxxxx/";
```

変更が完了したら、 `webpack` コマンドにて、ビルドすれば `dist` 配下に成果物が出力されます。
dist配下に出力された、html/js を任意のWebサーバにデプロイいただければそのままご利用いただけます。

### versions

```
$ node --version
v9.11.1

$ webpack --help
webpack 1.15.0
```

## 備考

### データスキーマ

Firebaseは、以下のJSON形式でデータが保存されていることを前提としています。
JSONのPOST先URLは、 `https://XXXX.firebaseio.com/teams/:チーム名.json` になります。

```
{  
  "score":18000,
  "timestamp":1534655249667
}
```

ベンチマーカが走りきった後に、上記JSONをFirebaseへHTTP Postで渡すようにしてください。

### Firebaseの設定

Firebase側の`.read`は認証が無い前提で利用しています。

もし認証を追記される場合は、[公式ドキュメント](https://www.firebase.com/docs/web/guide/login/password.html) を参考に、
Firebase接続部分のコードの変更が必要です。
