# Databricks ML / 生成AI ハンズオン

Databricks 上で機械学習（ML）と生成AI を低コストで試せる初心者向けハンズオン教材です。

## 対象者

- Databricks をこれから使い始める方
- 機械学習や生成AI に興味があるエンジニア・データサイエンティスト
- Python の基本的な知識がある方

## 必要な環境

- Databricks ワークスペース（Community Edition でも可※）
- **Databricks Runtime ML**（例: 16.x ML）のクラスター
- クラスターサイズは **シングルノード（Single Node）** で十分です

> ※ Community Edition では Model Serving や Databricks Apps は利用できません。
> これらの機能を試す場合は有償ワークスペースが必要です。

## 使い方

### 1. リポジトリを Databricks にクローン

1. Databricks ワークスペースの左サイドバーで **「ワークスペース」** を選択
2. 右上の **「追加」** → **「Git フォルダー」** をクリック
3. このリポジトリの URL を入力してクローン

### 2. クラスターの作成

1. 左サイドバーの **「コンピューティング」** を選択
2. **「クラスターを作成」** をクリック
3. 以下の設定を推奨:
   - クラスターモード: **シングルノード**
   - Databricks Runtime: **Runtime ML** を選択（例: 16.x ML）
   - ノードタイプ: 最小構成でOK

### 3. ノートブックの実行

クローンしたフォルダー内のノートブック（`.py` ファイル）を開き、上から順にセルを実行してください。

## コンテンツ

### ML（機械学習）

| # | ノートブック | 内容 |
|---|---|---|
| 1 | `ml/01_scikit-learn_classification.py` | scikit-learn でワインの分類モデルを構築。MLflow で実験管理。 |
| 2 | `ml/02_model_serving.py` | 学習済みモデルを Model Serving で REST API として公開。Unity Catalog へのモデル登録。 |
| 3 | `ml/03_cleanup.py` | ハンズオンで作成したリソース（エンドポイント・モデル）のクリーンアップ。 |

### GenAI（生成AI）

| # | ノートブック | 内容 |
|---|---|---|
| 1 | `genai/01_foundation_model_apis.py` | Foundation Model APIs で LLM を呼び出し。感情分析・構造化出力・Embedding など。 |

### App（Databricks Apps）

| ファイル | 内容 |
|---|---|
| `app/app.py` | Model Serving エンドポイントを呼び出す Streamlit アプリ。Databricks Apps としてデプロイ。 |
| `app/requirements.txt` | アプリの依存ライブラリ。 |

## 推奨する実行順序

```
1. ml/01_scikit-learn_classification.py  ← モデルの学習・評価
2. ml/02_model_serving.py               ← モデルをAPIとして公開
3. app/ をDatabricks Appsとしてデプロイ    ← ブラウザからモデルを呼び出すUI
4. ml/03_cleanup.py                     ← リソースの削除（終了時）
```

## Databricks App のデプロイ方法

`app/` ディレクトリの Streamlit アプリを Databricks Apps としてデプロイする手順:

1. 左サイドバーの **「コンピューティング」** → **「アプリ」** を選択
2. **「アプリの作成」** をクリック
3. アプリ名を入力（例: `wine-classifier-app`）
4. ソースコードのパスとして、クローンしたリポジトリ内の `app/` フォルダを指定
5. **「デプロイ」** を実行

デプロイ後、表示されるURLにアクセスするとアプリが開きます。

## ディレクトリ構成

```
databricks-ai-ml-hands-on/
├── README.md
├── ml/                                  # 機械学習ノートブック
│   ├── 01_scikit-learn_classification.py  # モデルの学習・評価
│   ├── 02_model_serving.py                # モデルサービング
│   └── 03_cleanup.py                      # リソースのクリーンアップ
├── genai/                               # 生成AIノートブック
│   └── 01_foundation_model_apis.py        # Foundation Model APIs
└── app/                                 # Databricks App（Streamlit）
    ├── app.py                             # Streamlitアプリ本体
    └── requirements.txt                   # 依存ライブラリ
```

## コスト目安

- **ML 01（分類モデル）**: シングルノードクラスターで数分で完了します
- **ML 02（モデルサービング）**: Model Serving エンドポイントの稼働時間に応じた課金。`scale_to_zero_enabled=True` 設定により、未使用時の課金を抑えられます
- **生成AIノートブック**: Foundation Model APIs は pay-per-token のため、このハンズオンの範囲では少額で収まります
- **Databricks App**: アプリの稼働時間に応じた課金。不要になったら削除してください

> **重要**: ハンズオン終了後は必ず `ml/03_cleanup.py` を実行し、エンドポイントとアプリを削除してください。

## ライセンス

MIT License
