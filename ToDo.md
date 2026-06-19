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
- 2026-06-19 macbookpro: スクロール速度はデフォルト10より遅くしたいとのことで5を選択。ZMK_POINTING_DEFAULT_SCRL_VAL は roBa_R.conf（Central側・トラックボール側）に CONFIG_ プレフィックスで追記する
- ビルド結果URL: https://github.com/kokuda57/zmk-config-roBa/actions/runs/27807921675
- 書き込み順序: settings_reset（両方）→ roBa_R → roBa_L
