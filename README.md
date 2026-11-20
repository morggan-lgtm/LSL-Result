# LSL — Participant Result Page

Limbic Sensing Laboratory 展覽的參與者結果頁。
參與者在展場入口用卡片上的 QR code 開始訓練，離場後用**同一張卡**、自己的手機再掃一次，
就會開啟這個頁面看到自己的結果。

The participant-facing result page for the Limbic Sensing Laboratory exhibition.
The same QR card that starts a training session doubles as the link to that
participant's own result — scanned later on their own phone.

---

## 網址格式 / URL format

```
https://morggan-lgtm.github.io/LSL-Result/?c=LSL-0118
```

用查詢字串而不是 `/r/LSL-0118`，因為 GitHub Pages 是純靜態主機，沒有伺服器端路由。
Query string rather than a path segment, because GitHub Pages has no server-side routing.

---

## 結構 / layout

```
index.html              結果頁本身(單一檔案,零依賴,無建置步驟)
results/<card_id>.json  一位參與者一個檔
posters/<card_id>.jpg   ComfyUI 生成的海報,縮到長邊 1200px(約 100 KB)
```

## 資料格式 / data contract

```json
{
  "card_id": "LSL-0118",
  "created_at": "2026-11-20T17:42:00Z",
  "planet": {
    "id": "gj887b", "display_name": "GJ 887 b", "star_class": "M2V",
    "teq_k": 426, "mass_earth": 3.9, "tidally_locked": true,
    "descriptors": ["sulphurous / struck match / onsen egg"],
    "earth_memory": "Downwind of a hot spring: ..."
  },
  "odour_vector":  {"volatility":0.62,"chemistry":0.13,"intensity":0.54,
                    "valence":0.73,"persistence":0.72},
  "planet_vector": {"volatility":0.756,"chemistry":0.265,"intensity":0.66,
                    "valence":0.087,"persistence":0.353},
  "scores": [{"planet_id":"gj887b","display_name":"GJ 887 b","p":0.2362}],
  "dialogue": "The pressure builds. A slow darkening of the east.",
  "poster": "posters/LSL-0118.jpg"
}
```

來源 / sources:
- `planet.*` / `planet_vector` ← `LSL-M0/planets/<id>/params.json`
- `odour_vector` / `dialogue` ← M5 的 `<participant_id>_<planet>_result.json`
- `scores` ← `LSL-M2-M3/results.csv` 的 `p_*` 欄位
- `poster` ← M5 的 PNG 壓縮後

## 頁面的四種狀態 / page states

| 狀態 | 時機 |
|---|---|
| 結果 | `results/<card_id>.json` 存在 |
| 還在生成中 | 檔案還沒出現 —— 每 15 秒自動重試（處理 Pages 建置延遲） |
| 沒帶卡號 | 網址沒有 `?c=` |
| 查無此卡 | 重試 20 次仍然沒有 |

頁面會先試 `raw.githubusercontent.com`（push 後幾乎立即可用），失敗再退回同目錄的相對路徑。

---

## 隱私 / privacy

卡號是連號的，網址可以被猜到 —— 任何人都能瀏覽所有參與者的結果。
這是展覽團隊評估後接受的取捨（資料不含個人身分資訊）。

Card ids are sequential and the URLs are guessable, so anyone can browse any
participant's result. Accepted by the exhibition team — the data contains no
personally identifying information.

---

詳細背景見主專案的 `HANDOFF_scanner_and_result_page.md`。
