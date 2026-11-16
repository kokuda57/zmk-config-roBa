# 経緯

設定変更の経緯（いつ何をした・試したこと）。決定の理由は `docs/decisions.md`。

## ロータリーエンコーダ

- 2026-06-20: default 層のエンコーダは最初 `&inc_dec_kp PG_UP PAGE_DOWN`。速度は OS 設定か `&msc` への変更で変える想定だった（後に矢印キー行スクロールへ変更）
- 2026-06-20: ページ送りの行き過ぎ対策で `triggers-per-rotation` を 10→5→1 と減らした（1 = 1回転で1ページ送り、最小）が、
  実機は変わらなかった。原因は左手 roBa_L だけに書き込んでいたこと（エンコーダはセントラル＝右手が解釈する）
- 2026-06-20: 右手 roBa_R へ書き込み、`triggers-per-rotation` が効くことを確認
- 2026-06-20: 1 では遅すぎたので 3 にした（a9eef8f）。マウスホイール方式へ変えたときに、1ノッチの細かさを優先して 10 へ戻した（6381ee8）
- 2026-06-20: default 層を `&encoder_scroll`（`zmk,behavior-sensor-rotate`, bindings=`<&msc SCRL_UP>,<&msc SCRL_DOWN>`）へ変えて試した。
  pointing.h は include 済み・ZMK_POINTING=y。ARROW 層の LC(PAGE_UP/DOWN)（タブ移動）は維持。量は triggers-per-rotation と
  Mac のホイール速度で、方向が逆なら SCRL_UP/DOWN を入れ替えて直す想定だった → 暴走して見切った（理由は `docs/decisions.md`）
- 2026-06-20: default 層を矢印キー行スクロール `&inc_dec_kp UP_ARROW DOWN_ARROW`、triggers-per-rotation=10 にした（commit dc859cb, push 済み）。
  この時点の状態: ARROW 層は LC(PAGE_UP/DOWN) を維持、それ以外は upstream と同一（SCROLL_TICK=16）。
  2026-06-21 に automouse を無効化したので、それ以降は「upstream と同一」ではない

## ZMK Studio

- 2026-06-20: ZMK Studio で Mouse Key Press が反映されないと思ったのは操作方法の問題だった（仕様を理解して解決）
