# ToDo

## 進行中 / 未完了
- [ ] triggers-per-rotation=5 をビルドして XIAO BLE（左手）に書き込み、ページ送りの行き過ぎを実機確認 <!-- 2026-06-20 macbookpro -->

## 完了
- [x] エンコーダのページ送り行き過ぎ対策: triggers-per-rotation を 10→5 に変更（roBa.dtsi:112）<!-- 2026-06-20 macbookpro -->
- [x] ロータリーエンコーダのスクロール速度を遅くする方法を検討・実装 <!-- 2026-06-20 macbookpro -->
- [x] kumamuk-git/zmk-config-roBa を kokuda57 にfork <!-- 2026-06-19 macbookpro -->
- [x] ~/workspace/zmk-config-roBa にクローン <!-- 2026-06-19 macbookpro -->
- [x] settings_reset → roBa_R → roBa_L の順で XIAO BLE に書き込み <!-- 2026-06-20 macbookpro -->
- [x] 左右ペアリング確認済み <!-- 2026-06-20 macbookpro -->
- [x] SCROLL_TICK を 16（デフォルト）に戻す（トラックボール速度は変更不要と判断）<!-- 2026-06-20 macbookpro -->
- [x] MOUSEレイヤー左手 MB1 追加→不要のためリバート済み <!-- 2026-06-20 macbookpro -->

## メモ・決定
- 2026-06-19 macbookpro: ZMK_POINTING_DEFAULT_SCRL_VAL は v0.3-branch では未定義シンボルのためビルドエラーになる。代わりに CONFIG_PMW3610_SCROLL_TICK で調整する（値を大きくするほど遅くなる）
- 2026-06-20 macbookpro: ロータリーエンコーダは現在 inc_dec_kp PG_UP PAGE_DOWN にバインド。速度変更は OS 設定か msc バインドへの変更で対応可能
- 2026-06-20 macbookpro: エンコーダ感度ノブは roBa.dtsi の triggers-per-rotation（1回転あたりの発火回数）。steps=12 は物理パルス数なので触らない。10→5 で発火半減。両エンコーダレイヤー（PG_UP/DOWN, LC(PAGE_UP/DOWN)）共通に効く。まだ行き過ぎるなら 3 へ。エンコーダは左手側のみ有効（roBa_L.overlay）
- 2026-06-20 macbookpro: ZMK Studio での Mouse Key Press 反映は操作方法の問題だった（仕様理解で解決）
- 2026-06-20 macbookpro: gh auth の active アカウントが kyosuke-lab になっていると push が 403 になる。push 前に `gh auth switch --user kokuda57` が必要
- 現在のリポジトリ状態: upstream と同一（SCROLL_TICK=16、keymap 変更なし）
