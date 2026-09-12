# プランクタイマー（PWA）

体幹トレーニング「プランク」用のタイマー + カレンダー履歴。
スマホのホーム画面に追加すると、アプリのように全画面・オフラインで動きます。

## 機能
- **プラン**：秒数の違う種目を並べた一連のメニューを、最初から最後まで通しで実行
- 休憩時間 / 音のオン・オフを選んでスタート（設定は保存される）
- 残り3秒ビープ・切り替え音・バイブ、画面スリープ防止（対応ブラウザ）
- 完了すると自動でその日の履歴に記録
- カレンダーで実施日を確認、日をタップで詳細・削除・手動追加
- 連続日数 / 今月の実施日 / 累計時間

### プラン
| プラン | 内容 |
|---|---|
| Week 1 | フロントプランク 30秒 × 3セット |
| Week 2 | フロントプランク 45秒 × 3セット |
| Week 3 | フロントプランク 60秒 × 3セット |
| Week 4 | フロント 60秒 × 2セット ＋ サイド 20秒 × 左右 |
| 維持 | フロント 60秒 × 3セット ＋ サイド 30秒 × 左右 |
| カスタム | キープ時間とセット数を自分で選ぶ（従来どおり） |

セットの間にはすべて「休憩」で選んだ秒数が入ります。
種目が切り替わる休憩明け（左→右など）は音とバイブのパターンを変えて知らせます。

プランを増やす・秒数を変えるときは `index.html` の `PLANS` 配列を編集します。

```js
{id:'w4', label:'Week 4', desc:'フロント60秒×2 ＋ サイド20秒×左右',
 steps:[{name:'フロントプランク', hold:60, sets:2},
        {name:'サイドプランク（左）', hold:20, sets:1},
        {name:'サイドプランク（右）', hold:20, sets:1}]}
```

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
