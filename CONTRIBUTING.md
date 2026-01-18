# Instructions for Contributors

## GitHub Settings

1. GitHubアカウントを持っていない場合は 
[新しい個人用アカウントへのサインアップ](https://docs.github.com/ja/get-started/start-your-journey/creating-an-account-on-github#signing-up-for-a-new-personal-account) を参考にしてアカウントを作成してください。

2. [本リポジトリ](https://github.com/YasashiRikeiOnityan/mathlava-kaito-sokuho) をforkしてください。

## Docker Settings

1. [Get Docker](https://docs.docker.com/) からDocker Desctopをダウンロードし、手順に従ってDockerをインストールしてください。

2. ターミナルで `docker -v` を実行し、正しくインストールされたか確認してください。

## Folder Structure

プロジェクトのディレクトリ構造は以下の通りです。

```
.
├── .github/
│   └── workflows/                  # GitHub Actionsワークフローを定義
├── docker/
│   └── Dockerfile                  # Dockerfile
├── scripts/                         # スクリプトを格納
├── src/
│   ├── contents/
│   │   └── {YEAR}/                # 年度ごとにフォルダを作成
│   │       └── {UNIVERSITY}/      # 大学ごとにフォルダを作成
│   │           └── {PROBLEM}.tex  # texファイル
│   └── sty/                        # styファイル
├── .gitignore
├── CONTRIBUTING.md
└── README.md
```

## How to Write

- 数式の記述は標準的なLaTeX記法に従ってください

## Creating Solutions

1. まずは解答する問題のブランチへ移動しましょう。
   ```bash
   git fetch --all
   git checkout 2026-tokyo-1
   ```
2. 適宜 [ビルド](#build) して内容を確認しましょう。
   ```bash
   ./scripts/build.sh
   ```
3. 完成したらコミットしましょう。
   ```bash
   git add src/contents/2026/tokyo/1.tex
   git commit -m "2026年東大第1問の解答を作成"
   git push origin 2026-tokyo-1
   ```
4. [プルリクエスト](#pull-request) を作成しましょう。

## Build

### ビルド方法

ビルドスクリプトは最大3つの引数を受け取ります。

```bash
./scripts/build.sh YEAR [UNIVERSITY] [PROBLEM]
```

| 引数 | 必須 | 説明 | 値 |
| :-- | :--: | :-- | :-- |
| `YEAR` | ⚪︎ | 年度 | `2026` \| `2027` \| ... |
| `UNIVERSITY` |  | 大学名 | `tokyo` \| `kyoto` \| `science-tokyo` |
| `PROBLEM` |  | 問題番号| `1` \| `2` \| `3` \| `4` \| `5` \| `6` |

### 使用例

年度のみを指定した場合、その年度のすべてのtexファイルをコンパイルします。

```bash
./scripts/build.sh 2026
```

年度と大学名を指定した場合、その年度・大学のすべてのtexファイルをコンパイルします。

```bash
./scripts/build.sh 2026 tokyo
```

年度、大学名、問題番号を指定した場合、特定のtexファイルをコンパイルします。

```bash
./scripts/build.sh 2026 tokyo 1
```

## Pull Request

1. 変更内容を明確に説明してください
2. 関連するIssue番号を記載してください（Descriptionに `Fixes: #{Issue番号}` を含めてください。）
