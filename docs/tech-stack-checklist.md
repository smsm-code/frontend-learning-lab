# 技術スタック包括リスト(習得チェックリスト)

| | |
|---|---|
| 最終更新日 | 2026-07-15 |
| 前提バージョン | TypeScript 5.x / Svelte 5(Runes)/ SvelteKit 2 / Tailwind CSS v4 / Node.js LTS |
| インフラ前提 | Google Cloud Platform(GCP) |
| 見直しサイクル | 四半期ごと(1月・4月・7月・10月)。「What's new in Svelte」月次記事の確認とセットで行う |
| 対の文書 | `learning-roadmap.md`(各Phaseからこのリストの該当項目を参照する) |

---

## このリストの使い方

### 習得レベルの定義(4段階)

| レベル | 名称 | 到達基準 |
|---|---|---|
| **L0** | 未着手 | 名前を知っている程度 |
| **L1** | 触った | チュートリアルや写経で動かしたことがある |
| **L2** | 使える | 自分のプロジェクトで、独力で(調べながら)課題を解決できる |
| **L3** | 説明できる | 内部動作・設計思想・採用理由を、他人に平易に説明できる |

**L3を最上位に置く理由**: 「動かせる」と「わかっている」の間には大きな溝がある。面接・技術選定・障害対応で問われるのはL3の理解であり、記事執筆やレビューで他者に説明する行為そのものがL3への最短経路になる。

### 優先度の定義

- **◎ コア**: L3を目指す。プロとしての土台
- **○ 実務頻出**: L2で十分。必要になったらL3へ
- **△ 認知**: L0〜L1でよい。「名前と役割、何を置き換えるものか」を言えれば合格。**全部やろうとしないこと**(プロも全部は使いこなしていない)

### 記入例

`レベル` 列に現在値を記入し、更新日をメモする。GitHubで管理し、レベルが上がったらコミットする(コミット履歴=成長ログになる)。

---

## 1. Web標準・基盤(レイヤー1)

フレームワークは入れ替わるが、この層は腐らない。すべての「なぜ?」の答えがここにある。

| # | 項目 | 優先度 | レベル | L3の目安(これを説明できるか) |
|---|---|---|---|---|
| 1-1 | セマンティックHTML | ◎ | | なぜ `div` でなく `button`/`nav`/`main` を使うのか(a11y・SEOへの影響) |
| 1-2 | CSS基礎(カスケード/詳細度/ボックスモデル) | ◎ | | Tailwindのクラスが「何のCSSの略記か」を即答できる |
| 1-3 | Flexbox / Grid | ◎ | | レイアウト要件を見てどちらを使うか判断・説明できる |
| 1-4 | ブラウザのレンダリングパイプライン | ◎ | | パース→スタイル計算→レイアウト→ペイント→コンポジットの流れと、reflowが高コストな理由 |
| 1-5 | JSイベントループ / Promise / async-await | ◎ | | 「なぜsetTimeoutより先にPromiseが解決されるか」(タスク/マイクロタスク) |
| 1-6 | HTTP(メソッド/ステータス/ヘッダ/キャッシュ/Cookie) | ◎ | | `Cache-Control` の各ディレクティブの効果、CookieのSameSite属性の意味 |
| 1-7 | DNS・TLS・CDNの仕組み | ○ | | 「URLを入力してから画面が出るまで」を一通り語れる |
| 1-8 | Web API(fetch / FormData / URL / Intl 等) | ○ | | ライブラリなしで素のfetchでAPI通信を書ける |
| 1-9 | ブラウザDevTools(Elements/Network/Performance) | ◎ | | Performanceタブでボトルネックを特定できる |

## 2. 言語・フレームワーク(レイヤー2)

| # | 項目 | 優先度 | レベル | L3の目安 |
|---|---|---|---|---|
| 2-1 | TypeScript: strict設定・基本型・ユニオン | ◎ | | `strict: true` 下で `any` なしに書ける |
| 2-2 | TypeScript: 構造的部分型 | ◎ | | 名前的型付けとの違いと、`Pick`/`Omit` が機能する理由 |
| 2-3 | TypeScript: narrowing / 判別可能ユニオン | ◎ | | 「あり得ない状態を型で排除する」状態モデリングができる |
| 2-4 | TypeScript: ジェネリクス / 型推論 / `infer` | ○ | | ライブラリの型定義(.d.ts)を読んでAPIを理解できる |
| 2-5 | Svelte 5: Runes(`$state`/`$derived`/`$effect`) | ◎ | | シグナルの依存追跡の仕組み。`$effect` を乱用すべきでない理由 |
| 2-6 | Svelte 5: `$props()` / snippets / イベント | ◎ | | Svelte 4以前の書き方との違いを指摘できる(古い情報の判別) |
| 2-7 | Svelte: コンパイラであることの意味 | ◎ | | 仮想DOM不要の理由(コンパイル時に依存関係が静的に判明する)を説明できる |
| 2-8 | 共有状態パターン(`.svelte.ts`) | ○ | | ローカル/共有/サーバー/URL状態の使い分けを判断できる |
| 2-9 | Tailwind v4: ユーティリティファースト | ◎ | | 「デザイントークンの制約内で組む」思想。恣意値乱用がなぜアンチパターンか |
| 2-10 | Tailwind v4: CSSファースト設定(`@theme`) | ◎ | | v3(JS config)との違い。ダークモード(`@custom-variant`)の仕組み |
| 2-11 | OKLCH色空間 | △ | | HSLとの違い(知覚的均一性)を一言で言える |

