# gyumeshi-rader-data

牛めしレーダーアプリ向けの店舗データ配信リポジトリ。
GitHub Pages で JSON を公開し、アプリから取得する。

## 方針

### 配信ファイル

| ファイル | 内容 |
|---------|------|
| `version.json` | データバージョン・更新日時・各JSONのURL。アプリは起動時にこれだけ fetch してローカルと比較する |
| `map_data.json` | 全店舗の位置情報（ID下4桁, ローマ字名, 緯度経度, 営業時間, ステータス） |
| `limited_shops.json` | 店舗限定メニューのキャンペーン情報と対象店舗ID |

### version.json の想定スキーマ

```json
{
  "version": "2026-03-07T15:00:00+09:00",
  "map_data_url": "https://gyumesy.github.io/gyumeshi-rader-data/map_data.json",
  "limited_url": "https://gyumesy.github.io/gyumeshi-rader-data/limited_shops.json"
}
```

### 更新フロー

1. `gyumeshi-rader-batch` (GAS) が15分ごとに shop.json / limited.json を取得
2. map_data.json / limited_shops.json に変換
3. GitHub API でこのリポジトリに push
4. GitHub Pages で自動公開

### GitHub Pages 設定

- ソース: `main` ブランチ / ルート (`/`)
- URL: `https://gyumesy.github.io/gyumeshi-rader-data/`
