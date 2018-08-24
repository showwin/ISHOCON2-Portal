# ISHOCON2 の結果描画用のポータルページ (イベント用)

inspired from [iwashi/private-isu-portal](https://github.com/iwashi/private-isu-portal)

## 本リポジトリでできること

Firebaseをデータストアとして利用して、保存したデータを描画するためのポータルページです。  
ISHOCON2 を個人ではなく、社内ISUCONのように複数人で取り組む時に使用すると便利です。

以下のようなグラフをリアルタイムで描画します。

![Portalイメージ](https://user-images.githubusercontent.com/1732016/44306652-5e91bd00-a3ce-11e8-91ae-24b93ea77632.png)

## 使い方

本リポジトリを `git clone` したのち、 `npm install` で関連モジュールをインストールしてください。
その後、 `src/app.js` にある以下の行をご自身のFirebaseアカウントに変更してください。

```
const baseUrl = 'https://XXXX.firebaseio.com/';
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
  "pass":true,
  "score":18000,
  "success":1434,
  "fail":0,
  "messages":[],
  "timestamp":1534655249667
}
```

ベンチマーカが走りきった後に、上記JSONをFirebaseへHTTP Postで渡すようにしてください。

### Firebaseの設定

Firebase側の`.read`は認証が無い前提で利用しています。

もし認証を追記される場合は、[公式ドキュメント](https://www.firebase.com/docs/web/guide/login/password.html) を参考に、
Firebase接続部分のコードの変更が必要です。
