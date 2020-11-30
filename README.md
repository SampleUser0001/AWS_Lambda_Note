# AWS_Lambda_Note

- [AWS_Lambda_Note](#aws_lambda_note)
  - [使用するサービス](#使用するサービス)
  - [AWS Lambda](#aws-lambda)
    - [関数の作成](#関数の作成)
    - [実装](#実装)
  - [Amazon API Gateway](#amazon-api-gateway)
    - [APIの作成](#apiの作成)
    - [Lambdaと紐づける](#lambdaと紐づける)
    - [エンドポイントの作成](#エンドポイントの作成)
    - [デプロイ](#デプロイ)
  - [AWS Lambda と API Gatewayの紐づけ](#aws-lambda-と-api-gatewayの紐づけ)
  - [実行例](#実行例)
  - [参考](#参考)

## 使用するサービス

- AWS Lambda
- Amazon API Gateway

## AWS Lambda

### 関数の作成

1. AWS Lambda → 関数の作成 → 一から作成
2. 基本的な情報入力
   - 関数名
     - SampleFunction
   - ランタイム
     - Python 3.8
   - その他
     - デフォルト
3. 「関数の作成」を押下

### 実装

1. AWS Lambdaホーム → 関数 → 作成した関数
2. エイリアスタブ → 最新クリック
3. コードタブをクリック

## Amazon API Gateway

### APIの作成

1. APIタイプを選択 → REST API
2. 作成
   - 新しいAPIの作成
     - 新しいAPI
   - 名前と説明
     - API名
       - SampleAPI
     - 説明
       - サンプル
     - エントリポイントタイプ
       - リージョン
3. APIの作成を押下

### Lambdaと紐づける

1. アクション → メソッドの作成 → GET
2. GETセットアップ
   - 統合タイプ
     - Lambda 関数
   - Lambda関数
     - SampleFunction

### エンドポイントの作成

1. 統合リクエスト   
2. GET - 統合リクエスト
   - マッピングテンプレート
     - リクエスト本文のパススルー
       - テンプレートが定義されていない場合 (推奨)
     - Content-Type
       - application/json
```json
{
 "first_name": "$input.params('first_name')",
 "last_name": "$input.params('last_name')"
}
```

### デプロイ

1. API Gateway → リソース → アクション → APIのデプロイ
2. デプロイ先ステージの選択（選択肢が無ければ作成。）

## AWS Lambda と API Gatewayの紐づけ

1. AWS Lambda → （中略） → 最新の設定タブ
2. トリガー → トリガーを追加
3. メニューに出た通りに設定

## 実行例

```
curl https://z56j1vzusk.execute-api.ap-northeast-1.amazonaws.com/test/SampleFunction?firstname=Satoru&lastname=Tanaka
```

```json
{"statusCode": 200, "body": "Hello! Satoru !"}
```

## 参考

- [CCI TECH BLOG:AWS Lambdaで簡単なREST APIを作ってみた](https://tech-cci.io/archives/1399)
- [AWS ドキュメント:Python の AWS Lambda 関数ハンドラー](https://docs.aws.amazon.com/ja_jp/lambda/latest/dg/python-handler.html)
- [AWS ドキュメント:AWS Lambda を Amazon API Gateway に使用する](https://docs.aws.amazon.com/ja_jp/lambda/latest/dg/services-apigateway.html)
- [AWS ドキュメント:HTTP API Lambda 統合に関する問題のトラブルシューティング](https://docs.aws.amazon.com/ja_jp/apigateway/latest/developerguide/http-api-troubleshooting-lambda.html)
- 
