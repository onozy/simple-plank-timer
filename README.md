# プランクタイマー（PWA）

体幹トレーニング「プランク」用のタイマー + カレンダー履歴。
スマホのホーム画面に追加すると、アプリのように全画面・オフラインで動きます。

## 機能
- キープ時間 / セット数 / 休憩時間を選んでスタート（設定は保存される）
- 残り3秒ビープ・切り替え音・バイブ、画面スリープ防止（対応ブラウザ）
- 完了すると自動でその日の履歴に記録
- カレンダーで実施日を確認、日をタップで詳細・削除・手動追加
- 連続日数 / 今月の実施日 / 累計時間

履歴は端末内（localStorage）に保存されます。サーバーには送りません。

## スマホに入れる手順

### 1. どこかに公開する（HTTPS が必要）
一番手軽なのは GitHub Pages：

```sh
cd simple-plank-timer
git init && git add . && git commit -m "plank timer"
gh repo create simple-plank-timer --public --source=. --push
gh api -X POST repos/{owner}/simple-plank-timer/pages -f build_type=legacy -f 'source[branch]=main' -f 'source[path]=/'
```
数分後に `https://<ユーザー名>.github.io/simple-plank-timer/` で開けます。

（同じ Wi-Fi の中だけで試すなら `python3 -m http.server 8000` でも動きますが、
ホーム画面追加・オフラインは HTTPS か localhost のみです）

### 2. ホーム画面に追加
- **iPhone (Safari)**: 共有ボタン → 「ホーム画面に追加」
- **Android (Chrome)**: メニュー → 「ホーム画面に追加」/「アプリをインストール」

## ローカルで確認
```sh
python3 -m http.server 8000
# → http://localhost:8000
```
