# Living Scent Ledger (LSL) — Participant Result Page

The participant-facing result page for Living Scent Ledger. The same QR card that starts a training session can be scanned later on the participant's own phone to view the result.

這是 Living Scent Ledger（生命氣味紀錄）的參與者結果頁。開始訓練時使用的 QR 卡片，之後可用參與者自己的手機再次掃描，查看結果。

---

## URL format / 網址格式

```
https://morggan-lgtm.github.io/LSL-Result/?c=LSL-0118
```

Query string rather than a path segment, because GitHub Pages has no server-side routing.

使用查詢字串而非 `/r/LSL-0118` 路徑，因為 GitHub Pages 是靜態主機，沒有伺服器端路由。

---

## Layout / 結構

```
index.html              Single-file result page; no dependencies or build step
results/<card_id>.json  One result file per participant
posters/<card_id>.jpg   Generated poster, resized to 1200px on its longest side
```

`index.html` is the result page, each JSON file holds one participant's result, and each JPEG is its generated poster.

`index.html` 是結果頁，每個 JSON 檔儲存一位參與者的結果，每張 JPEG 則是對應的生成海報。

## Data contract / 資料格式

```json
{
  "card_id": "LSL-0118",
  "created_at": "2026-11-20T17:42:00Z",
  "planet": {
    "id": "gj887b", "display_name": "GJ 887 b", "star_class": "M2V",
    "teq_k": 426, "mass_earth": 3.9, "tidally_locked": true,
    "descriptors": ["sulphurous / struck match / onsen egg"],
    "earth_memory": "Downwind of a hot spring: ...",
    "earth_memory_zh_tw": "站在溫泉的下風處：……"
  },
  "odour_vector":  {"volatility":0.62,"chemistry":0.13,"intensity":0.54,
                    "valence":0.73,"persistence":0.72},
  "planet_vector": {"volatility":0.756,"chemistry":0.265,"intensity":0.66,
                    "valence":0.087,"persistence":0.353},
  "scores": [{"planet_id":"gj887b","display_name":"GJ 887 b","p":0.2362}],
  "dialogue": "The pressure builds. A slow darkening of the east.",
  "dialogue_zh_tw": "壓力逐漸累積。東方緩緩暗了下來。",
  "poster": "posters/LSL-0118.jpg"
}
```

Sources / 來源:
- `planet.*` / `planet_vector` ← `LSL-M0/planets/<id>/params.json`
- `odour_vector` / `dialogue` ← M5 participant result / M5 參與者結果
- `scores` ← `p_*` columns in `LSL-M2-M3/results.csv` / `p_*` 欄位
- `poster` ← M5 image, converted to JPEG / M5 影像轉為 JPEG

The optional `earth_memory_zh_tw` and `dialogue_zh_tw` fields put Traditional Chinese after each English paragraph on the page.

可選的 `earth_memory_zh_tw` 和 `dialogue_zh_tw` 欄位，會在頁面的英文段落後顯示繁體中文。

## Page states / 頁面狀態

| State / 狀態 | When / 時機 |
|---|---|
| Result / 結果 | `results/<card_id>.json` exists / 檔案存在 |
| Pending / 生成中 | File unavailable; retry every 15 seconds / 檔案尚未可用；每 15 秒重試 |
| No card / 未指定卡片 | URL has no `?c=` / 網址沒有 `?c=` |
| No record / 查無紀錄 | Still unavailable after 20 attempts / 重試 20 次後仍無檔案 |

The page tries `raw.githubusercontent.com` first so a result can appear before the GitHub Pages build finishes. It falls back to the relative path.

頁面會先讀取 `raw.githubusercontent.com`，讓結果在 GitHub Pages 建置完成前就能顯示；若失敗則改用相對路徑。

---

## Privacy / 隱私

Card IDs are sequential and the URLs are guessable, so anyone can browse participant results. The result files contain no personally identifying information.

卡號是連號的，網址可以被猜到，因此任何人都能瀏覽參與者結果。結果檔不含可識別個人身分的資訊。

---

For project context, see `HANDOFF_scanner_and_result_page.md` in the main project.

專案背景請參閱主專案中的 `HANDOFF_scanner_and_result_page.md`。
