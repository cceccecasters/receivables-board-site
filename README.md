# 彰銀入帳-外銷訂單對帳 · 看板（GitHub Pages）

看板網址：https://cceccecasters.github.io/receivables-board-site/

這個 repo 只放**建置後的靜態檔**（repo 根目錄即網站根目錄），原始碼在私有 repo `cceccecasters/receivables-board`。

## 部署方式

GitHub Pages → Deploy from a branch → `main` / `(root)`。推上 `main` 約 1 分鐘後自動更新。
`.nojekyll` 已放在根目錄，避免 Jekyll 處理 `assets/` 內的檔案。

## 資料與安全性

- `assets/index-*.js` 內的看板資料是 AES-256-GCM 密文（PBKDF2-SHA256，31 萬次迭代），沒有通行碼無法解讀。
- 沒有上傳 Excel、`board.json`、通行碼或任何明文帳務資料。
- 前端會帶 Supabase anon key（設計上即公開，與原站相同）；實際讀寫仍受 RLS 與登入身份限制。

## 更新流程

在私有原始碼 repo 內：

```powershell
$env:VITE_BASE="/receivables-board-site/"
npm run build -- --outDir dist-gh --emptyOutDir
```

把 `dist-gh/` 內容覆蓋到本 repo 根目錄（保留 `.nojekyll`、`404.html`、`README.md`），commit 後 push。
