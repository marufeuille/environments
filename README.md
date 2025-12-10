# デプロイフロー

このリポジトリでは GitHub Actions を使用してデプロイを行います。ワークフローは Staging (検証環境) と Production (本番環境) に分かれています。

## 1. Stagingへのデプロイ
検証のために、現在のコードを Staging 環境へデプロイします。

- **トリガー**: 手動実行 (`workflow_dispatch`)
- **アクション**: Actions タブから **Deploy-Staging** ワークフローを実行してください。デプロイ後、自動的にテスト (`test_staging`) が実行されます。

## 2. Productionへのデプロイ
検証済み（テスト通過済み）のコードを Production 環境へデプロイします。この手順には承認ステップが含まれます。

- **トリガー**: **GitHub Release** の公開 (Publish)
- **手順**:
    1.  Staging 環境で変更内容を検証します。
    2.  GitHub で新しい Release を作成します (例: tag `v1.0.0`)。
    3.  Description (説明) 欄にリリースノート（変更内容など）を記入します。
    4.  **Publish release** をクリックします。
    5.  レビュワーに Slack 通知が送信されます（リリースノートとコミットハッシュが含まれます）。
    6.  レビュワーは通知内のリンクからコミットのステータス（Stagingテストが✅になっているか）を確認し、問題なければ GitHub Actions 上でデプロイを承認 (Approve) します。
