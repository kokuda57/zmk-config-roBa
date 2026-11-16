# ToDo Archive

`ToDo.md` の「完了」から期限（既定7日）を過ぎた項目を機械的に移した記録。context には注入されない。

- [x] トラックボール移動での自動レイヤー切替を無効化（automouse-layer 4→-1, roBa.keymap:12）。誤クリック対策。クリック手段は別途用意済みのため automouse 不要。commit 13b8b49 / origin/main push 済み / 右手 roBa_R 書き込み完了 <!-- 2026-06-21 macmini -->
- [x] 設定変更の標準手順を CLAUDE.md にルール化（新規作成）。commit 618878b / push 済み <!-- 2026-06-21 macmini -->
- [x] エンコーダ default 層を矢印キー行スクロール(&inc_dec_kp UP_ARROW DOWN_ARROW, triggers-per-rotation=10)へ変更し実機で「完璧」確認。commit dc859cb / 右手(roBa_R)書き込み済み <!-- 2026-06-20 macbookpro -->
- [x] エンコーダのページ送り行き過ぎ対策: triggers-per-rotation を 10→5 に変更（roBa.dtsi:112）→ commit a5918b4 / origin/main へ push 済み <!-- 2026-06-20 macbookpro -->
- [x] ロータリーエンコーダのスクロール速度を遅くする方法を検討・実装 <!-- 2026-06-20 macbookpro -->
- [x] kumamuk-git/zmk-config-roBa を kokuda57 にfork <!-- 2026-06-19 macbookpro -->
- [x] ~/workspace/zmk-config-roBa にクローン <!-- 2026-06-19 macbookpro -->
- [x] settings_reset → roBa_R → roBa_L の順で XIAO BLE に書き込み <!-- 2026-06-20 macbookpro -->
- [x] 左右ペアリング確認済み <!-- 2026-06-20 macbookpro -->
- [x] SCROLL_TICK を 16（デフォルト）に戻す（トラックボール速度は変更不要と判断）<!-- 2026-06-20 macbookpro -->
- [x] MOUSEレイヤー左手 MB1 追加→不要のためリバート済み <!-- 2026-06-20 macbookpro -->
