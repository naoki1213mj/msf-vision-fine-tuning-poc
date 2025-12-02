# Blog Articles

このフォルダには、本プロジェクトに関連する技術記事の下書きや関連資料を格納しています。

## 📝 記事一覧

### zenn.md
- **プラットフォーム**: [Zenn](https://zenn.dev/)
- **テーマ**: Azure OpenAI GPT-4.1 Vision Fine-tuning による鋼材表面欠陥分類の検証
- **ステータス**: 執筆準備中

## 📌 記事執筆のポイント

本プロジェクトで記事化できる主なトピック：

1. **技術検証結果**
   - GPT-4.1 Vision Fine-tuning の効果（精度向上: 53.45% → 96.55%）
   - ベースラインモデルとの比較分析

2. **実装のポイント**
   - Azure OpenAI での Vision Fine-tuning の手順
   - データセット準備（NEU-DET）と JSONL 形式への変換
   - デプロイメントとモデル評価の自動化

3. **ハマりどころと解決策**
   - リージョン制限（Sweden Central / North Central US）
   - Vision Fine-tuning の制約事項
   - コスト最適化のヒント

4. **今後の展開**
   - 本番環境への適用
   - 他のドメインへの応用可能性

## 🔗 関連リンク

- [プロジェクトリポジトリ](https://github.com/naoki1213mj/msf-vision-fine-tuning-poc)
- [Azure OpenAI Documentation](https://learn.microsoft.com/azure/ai-services/openai/how-to/fine-tuning)
