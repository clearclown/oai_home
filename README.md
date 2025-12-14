# oai_home

OpenAI Operator のホームディレクトリ設定リポジトリ。Operator エージェントが動作するコンテナ環境（`/home/oai`）の初期設定ファイル群を管理する。

## 概要

OpenAI Operator は、ブラウザを操作できる AI エージェントである。このリポジトリは、その実行環境となる Linux コンテナのホームディレクトリ構成を定義している。

## ディレクトリ構成

```
.
├── .bashrc / .profile / .bash_logout   # シェル設定
├── .chromium/                          # Chromium ブラウザ設定
├── .config/openbox/                    # OpenBox ウィンドウマネージャー設定
├── .ipython/                           # IPython 設定
├── .pki/                               # PKI/証明書関連
├── redirect.html                       # ブラウザリダイレクト用ページ
├── share/
│   └── slides/                         # スライド変換ツール
│       ├── render_slides.py            # PPTX → PNG 変換
│       ├── create_montage.py           # モンタージュ画像生成
│       └── ensure_raster_image.py      # ラスター画像保証
└── skills/                             # エージェントスキル定義
    ├── docs/                           # DOCX 操作ガイド
    ├── pdfs/                           # PDF 操作ガイド
    └── spreadsheets/                   # スプレッドシート操作ガイド
```

## 主要コンポーネント

### 環境設定

- **シェル設定**: Bash の履歴管理、プロンプト設定、NVM 統合
- **OpenBox**: デコレーションなし・最大化状態でウィンドウを表示（ヘッドレス GUI 用）
- **Chromium**: ブラウザ自動操作用の設定プリセット

### ツール (`share/slides/`)

PowerPoint ファイルを PNG 画像に変換するユーティリティ群。LibreOffice と pdf2image を使用。

| ファイル | 機能 |
|---------|------|
| `render_slides.py` | PPTX → PDF → PNG 変換（DPI 自動計算） |
| `create_montage.py` | 複数スライドのモンタージュ生成 |
| `ensure_raster_image.py` | ラスター画像形式への変換保証 |

### スキル定義 (`skills/`)

エージェントがドキュメントを作成・編集する際のガイドライン。

| スキル | 概要 |
|--------|------|
| `docs/` | DOCX の読み取り・作成・レビュー手順（python-docx, LibreOffice 使用） |
| `pdfs/` | PDF の読み取り・作成手順（reportlab, pdftoppm 使用） |
| `spreadsheets/` | Excel/CSV の操作ガイド（openpyxl, artifact_tool 使用） |

## 技術スタック

- **OS**: Linux (Debian ベース)
- **ウィンドウマネージャー**: OpenBox
- **ブラウザ**: Chromium
- **ドキュメント変換**: LibreOffice (headless)
- **Python ライブラリ**: python-docx, reportlab, openpyxl, pdf2image, pdfplumber

## ライセンス

Copyright (c) OpenAI. All rights reserved.