## 3. アプリケーション構築(レイヤー3)

| # | 項目 | 優先度 | レベル | L3の目安 |
|---|---|---|---|---|
| 3-1 | SvelteKit: ルーティング / レイアウト | ◎ | | `+page` / `+layout` / グループの使い分け |
| 3-2 | SvelteKit: `load`(server / universal) | ◎ | | どちらで動くか・なぜその選択か(SSR/秘匿情報/ウォーターフォール回避) |
| 3-3 | SvelteKit: フォームアクション / Progressive Enhancement | ◎ | | JSなしでも動くフォームの価値と `use:enhance` の仕組み |
| 3-4 | SvelteKit: SSR / SSG / CSR / prerender の選択 | ◎ | | ページごとに「なぜこのレンダリング戦略か」を説明できる |
| 3-5 | SvelteKit: hooks / エラーハンドリング | ○ | | `handle` フックで認証ミドルウェアを書ける |
| 3-6 | SvelteKit: アダプタの仕組み | ○ | | adapter-node がCloud Runで動く理由(ビルド成果物=Nodeサーバー) |
| 3-7 | Zod / Valibot(スキーマバリデーション) | ◎ | | 「TSの型は実行時に消える」→ 境界で検証し `z.infer` で型を導出する原則 |
| 3-8 | sveltekit-superforms + formsnap | ○ | | サーバー/クライアント双方のバリデーション統合 |
| 3-9 | shadcn-svelte / Bits UI | ◎ | | ヘッドレスUI(振る舞い)とスタイルの分離。コード所有モデルの利点 |
| 3-10 | clsx + tailwind-merge(`cn()`) | ○ | | クラス衝突の解決がなぜ必要か |
| 3-11 | @lucide/svelte(アイコン) | ○ | | — |
| 3-12 | Drizzle ORM + SQLite / Cloud SQL | ○ | | ORMが生成するSQLを読める。N+1問題を説明できる |
| 3-13 | 認証(セッション vs JWT / OAuth 2.0 の流れ) | ◎ | | Cookieセッションの仕組みを自前実装レベルで理解(その上でライブラリを使う) |
| 3-14 | Better Auth / Identity Platform(Firebase Auth) | ○ | | GCP環境での認証の選択肢と使い分け |
| 3-15 | TanStack Query(svelte-query) | △ | | SvelteKit標準のデータフローで足りないケース(積極的キャッシュ/リアルタイム)の判断 |

## 4. 品質保証(レイヤー4)

| # | 項目 | 優先度 | レベル | L3の目安 |
|---|---|---|---|---|
| 4-1 | テスト戦略(ピラミッド/トロフィー) | ◎ | | 「何をテストし、何をしないか」を費用対効果で語れる |
| 4-2 | Vitest(ユニット/コンポーネント) | ◎ | | Vite設定を共有するため高速、という構造を説明できる |
| 4-3 | Testing Library(@testing-library/svelte) | ○ | | 「実装詳細でなくユーザー視点でテストする」哲学 |
| 4-4 | Playwright(E2E) | ◎ | | auto-wait がflaky test を減らす仕組み。Trace Viewerでのデバッグ |
| 4-5 | MSW(APIモック) | ○ | | ネットワーク境界でモックする利点(テスト/開発/Storybookで共有) |
| 4-6 | ESLint + Prettier + svelte-check | ◎ | | flat config の構造。svelte-check が何を検査するか |
| 4-7 | Biome / Oxlint(Rust製高速代替) | △ | | 何を置き換えるものか。Svelte対応の成熟度を確認してから採用判断 |
| 4-8 | アクセシビリティ(WAI-ARIA / キーボード操作) | ◎ | | スクリーンリーダーで自作アプリを操作した経験。axe-coreでの自動検査 |
| 4-9 | GitHub Actions(CI) | ◎ | | PRごとに lint / check / test / build を回すワークフローを書ける |
| 4-10 | セキュリティ: XSS / CSRF / CSP | ◎ | | `{@html}` が危険な理由。SvelteKitのCSRF対策の仕組み |
| 4-11 | Storybook / 視覚回帰テスト | △ | | デザインシステムが安定してから導入、という判断基準 |

## 5. インフラ・運用(レイヤー5)— GCP前提

学習用途では**無料枠と予算アラートの設定を最初に行うこと**(5-1)。Cloud Runはリクエストがない間は課金されないため、個人学習との相性が良い。

