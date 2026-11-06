# 彰銀入帳-外銷訂單對帳 · 看板（GitHub Pages 部署）

看板網址：https://cceccecasters.github.io/receivables-board-site/

這個 repo 只放**建置後的靜態檔**（`site/`），原始碼在私有 repo `cceccecasters/receivables-board`。

## 內容

| 路徑 | 說明 |
|---|---|
| `site/` | Vite production build（`VITE_BASE=/receivables-board-site/`） |
| `.github/workflows/pages.yml` | 推上 `main` 就部署到 GitHub Pages |

## 資料與安全性

- `site/assets/index-*.js` 內的看板資料是 AES-256-GCM 密文（PBKDF2-SHA256，31 萬次迭代），沒有通行碼無法解讀。
- 沒有上傳 Excel、`board.json`、通行碼或任何明文帳務資料。
- 前端會帶 Supabase anon key（設計上就是公開的，與原站相同）；實際讀寫仍受 RLS 與登入身份限制。

## 更新流程

```powershell
# 在私有原始碼 repo 內
$env:VITE_BASE="/receivables-board-site/"
npm run build -- --outDir dist-gh --emptyOutDir
# 把 dist-gh/ 內容複製到本 repo 的 site/，commit 後 push
```

推上去後 GitHub Actions 會自動部署，約 1 分鐘生效。
