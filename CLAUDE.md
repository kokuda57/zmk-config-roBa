# zmk-config-roBa 作業ルール

kumamuk-git/zmk-config-roBa の fork（`kokuda57/zmk-config-roBa`）。XIAO BLE 搭載の分割キーボード「roBa」。右手にトラックボール(PMW3610)、左手にロータリーエンコーダ。

## 設定変更の標準手順

設定を変更したら、以下の順で実機反映まで行う。

1. **編集** — 下表で対象ファイルを選ぶ
2. **commit** — 設定値のみの変更はレビュー不要。新規ファイル/関数追加・複数ファイル変更時は `code-reviewer` を通す
3. **push 前に必ず `gh auth switch --user kokuda57`** — active が `kyosuke-lab` だと push が 403
4. **push** → `git push origin main`
5. **GitHub Actions が自動ビルド**（約2分）
   - `gh run list -R kokuda57/zmk-config-roBa -L 1 --json databaseId,status,conclusion`
   - `gh run watch <run-id> -R kokuda57/zmk-config-roBa --exit-status`
6. **uf2 取得** — `gh run download <run-id> -R kokuda57/zmk-config-roBa -D <dir>`
7. **書き込み（手動・ユーザー作業）** — 対象の XIAO BLE をリセット**2回押し**でボリュームをマウント → 該当 uf2 をドラッグ&ドロップ。**settings_reset 不要・ペアリング維持**

## ファイルの役割

| ファイル | 役割 |
|---|---|
| `config/roBa.keymap` | キー配列・レイヤー・ビヘイビア・トラックボール挙動（automouse-layer / scroll-layers）の本体 |
| `boards/shields/roBa/roBa.dtsi` | 左右共通のハード定義（エンコーダ `triggers-per-rotation` 等） |
| `boards/shields/roBa/roBa_R.overlay` / `roBa_L.overlay` | 右手/左手 固有のハード（トラックボール・エンコーダ有効化） |
| `boards/shields/roBa/roBa_R.conf` / `roBa_L.conf` | Kconfig（機能フラグ・PMW3610 感度等） |

## どちらの手に書き込むか（重要）

**右手 (roBa_R) がセントラル**（`CONFIG_ZMK_SPLIT_ROLE_CENTRAL=y`）。トラックボール・エンコーダ感度・automouse など**ポインティングとセンサ解釈はすべて右手が処理する**。左手はペリフェラルで生データを転送するだけ。

- トラックボール / エンコーダ / automouse / スクロール系の変更 → **右手 roBa_R に書き込む**（左手だけ書いても無変化）
- 左手側のキーやハード固有設定 → 左手 roBa_L
- 不明なら両手に書く

## 既知のハマりどころ

- `ZMK_POINTING_DEFAULT_SCRL_VAL` は v0.3-branch で未定義シンボル → ビルドエラー。スクロール速度は `CONFIG_PMW3610_SCROLL_TICK`（大きいほど遅い）で調整
- PMW3610 ドライバ（kumamuk-git/zmk-pmw3610-driver）の automouse 関連プロパティは `automouse-layer` / `scroll-layers` / `snipe-layers` のみ。typing-idle ガードは無い。感度は `CONFIG_PMW3610_MOVEMENT_THRESHOLD`（大きいほど鈍感、0=即時）・`CONFIG_PMW3610_AUTOMOUSE_TIMEOUT_MS`（層の居座り時間）で調整。`automouse-layer = <(-1)>` で完全無効
- `&msc`（マウススクロール）はエンコーダと相性が悪い（時間ベースで暴走しやすい）。離散スクロールは `&inc_dec_kp` を使う

## Git

- author: `kokuda57` / `k.okuda57@gmail.com`、gh active: `kokuda57`
- push は明示指示時のみ。`--no-verify`・`--amend` は明示指示時のみ
- セッション跨ぎの状態・決定は `ToDo.md` に記録（グローバル CLAUDE.md 準拠）
