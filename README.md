# portfolio-lambda-snippets

AWS Lambda を用いて開発・保守してきた各種スクリプトをまとめたポートフォリオ用のスニペット集です。  
主に Amazon Connect、DynamoDB との連携や、運用自動化を目的としたコードを収録しています。

## 📦 構成
```
portfolio-lambda-snippets/
├── connect_quickconnect_duplicate_handler/
│ ├── main.py
│ └── README.md
├── daily_dynamodb_cleanup/
│ ├── cleanup.py
│ └── README.md
└── ...
```

## 🛠 使用技術

- **AWS Lambda (Python)**
- **boto3**（AWS公式SDK）
- **Amazon Connect**
- **AWS S3**
- **CloudWatch Logs**

## 🔍 スニペット紹介

### 1. `connect_quickconnect_duplicate_handler`

Amazon Connect でクイック接続を登録する際、**同姓同名のユーザーが存在することで発生する重複エラー**を回避するスクリプトです。

- ユーザーの識別に チーム名 を使用
- 既存データとの整合性を保ちながら、安全に再登録を行う
- エラー発生時も CloudWatch Logs に詳細を出力

### 2. `refresh_connect_quickconnect_all`

Amazon Connect に登録されているすべてのクイック接続を**一括削除し、再作成**するスクリプトです。  
システムに不備が見つかった際に、設定をフルリフレッシュする目的で使用します。

- 全クイック接続を削除後、指定フォーマットで再作成
- 各クイック接続を適切なキューに自動で登録
- スケーラビリティに配慮し、**一度に50名までの処理を分割実行**
- 1000人以上のユーザー規模にも対応可能
- エラー時のロールバック対応・ログ出力あり

## 📌 本リポジトリの目的

- 保守業務で得た知見や工夫をコードとして残す
- boto3 や AWS 各種サービスの活用例を共有
- 一から開発した機能でなくても「現場で実際に役立ったコード」を再利用可能にする
