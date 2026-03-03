# 🔮 Code-Grimoire-Core

<!-- ここにプロジェクトの簡単な説明を書きます。必要に応じてバッジ（CIステータスやライセンスなど）を貼るのもおすすめです -->
このプロジェクトは、VS Code上でコードの依存関係を「魔方陣」として美しく可視化するプラットフォームの中核（描画・オーケストレーションエンジン）です。

PixiJS (WebGL) と d3-force の力学シミュレーションを活用し、数万ファイル規模のプロジェクトでも60fpsを維持する圧倒的な描画パフォーマンスを提供します。
本リポジトリは**描画・UIレイヤーに特化**しており、実際のソースコード解析は各言語向けのプラグイン拡張機能（例: `code-grimoire-ts`）に委譲する「クリーンアーキテクチャ（プラグイン方式）」を採用しています。

## ✨ この基盤の役割と仕組み

Code-Grimoire-Core は、他の拡張機能からデータを受け取るための**VS Code API (`exports`)** を公開しています。
他言語対応プラグインは、AST解析などで生成した依存関係データを共通のスキーマフォーマット（Universal Node/Edge）に変換し、このCoreエンジンのAPIへ送信することで、任意の言語の魔方陣を展開できるようになります。

プラグイン開発者向けのAPI仕様については [docs/api-design.md](docs/api-design.md) を参照してください。

---

## 💻 開発環境の構築手順

このプロジェクトは VS Code 拡張機能として動作し、UIの描画には Webview を使用しています。

1. **依存関係のインストール**
   ```bash
   npm install
   ```

2. **ビルドとウォッチ（監視）の開始**
   esbuildを使用してExtension側のコードとWebview側のコードをバンドルします。
   ```bash
   npm run watch
   ```

3. **開発サーバーの起動（デバッグ）**
   VS Code上で `F5` キーを押すか、Run & Debug パネルから「Run Extension」を実行します。
   新しい VS Code ウィンドウ（Extension Development Host）が起動し、拡張機能がテスト可能な状態になります。

## 📁 主要なディレクトリ構成

プラグインアーキテクチャを実現するため、VS Code拡張機能のバックエンド層と、描画を担うWebview層を明確に分離しています。

```text
.
├── .vscode/          # VS Code のデバッグ・タスク設定
├── docs/             # 共通データスキーマなどのAPIドキュメント
├── src/
│   ├── extension/    # VS Code 拡張機能のコアロジック (APIの公開, Webviewの管理)
│   ├── webview/      # UI・描画レイヤー (PixiJS, d3-force, レンダリングロジック)
│   └── shared/       # ExtensionとWebviewで共有する型定義 (APIスキーマなど)
├── tests/            # 単体テスト・結合テストコード
├── esbuild.js        # バンドラの設定スクリプト
└── README.md         # このファイル
```

## 🤝 コントリビューション

このプロジェクトへの貢献（バグ報告や機能追加など）については、[CONTRIBUTING.md](CONTRIBUTING.md) のガイドラインをご一読ください。
プラグイン開発者からの「コア側でこんなAPIを公開してほしい」「こんな情報をWebviewに渡してほしい」といった要望（Feature Request）も歓迎しています。

また、健全なコミュニティを維持するため、[行動規範 (CODE_OF_CONDUCT.md)](CODE_OF_CONDUCT.md) への準拠をお願いしています。

## 📄 ライセンス

このプロジェクトは [MIT License](LICENSE) のもとで公開されています。