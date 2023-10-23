# llama-trial

## quick-start 

- [replicate](https://replicate.com/)にGithubアカウントでログイン
- [api-tokens](https://replicate.com/account/api-tokens)からAPIキーを取得
- `REPLICATE_API_TOKEN`という名前で環境変数に登録
- 下記を実行

```python
import replicate

output = replicate.run(
    "replicate/llama-2-70b-chat:2c1608e18606fad2812020dc541930f2d0495ce32eee50074220b87300bc16e1",
    input={"prompt": "入力"}
)
```

## 検証

- 各種制約
    - 短時間に大量のリクエストを送るとエラーが起きる（無料枠の場合） cf. https://qiita.com/dpnk_yk0726/items/588389291e318ba2c334
    - 課金の場合、リクエスト数ではなくて実行時間に従って課金されるらしい。
    - ハードが複数用意されており、ハードによってprice (per seconds)が変わってくる
- 日本語は扱えるか？
    - 入力を日本語にして「日本語で出力して」といっても出力は英語 → 70bでダメなのでダメっぽい。
- ランタイム
    - "Describe the difference between apples and oranges?"といった短い文章でも30秒近くかかる
    - 要約とかになると1レスポンスで50秒近くかかる

# deepl API

- [DeepL](https://www.deepl.com/ja/pro-api?cta=header-pro-api)からアカウント作成、API利用登録を済ませると利用できるようになる

e.g.
```sh
curl -X POST 'https://api-free.deepl.com/v2/translate' \
--header 'Authorization: DeepL-Auth-Key [yourAuthKey]' \
--header 'Content-Type: application/json' \
--data '{
  "text": [
    "Hello, world!"
  ],
  "target_lang": "DE"
}'
```

```sh
{
  "translations": [
    {
      "detected_source_language": "EN",
      "text": "Hallo, Welt!"
    }
  ]
}
```
