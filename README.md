# オープンソース・ディープリサーチ・ベースライン

このプロジェクトは、大規模言語モデルを使用して、与えられたトピックについて体系的な調査・分析を行うためのベースラインシステムです。

Milvus社が公開してくれた以下の記事をベースにして作成しています。

[I Built a Deep Research with Open Source—and So Can You!](https://milvus.io/blog/i-built-a-deep-research-with-open-source-so-can-you.md)

## 機能概要

1. **質問の分解と構造化**
   - メインの質問を小さなサブクエリに分解
   - 階層的な質問構造を生成
   - トピックの特定と報告書タイトルの生成

2. **多言語対応と翻訳**
   - 日本語での入力と出力
   - 内部処理での英語への自動翻訳
   - 結果の日本語への翻訳

3. **情報収集と検索**
   - Wikipedia APIを使用した情報収集
   - Chromaベクトルデータベースによる効率的な検索
   - 文書の分割と埋め込み処理

4. **分析と回答生成**
   - OllamaとDeepSeekモデルによる質問応答
   - コンテキストを考慮した回答生成
   - 階層的な質問に対する体系的な回答

5. **レポート生成**
   - Markdown形式でのレポート自動生成
   - 階層構造を反映した文書構成
   - 質問と回答の整理された提示

## 必要条件

- Python 3.8以上
- Ollama（ローカルでの推論用）
- requirements.txtに記載された依存ライブラリ

## セットアップ

1. リポジトリのクローン
```bash
git clone https://github.com/Tomatio13/free_wiki_deep_research.git
```

2. 依存ライブラリのインストール
```bash
pip install -r requirements.txt
```

3. Ollamaのセットアップ
```bash
# Ollamaのインストールと必要なモデルのダウンロード
ollama pull deepseek-r1:1.5b
ollama pull 7shi/gemma-2-jpn-translate:2b-instruct-q8_0
```

## 使用方法

1. メインの質問とWikipediaページを設定
```python
query = "調査したい質問"
page_title = "Wikipediaの記事タイトル"
```

2. アシスタントの実行
```bash
python open_deep_research_baseline.py
```

## 主要コンポーネント

- **ChatOllama**: 推論用の言語モデル
- **HuggingFaceEmbeddings**: テキスト埋め込み生成
- **Chroma**: ベクトルデータベース
- **LangChain**: プロンプト処理とチェーン管理
- **WikipediaAPI**: Wikipedia記事の取得

## 設定オプション

- `model_name`: 使用する推論モデル（デフォルト: "deepseek-r1:1.5b"）
- `translate_model_name`: 翻訳モデル（デフォルト: "7shi/gemma-2-jpn-translate:2b-instruct-q8_0"）
- `embedding_model`: 埋め込みモデル（デフォルト: "hotchpotch/static-embedding-japanese"）
- `chroma_dir`: Chromaデータベースのディレクトリ
- `output_dir`: 出力ファイルの保存先
- `ollama_base_url`: OllamaサーバーのURL

## 出力

- `output/report.md`: 構造化された調査レポート
- `output/answers.pkl`: 生成された回答のピクルファイル

## 注意事項

- Ollamaサーバーが実行中であることを確認
- Wikipediaからの情報取得時は適切なuser-agentの設定が必要
- 大規模な質問処理には十分なリソースが推奨

## ライセンス

[ライセンス情報を記載]
MIT License