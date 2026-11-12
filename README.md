# skills

汎用的な開発作業を支援するための Agent Skills をまとめています。
特定のプロジェクトやフレームワークに依存しないことを基本方針としています。

## Skills

### feature-implementation

機能追加・仕様変更・バグ修正などの実装を支援します。

* リポジトリや既存コードの調査
* 要件整理・実装計画
* TDD による実装
* リファクタリング
* テスト・ビルドなどの検証

### adversarial-review

実装後のコードを独立した立場からレビューします。

* 正確性・要件充足
* 回帰リスク
* テスト品質
* セキュリティ
* エラーハンドリング
* 保守性・可読性
* スコープの妥当性

プロジェクト固有のレビュー観点にも対応できるよう、汎用的な最低限のチェックリストのみを定義しています。

### release-publication

各リポジトリの既存手順に従い、リリース準備から公開確認までを支援します。

* 変更範囲・依存更新・公開権限の確認
* テスト・ビルド・配布物の検証
* 公開処理とレジストリ反映の確認
* 公開コミット・タグ・GitHub Releaseの整合性確認

特定のパッケージ、ブランチ名、ワークフローに固定せず、対象リポジトリの設定を確認して進めます。

## Installation

`gh skill` を使用して、ユーザースコープにインストールできます。

```bash
gh skill install htnabe/skills feature-implementation --scope user
gh skill install htnabe/skills adversarial-review --scope user
gh skill install htnabe/skills release-publication --scope user
```

インストール済みの Skill は以下で確認できます。

```bash
gh skill list
```

更新する場合は以下を使用します。

```bash
gh skill update
```

## Maintenance

GitHubからインストールする共有スキルの正本は、このリポジトリ内のファイルです。
変更は`~/.copilot/skills/`のインストール済みコピーだけでなく、このリポジトリへ反映してください。
共有スキルには特定の利用先リポジトリのパス・バージョン・公開手順を固定せず、各リポジトリの設定やドキュメントを参照する方針を記述します。

## License

MIT
