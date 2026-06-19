# ToDo

## 完了
- [x] kumamuk-git/zmk-config-roBa を kokuda57 にfork <!-- 2026-06-19 macbookpro -->
- [x] ~/workspace/zmk-config-roBa にクローン <!-- 2026-06-19 macbookpro -->
- [x] CONFIG_ZMK_POINTING_DEFAULT_SCRL_VAL=5 を roBa_R.conf に追記 <!-- 2026-06-19 macbookpro -->
- [x] push & GitHub Actions ビルド起動 <!-- 2026-06-19 macbookpro -->

## 進行中 / 未完了
- [ ] GitHub Actions ビルド完了を確認し .uf2 をダウンロード <!-- 2026-06-19 macbookpro -->
- [ ] settings_reset → roBa_R → roBa_L の順で XIAO BLE に書き込み <!-- 2026-06-19 macbookpro -->
- [ ] スクロール速度 5 の体感確認（速度が合わなければ値を再調整）

## メモ・決定
- 2026-06-19 macbookpro: ZMK_POINTING_DEFAULT_SCRL_VAL は v0.3-branch では未定義シンボルのためビルドエラーになる。代わりに CONFIG_PMW3610_SCROLL_TICK で調整する（値を大きくするほど遅くなる）
- 2026-06-19 macbookpro: SCROLL_TICK=16（デフォルト）→ 32 に変更。1スクロールに必要なトラックボール移動量が2倍になり速度が半分になる
- 書き込み順序: settings_reset（両方）→ roBa_R → roBa_L
- 最新ビルドURL: https://github.com/kokuda57/zmk-config-roBa/actions/runs/27808759381
