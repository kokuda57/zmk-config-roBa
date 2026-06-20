# ToDo

## 進行中 / 未完了
（なし）

## 完了
- [x] エンコーダ default 層を矢印キー行スクロール(&inc_dec_kp UP_ARROW DOWN_ARROW, triggers-per-rotation=10)へ変更し実機で「完璧」確認。commit dc859cb / 右手(roBa_R)書き込み済み <!-- 2026-06-20 macbookpro -->
- [x] エンコーダのページ送り行き過ぎ対策: triggers-per-rotation を 10→5 に変更（roBa.dtsi:112）→ commit a5918b4 / origin/main へ push 済み <!-- 2026-06-20 macbookpro -->
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
- 2026-06-20 macbookpro: エンコーダ感度ノブは roBa.dtsi の triggers-per-rotation（1回転あたりの発火回数）。steps=12 は物理パルス数なので触らない。両エンコーダレイヤー（PG_UP/DOWN, LC(PAGE_UP/DOWN)）共通に効く。エンコーダは左手側のみ有効（roBa_L.overlay）。10→5→1 と段階的に減らした。1 = 1回転で1ページ送り（最小）
- 2026-06-20 macbookpro: ZMK Studio での Mouse Key Press 反映は操作方法の問題だった（仕様理解で解決）
- 2026-06-20 macbookpro: gh auth の active アカウントが kyosuke-lab になっていると push が 403 になる。push 前に `gh auth switch --user kokuda57` が必要
- 2026-06-20 macbookpro: 【重要・訂正】エンコーダ感度(triggers-per-rotation)はセントラル＝右手(roBa_R, CONFIG_ZMK_SPLIT_ROLE_CENTRAL=y)が解釈する。左手はペリフェラルで生の回転を転送するだけ。よってエンコーダ設定変更は【右手 roBa_R に書き込む】必要がある。左手だけ書き込んでも無変化（10→5→1 が効かなかった原因）。トラックボールも右手側。
- 2026-06-20 macbookpro: 実機更新手順 = push → GitHub Actions 自動ビルド（約2分）→ `gh run download <run-id> -R kokuda57/zmk-config-roBa -D <dir>` で uf2 取得 → 対象 XIAO BLE をリセット2回押しでマウント → 該当 uf2 をドラッグ&ドロップ。settings_reset 不要・ペアリング維持
- 2026-06-20 macbookpro: 右手書き込みで triggers-per-rotation が効くことを確認。PG_UP/PAGE_DOWN は1ページ固定キーのため「1/3ページ」等のサブページ移動は不可。サブページ移動はマウスホイールスクロール化が必要
- 2026-06-20 macbookpro: default層エンコーダを &encoder_scroll（zmk,behavior-sensor-rotate, bindings=<&msc SCRL_UP>,<&msc SCRL_DOWN>）へ変更。pointing.h は既にinclude済・ZMK_POINTING=y。ARROW層の LC(PAGE_UP/DOWN)（タブ移動）は維持。スクロール量調整ノブ: triggers-per-rotation（多→少で量減）＋ Mac のホイール速度。方向が逆なら SCRL_UP/DOWN を入替
- 2026-06-20 macbookpro: &msc(マウススクロール)はエンコーダと相性が悪い。時間ベース(押下中スクロール継続)のため、sensor-rotate tap-ms=5msで無反応・30msで暴走（押しっぱなし扱い）。安定窓が狭く実用困難。→ msc方式は見切った。（参考: SCRL_UP=MOVE_Y(10)で量はゼロではない、zmk,behavior-sensor-rotate は v0.3に存在）
- 2026-06-20 macbookpro: 「1ノッチ1/3ページ」厳密はキーボード側で不可（1ページの行数がアプリ/ウィンドウ依存）。近似のみ。採用: 矢印キー行スクロール &inc_dec_kp UP_ARROW DOWN_ARROW（離散keypressで確実・暴走なし）。1ノッチの行数は triggers-per-rotation で調整、足りなければ1トリガ複数行のマクロ化
- 現在のリポジトリ状態: default層エンコーダ=矢印キー行スクロール(&inc_dec_kp UP_ARROW DOWN_ARROW), triggers-per-rotation=10（commit dc859cb push 済み）。ARROW層は LC(PAGE_UP/DOWN) 維持。それ以外は upstream と同一（SCROLL_TICK=16）