| # | 項目 | 優先度 | レベル | L3の目安 |
|---|---|---|---|---|
| 5-1 | GCP基礎(プロジェクト/IAM/課金/予算アラート) | ◎ | | サービスアカウントと最小権限の原則を説明できる |
| 5-2 | Cloud Run(SvelteKit + adapter-node + Docker) | ◎ | | コンテナのライフサイクル(コールドスタート/スケールto ゼロ/同時実行数) |
| 5-3 | Docker基礎(Dockerfile / マルチステージビルド) | ◎ | | イメージサイズ削減の理屈(レイヤーキャッシュ)。Node用Dockerfileを書ける |
| 5-4 | Artifact Registry | ○ | | コンテナイメージの保管とCloud Runへの連携 |
| 5-5 | Firebase Hosting / App Hosting | ○ | | 静的サイト・小規模SSRでのCloud Run直デプロイとの使い分け |
| 5-6 | Cloud Storage + Cloud CDN | ○ | | 静的アセット配信とキャッシュ戦略 |
| 5-7 | Secret Manager | ◎ | | 環境変数と秘密情報の管理。「APIキーをクライアントに出さない」実装 |
| 5-8 | Cloud SQL(PostgreSQL)/ Firestore | ○ | | RDBとNoSQLの使い分け。学習はローカルSQLite→Cloud SQLの順 |
| 5-9 | GitHub Actions → GCP デプロイ(Workload Identity連携) | ○ | | サービスアカウントキーを使わない認証がなぜ推奨か |
| 5-10 | Cloud Build | △ | | GitHub Actionsとの使い分け(GCP内完結CI) |
| 5-11 | Cloud Logging / Monitoring / Error Reporting | ○ | | 構造化ログの利点。アラート設定 |
| 5-12 | Sentry(フロントエンドエラー監視) | ○ | | Cloud Loggingとの役割分担(クライアント側エラーの捕捉) |
| 5-13 | Core Web Vitals(LCP / INP / CLS)+ Lighthouse CI | ◎ | | 各指標が何を測り、何が悪化させるか。計測→改善の実体験 |

## 6. 開発環境・ワークフロー

| # | 項目 | 優先度 | レベル | L3の目安 |
|---|---|---|---|---|
| 6-1 | Zed(Svelte拡張 / Tailwind LSP設定) | ◎ | | LSP(Language Server Protocol)の仕組み — エディタと言語サーバーの分離 |
| 6-2 | VS Code(サブ環境として) | ○ | | チーム開発でのVS Code前提環境(推奨拡張/Dev Containers)に対応できる |
| 6-3 | Git(ブランチ / rebase / conflict解決) | ◎ | | rebaseとmergeの違いを図で説明できる |
| 6-4 | GitHub Flow(PR / レビュー / Issue) | ◎ | | 個人開発でも常にPR経由でマージする習慣 |
| 6-5 | pnpm | ◎ | | コンテンツアドレス型ストレージ+ハードリンクの仕組み |
| 6-6 | Vite | ◎ | | 開発時(ネイティブESM)と本番(バンドル)の二段構え。SvelteKitとの関係 |
| 6-7 | Vite+ / Rolldown(統合ツールチェーン動向) | △ | | 業界の「Rust製・統合化」トレンドとして把握 |
| 6-8 | AI活用(コード生成のレビュー・判断) | ○ | | 生成コードの妥当性を自分の知識で検証する運用。学習初期は自力実装→比較 |
| 6-9 | Turborepo(モノレポ) | △ | | 必要になる規模感の判断 |

## 7. 拡張領域(Phase 4以降)

| # | 項目 | 優先度 | レベル | L3の目安 |
|---|---|---|---|---|
| 7-1 | React基礎(コンポーネント / hooks / JSX) | ○ | | Runesとhooksのリアクティビティモデルの違い(シグナル vs 再レンダリング) |
| 7-2 | Next.js(App Router / RSC の概念) | ○ | | SvelteKitとの概念対応表を自分で書ける。「なぜRSCが生まれたか」 |
| 7-3 | OSS貢献の作法(Issue / PR / CoC) | ○ | | 再現手順の書き方、メンテナとのコミュニケーション |
| 7-4 | 技術記事執筆 | ○ | | L3到達の手段として。日本語のSvelte 5情報は不足しており書く価値が高い |
| 7-5 | Web Components / 他FWとの相互運用 | △ | | — |
| 7-6 | i18n(Paraglide等) | △ | | — |
| 7-7 | PWA / Service Worker | △ | | — |

---

## 見直し時のチェック項目(四半期ごと)

1. 「What's new in Svelte」直近3ヶ月分を読み、影響のある変更をリストに反映したか
2. 前提バージョン(冒頭表)は現行のままか
3. △項目のうち、状況が変わって○に昇格すべきものはないか(例: BiomeのSvelte対応成熟)
4. レベルが3ヶ月間動いていない◎項目はないか → ロードマップの実践課題を見直す
