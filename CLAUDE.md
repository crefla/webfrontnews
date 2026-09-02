# webfrontnews

このリポジトリは、HTML/JS仕様(WHATWG HTML Living Standard, ECMAScript/TC39 proposals,
MDN/Baseline)の変更を日次で監視するためのステート置き場です。

## 日次チェックタスクへの指示

「HTML/JS仕様の変更を毎日チェックする」スケジュールタスクが起動したら、以下の手順に従うこと。

1. `spec-watch/state.json` を読み、各ソースの `last_seen_sha` を確認する。
2. 各ソースの現在のHEADコミット(またはtc39は `README.md` への最新コミット)を取得する。
   - WHATWG HTML: https://github.com/whatwg/html (branch: main)
   - TC39 proposals: https://github.com/tc39/proposals (README.md の変更履歴。Stage 4 = Finished proposals入り、既存提案のステージ変更に注目)
   - Baseline: https://github.com/web-platform-dx/web-features (branch: main。新機能追加やbaseline_status変更に注目)
   - 上記に加えMDN Web Docsの関連ページの更新も可能な範囲で確認する。
   - GitHub MCPツールはこのセッションでは `crefla/webfrontnews` にしかアクセスできないため、
     上記3リポジトリの参照には `WebFetch`(github.comのcommits画面など)を使うこと。
     `api.github.com` は本セッションのプロキシ経由ではアクセスできない点に注意。
3. `last_seen_sha` から現在のHEADまでの間のコミットを見て、実質的な変更かどうかを判定する。
   - 実質的 = 新しいAPI/構文の追加、既存機能の廃止・非推奨化、構文変更、Baseline状態の変化など。
   - 表記ゆれ修正・editorialな文言修正のみのコミットは実質的な変更に含めない。
4. 実質的な変更が見つかった場合のみ、Slackの `#l-frontend` チャンネルに
   「何が変わったか」「影響範囲」を3行以内で要約して投稿する。変更がなければ投稿しない。
5. チェックが終わったら `spec-watch/state.json` の該当ソースの `last_seen_sha` / `checked_at` /
   `last_run_at` を更新し、**`main` ブランチに直接コミット・pushする**
   (このファイルはコードではなくステートデータのため、PRを経由せず直接pushしてよい)。
   これを怠ると翌日以降のチェックが差分を検出できなくなるため、必ず実施すること。
