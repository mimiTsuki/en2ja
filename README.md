# en2ja

[ollama](https://ollama.com) を使ってテキストを英語から日本語へ翻訳する CLI ツールです。

## 前提条件

- [ollama](https://ollama.com) がインストールされ、サーバーが起動していること
- 使用するモデルが `ollama pull` でダウンロード済みであること

```sh
ollama pull translategemma   # デフォルトモデル
```

## インストール

1. リポジトリをクローンする

```sh
git clone https://github.com/mimiTsuki/en2ja.git
cd en2ja
```

2. `bin/en2ja` に実行権限を付与し、PATH の通ったディレクトリへコピーする

```sh
chmod +x bin/en2ja
cp bin/en2ja /usr/local/bin/en2ja
```

3. プロンプトテンプレートと設定ファイルを `~/.config/en2ja/` へコピーする

```sh
mkdir -p ~/.config/en2ja
cp -r config/prompts ~/.config/en2ja/
cp config/config.sh ~/.config/en2ja/
```

## 使い方

テキストをパイプで渡すと日本語訳を標準出力へ返します。

```sh
echo "Hello, world!" | en2ja
# → こんにちは、世界！
```

ファイルの内容を翻訳する場合:

```sh
cat document.txt | en2ja
```

### オプション

| オプション | 説明 |
|-----------|------|
| `-m <model>` | 使用するモデルを指定する (デフォルト: `translategemma`) |
| `-l`, `--list` | 利用可能なモデル（プロンプトテンプレート）の一覧を表示する |

```sh
# 別のモデルで翻訳
echo "Good morning." | en2ja -m mymodel

# 利用可能なモデルを確認
en2ja --list
```

## 設定

`~/.config/en2ja/config.sh` でデフォルトモデルを変更できます。

```sh
DEFAULT_MODEL="mymodel"
```

## モデルの追加

`~/.config/en2ja/prompts/<model名>.txt` にプロンプトテンプレートを追加することで、任意のモデルを利用できます。テンプレート内の `{{text}}` が入力テキストに置換されます。

```
You are a translator. Translate the following English text to Japanese: {{text}}
```
