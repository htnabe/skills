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

## Installation

`gh skill` を使用して、ユーザースコープにインストールできます。

```bash
gh skill install htnabe/skills implementation --scope user
gh skill install htnabe/skills adversarial-review --scope user
```

インストール済みの Skill は以下で確認できます。

```bash
gh skill list
```

更新する場合は以下を使用します。

```bash
gh skill update
```

## License

MIT
