# GENIACプロジェクト team kumagai コントリビューションガイド

このドキュメントでは、GENIAC kumagaiチームのコントリビューションに関するルールを説明します。
プロジェクトメンバーは、このガイドラインに従ってコントリビューションを行ってください。

## GitHub運用ルール

### ブランチ構成

- `dev` : 開発用ブランチ（各自の作業を取り込む場所）
  - 各自のブランチから `dev` へのプルリクエストは、チーム内の有識者によるレビューが必須
  - ただし、`dev` ブランチは最悪壊れても良いブランチです。
- `pre` : 検証環境用ブランチ（1Bまで）
  - `dev` から `pre` へのブランチ間マージは、チームを跨いだ有識者のレビューが必須
  - 壊れてはいけないブランチです。
- `main` : 本番用ブランチ（10B）
  - `pre` から `main` へのブランチ間マージは、チームを跨いだ有識者のレビューが必須
  - 壊れてはいけないブランチです。

### レビュワー

- modelチーム: MoEはkumagai、松尾研repoは確認中
- dataチーム: coreメンバー(fukuda / omori)
- evalチーム: coreメンバー(4名でクロスレビュー)

### コーディングスタイル

- linterの導入は後回しで良いが、将来的には以下のlinterを導入予定
  - Python: ruff
  - Shell Script: shellcheck

### リポジトリ構成

マルチリポ
- 松尾研のforkリポ
- moe-recipe派生リポ

備考: リリースタイミングが異なるため別リポジトリに分ける

## HuggingFace運用ルール

### 組織とリポジトリ

- 組織: https://huggingface.co/geniacllm
- spaces: modelが動くchatなどをpushする場合（おそらく最後まで使わない）
- models: 作成したmodel, tokenizerをpush
- datasets: 作成した事前学習、事後学習結果をpush

### モデルとデータセットのアップロード

- 学習結果はこまめにチェックポイント(ckpt)をアップロードする
- 組織の容量制限に引っかかるまではこまめにアップロードする
- tokenizerもHuggingFaceに保存する

### 命名規則

- 命名規則は決めていないが、iterationの数字部分を入れると読み込みがうまくいかない可能性がある
- 大変でなければ後から変更しても良い

## Weights & Biases (wandb) 運用ルール

### 組織とプロジェクト

- 組織: https://wandb.ai/geniac_kumagai
- プロジェクト名:
  - {model}
  - {model}_finetuning
  - {model}_{tokenizer}_{data} (使用するdataやtokenizerが決まったら、プロジェクト名で管理)

### 実験の命名規則

- プロジェクト内の実験名:
  - 名前
  - 学習率などのパラメータ

### 実験の進め方

- 評価チームは finetuning のみ使う
- プロジェクトを作るときに、利用するtokenizerを記載してディレクトリ構成と一致させる

## GCP環境と共有フォルダ構成

### フォルダ構成

```directory-structure
team_kumagai/
├── data/
├── tokenizer/
│   ├── tokenizer1/
│   └── tokenizer2/
└── model/
			├── Mixtral/
			│   ├── Mixtral_{説明}/
	    │   ├── iter_000250/
	    │   ├── iter_000500/
	    │   ├── iter_000750/
	    │   └── latest_iteration.txt
			└── Llama/
					├── ...
```

備考: [フォルダ構成候補](https://miro.com/welcomeonboard/b1p4b3cyQ2Fqd2xMN2JkM3c0UzBycHJFWXprWTVVdGZHd250dkV6V0JWeTlwdlVKak5CVzZMRFZlcFNVaENyOXwzNDU4NzY0NTc3Mjg1NTEyNDE1fDI=?share_link_id=703483708040)
