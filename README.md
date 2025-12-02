# Azure OpenAI GPT-4.1 Vision Fine-tuning PoC

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Python 3.12+](https://img.shields.io/badge/python-3.12+-blue.svg)](https://www.python.org/downloads/)
[![Azure OpenAI](https://img.shields.io/badge/Azure-OpenAI-0078D4?logo=microsoft-azure)](https://azure.microsoft.com/products/ai-services/openai-service)

Azure OpenAI の GPT-4.1 Vision モデルをファインチューニングし、鋼材表面欠陥の多クラス画像分類を行う PoC（Proof of Concept）プロジェクトです。

## 📊 結果サマリー

| モデル | 分類精度 | 向上率 |
|--------|----------|--------|
| GPT-4.1 ベースラインモデル | 53.45% | — |
| GPT-4.1 Vision ファインチューニングモデル | 96.55% | **+43.10%** |

> 🎉 Vision ファインチューニングにより、分類精度が約 **43 ポイント向上** しました。

## 🎯 ユースケース

熱間圧延鋼板の表面欠陥を自動分類するタスクです。6種類の欠陥クラスを識別します：

| 欠陥クラス | 説明 |
|------------|------|
| Crazing (Cr) | クレージング |
| Inclusion (In) | インクルージョン |
| Patches (Pa) | パッチ |
| Pitted Surface (PS) | ピット表面 |
| Rolled-in Scale (RS) | 圧延スケール |
| Scratches (Sc) | スクラッチ |

## 📁 プロジェクト構成

```text
msf-vision-fine-tuning-poc/
├── GPT-4.1 Vision Fine-tuning PoC.ipynb  # メインノートブック（GPT-4.1）
├── archive/                               # 古いノートブック（.gitignore対象）
├── NEU-DET/                               # データセット（Kaggleからダウンロード）
│   ├── train/                             # トレーニングデータ
│   │   ├── annotations/                   # アノテーション（XML）
│   │   └── images/                        # 画像ファイル
│   └── validation/                        # 検証データ
│       ├── annotations/
│       └── images/
├── steel_surface_defects/                 # 前処理済みデータ
│   ├── class1/ ~ class6/                  # クラス別画像
│   └── jsonl/                             # トレーニング用JSONLファイル
├── result/                                # 評価結果（.gitignore対象）
│   ├── confusion_matrix_*.png             # 混同行列画像
│   ├── evaluation_results_*.csv           # 評価結果CSV
│   └── evaluation_results_*.xlsx          # 評価結果Excel
├── picture/                               # ドキュメント用画像
├── pyproject.toml                         # Python プロジェクト設定
├── uv.lock                                # uvパッケージロックファイル
├── .env.example                           # 環境変数テンプレート
├── .gitignore                             # Git除外設定
├── LICENSE                                # MITライセンス
└── README.md                              # このファイル
```

> **注意**: `.gitignore`により、以下は追跡されません
>
> - `.venv/` - 仮想環境
> - `.env` - 環境変数（認証情報）
> - `archive/` - 古いノートブックファイル
> - `result/` - 評価結果ファイル
> - `NEU-DET/`, `steel_surface_defects/` - データセット（大容量）
> - `uv.lock` - パッケージロックファイル
> - `*.ipynb_checkpoints/` - Notebookチェックポイント

## 🚀 セットアップ

### 前提条件

- Python 3.12 以上
- [uv](https://docs.astral.sh/uv/) パッケージマネージャー
- Azure サブスクリプション
- Azure OpenAI リソース（Sweden Central または North Central US リージョン）

### 1. リポジトリのクローン

```bash
git clone https://github.com/naoki1213mj/msf-vision-fine-tuning-poc.git
cd msf-vision-fine-tuning-poc
```

### 2. 依存パッケージのインストール

```bash
uv sync --dev
```

### 3. 環境変数の設定

`.env.example` をコピーして `.env` を作成し、Azure の認証情報を設定します。

```bash
cp .env.example .env
```

`.env` ファイルを編集：

```env
api_key="your-azure-openai-api-key"
azure_endpoint="https://your-resource.openai.azure.com/"
subscription_id="your-subscription-id"
resource_name="your-openai-resource-name"
rg_name="your-resource-group-name"
```

### 4. データセットの準備

[NEU Surface Defect Database (Kaggle)](https://www.kaggle.com/datasets/kaustubhdikshit/neu-surface-defect-database) からデータセットをダウンロードし、`NEU-DET/` フォルダに配置します。

## 📓 ノートブックの実行

Jupyter Notebook または VS Code で `GPT-4.1 Vision Fine-tuning PoC.ipynb` を開いて実行します。

### ノートブックの内容

1. **環境設定**: パッケージのインポートと Azure 認証
2. **データ準備**: NEU-DET データセットの読み込みと JSONL 形式への変換
3. **ファイルアップロード**: トレーニング/検証データを Azure OpenAI にアップロード
4. **ファインチューニング**: GPT-4.1 Vision モデルのファインチューニングジョブ実行
5. **デプロイメント**: ファインチューニング済みモデルのデプロイ
6. **評価**: ベースラインモデルとファインチューニングモデルの比較評価
7. **結論**: 混同行列、分類レポート、誤分類分析

## 🔧 技術スタック

| カテゴリ | 技術 |
|----------|------|
| 言語 | Python 3.12+ |
| AI サービス | Azure OpenAI (GPT-4.1 Vision) |
| パッケージ管理 | uv |
| データ処理 | pandas, numpy |
| 可視化 | matplotlib, plotly |
| ML 評価 | scikit-learn |
| Azure SDK | azure-identity, azure-mgmt-cognitiveservices |

## 📖 参考資料

- [Azure OpenAI Fine-tuning Documentation](https://learn.microsoft.com/azure/ai-services/openai/how-to/fine-tuning)
- [NEU Surface Defect Database](http://faculty.neu.edu.cn/songkechen/zh_CN/zdylm/263270/list/)
- [GPT-4.1 Vision Capabilities](https://learn.microsoft.com/azure/ai-services/openai/concepts/models)
- [Fine-tuning Models - Microsoft Learn](https://learn.microsoft.com/azure/ai-services/openai/concepts/models#fine-tuning-models)

## ⚠️ 注意事項

- **リージョン制限**: GPT-4.1 Vision ファインチューニングは Sweden Central または North Central US リージョンでのみ利用可能です（2025年12月時点）
- **コスト**: ファインチューニングとモデルホスティングには Azure の課金が発生します
- **自動削除**: 15日間使用されないデプロイメントは自動削除されます

> 💡 **ヒント**: リージョンの対応状況やモデルの仕様は随時更新されます。最新情報は [Azure OpenAI ドキュメント](https://learn.microsoft.com/azure/ai-services/openai/concepts/models) をご確認ください。

## 🤝 コントリビューション

Issue や Pull Request は歓迎します。大きな変更を加える場合は、まず Issue で議論してください。

## 📄 ライセンス

このプロジェクトは [MIT License](LICENSE) の下で公開されています。

## 👤 Author

- GitHub: [@naoki1213mj](https://github.com/naoki1213mj)
