# Portfolio — Matsushima-A-830

個人開発で取り組んでいるプロダクトと検証活動をまとめたポートフォリオです。
**「設計をドキュメントで固め、テストと CI で守り、AI エージェントと分業して速く回す」** ことを一貫したテーマにしています。

## 自己紹介

ITエンジニア1年目です。現職ではマイクロサービス構成のシステムで、フロントエンド・バックエンド・DB の各領域を担当し、設計にも一部関わっています。
業務外では、カフェ特化SNS「ミツカフェ」を企画から本番運用まで一人で開発しています。あわせて、海外のAI技術を毎日検証して発信する活動も続けています。
職種は1つに絞らず、領域を横断してプロダクトに一貫して関われる環境を探しています。

---

## Highlights

| | プロジェクト | 一言で | 主な技術 | 公開 |
|---|---|---|---|---|
| ⭐ | [**ミツカフェ**（cafe_sns_site）](./projects/mitsu-cafe.md) | 「気分で見つかる、行きつけと繋がる」カフェ特化SNS。**設計〜本番運用まで単独で開発中** | Next.js 16 / TypeScript / Supabase(Postgres・RLS) / Playwright / GitHub Actions / Sentry | コード非公開（設計・判断を本リポジトリで公開） |
| | [**ai-100days**](./projects/ai-100days.md) | 海外のAI OSS・論文を **毎日1件、実際に動かして検証** し日本語で発信する100日チャレンジ | Claude Code Routines / Python / ローカルLLM / Zenn連携 | [Public](https://github.com/Matsushima-A-830/ai-100days) |
| | [**forget-bench**](./projects/forget-bench.md) | LLMエージェントの「覚える力・忘れる力・コスト」を、テキスト層とKVキャッシュ層で比較するベンチマーク | Python / uv / transformers / Ollama / Claude | [Public](https://github.com/Matsushima-A-830/forget-bench) |

### 数字で見る

| ミツカフェ（2026-09-03 着手） | |
|---|---|
| 実装済み画面 / 設計上の画面 | **37 / 37** |
| テーブル / マイグレーション / RLSポリシー | **27 / 74 / 100超** |
| テストファイル（うち統合 / E2E） | **184**（49 / 26） |
| マージ済み PR | **144** |
| GitHub Actions ワークフロー | **11**（CI・E2E・統合・マイグレーション承認ゲート・夜間検査・AIレビュー 等） |
| 設計ドキュメント | 約 **11,000行**（戦略・データモデル・画面遷移・ワイヤー37画面・運用手順） |
| 運用状況 | **招待制の検証ベータとして本番稼働中**（Vercel + Supabase Cloud + 独自ドメイン + Resend + Sentry） |

| ai-100days（2026-09-28 開始） | |
|---|---|
| 検証した日数 | **56日**（2026-11-23 時点・継続中） |
| マージ済み PR | **192** |

---

## 強み

### 1. プロダクトを「戦略から」設計できる
差別化の軸（気分起点の発見 × オーナーとの信頼関係）を先に言語化し、すべての機能判断をそこに立ち返らせています。
「やらないこと」（フォロー中心フィード、映えフィルタ、DM 等）も明文化しました。
→ [ミツカフェ: プロダクト戦略](./projects/mitsu-cafe.md#1-プロダクト戦略)

### 2. 品質を仕組みで担保する
TDD を主軸に、Zod による境界バリデーション、RLS への認可委譲、Result 型のエラーカタログ、デザインシステム違反を検出する独自 Lint を CI と pre-commit の両方で強制しています。
→ [品質を守る仕組み](./projects/mitsu-cafe.md#4-品質を守る仕組み)

### 3. 本番で起きた問題を記録し、再発を防ぐ
初回本番デプロイで判明した Auth 設定の非同期（全ユーザーに影響する不具合）や、定期ジョブが数日間失敗していた問題などを、原因・対応・教訓まで残しています。
→ [障害対応と学び](./projects/mitsu-cafe.md#6-障害対応と学び)

### 4. AI エージェントと「安全に」分業する
Claude Code にプロジェクト固有のスキル（実装・レビュー・引き継ぎ等 10種）を持たせ、
「1画面 = 1PR = 1セッション」の開発サイクルを定型化しました。
CI 上の無人実装エージェントには **権限を持たせないことで制御する** 設計（push 権限の後注入、変更範囲の機械判定、プロンプトインジェクション対策）を入れています。
→ [AI 協働開発の型](./docs/ai-driven-development.md)

### 5. 計測し、正直に書く
「動かしていないものを動いたと書かない」を全プロジェクト共通のルールにしています。
CI の課金分を分単位で実測してパイプラインを削る、ベンチマークの全数値に seed・モデル revision・commit を記録する、などがその実践です。

---

## スキルセット

| 領域 | 技術 | 実務的に使った場面 |
|---|---|---|
| フロントエンド | Next.js (App Router) / React 19 / TypeScript strict / Tailwind CSS / shadcn/ui / Tiptap | ミツカフェ 37画面、レスポンシブ（スマホ/タブレット/PC） |
| バックエンド | Supabase（Auth / Postgres / Storage） / Server Actions / Route Handlers / Zod | 認証・年齢確認・投稿・通報・オーナー認証 |
| データベース | PostgreSQL / RLS / トリガー / PostGIS / pg_trgm 全文検索 | 27テーブル・74マイグレーション、認可をRLSに集約 |
| テスト | Vitest / React Testing Library / Playwright / pytest | ユニット・統合（実DB）・E2E の3層 |
| CI/CD・運用 | GitHub Actions / Vercel / Sentry / Dependabot / lefthook / commitlint | 承認ゲート付きDBマイグレーション、夜間ジョブ、日次バッチ |
| AI / LLM | Claude Code（Skills・Routines・Actions） / Ollama / Hugging Face transformers / RAG / KVキャッシュ操作 | AI協働開発、自動検証パイプライン、メモリ戦略ベンチマーク |
| その他 | Python / uv / Google Maps Platform / Resend / Cloudflare DNS / WSL2 + CUDA | |

---

## ドキュメント

- [ミツカフェ ケーススタディ](./projects/mitsu-cafe.md)
- [ai-100days](./projects/ai-100days.md)
- [forget-bench](./projects/forget-bench.md)
- [AI 協働開発の型](./docs/ai-driven-development.md)
- [面接で話せるトピック集](./docs/talking-points.md)

## 連絡先

- Email: matsu120a40@gmail.com
- GitHub: [@Matsushima-A-830](https://github.com/Matsushima-A-830)
- Zenn: [matsushima_a](https://zenn.dev/matsushima_a)（技術記事: ai-100days の検証結果）
- note: [regal_poppy7370](https://note.com/regal_poppy7370)（検証の経緯・振り返り）

> ミツカフェのソースコードと稼働中の環境は非公開です。選考の場では画面共有でのデモ・コードの説明が可能です。
