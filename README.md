# 案頭 ψ-NET — 臨床心理學筆記網絡

這是用 [Quartz](https://quartz.jzhao.xyz/)（v5）建的個人知識庫，筆記是純 Markdown 檔案，
彼此用 `[[雙向連結]]` 串起來，網站會自動長出反向連結（backlinks）跟知識圖譜（graph view）。

## 本機預覽（不用部署也能看）

```bash
npm install
npx quartz plugin install   # 第一次跑，或外掛有更新時要重跑
npx quartz build --serve
```

跑完會給你一個 `http://localhost:8080` 之類的網址，瀏覽器打開就能看，存檔後重新整理就會看到改動。

## 怎麼新增/編輯筆記

直接在 `content/` 資料夾底下新增或編輯 `.md` 檔案就好：

```markdown
---
title: 筆記標題
description: 一句話描述（會出現在搜尋結果跟分享預覽）
tags: [研究所考科]
---

正文內容...

想連到別篇筆記，直接寫 [[筆記檔名]] 或 [[資料夾/筆記檔名|顯示文字]]，
存檔重 build 就會自動出現在對方的「反向連結」跟右側圖譜裡，不用兩邊各寫一次。
```

現有結構：

```
content/
  index.md              ← 首頁
  研究所考科/
  國考科目/
  其他心理學/
  社群/                  ← 對外連結（Threads、部落格），雙向連結用的入口
```

## 部署到 GitHub Pages（免費，不用網域）

1. 在 GitHub 開一個新的 repository（public 或 private 都可以，private 要付費方案才能開 Pages）
2. 把這個資料夾整個 push 上去：
   ```bash
   git init
   git add .
   git commit -m "init quartz site"
   git branch -M main
   git remote add origin https://github.com/你的帳號/你的repo.git
   git push -u origin main
   ```
3. 改 `quartz.config.yaml` 裡的 `baseUrl`，改成 `你的帳號.github.io/你的repo名稱`
4. GitHub repo 頁面 → Settings → Pages → Source 選「GitHub Actions」
5. push 之後 GitHub Actions 會自動跑 `.github/workflows/deploy.yml`，跑完網站就活了，網址是
   `https://你的帳號.github.io/你的repo名稱/`

之後每次 push 到 `main` 都會自動重新部署，不用手動做任何事。

## 開留言區（選用）

`quartz.config.yaml` 裡有個 `comments` 外掛，預設關閉。要開的話：
1. 去 [giscus.app](https://giscus.app) 用你的（public）repo 設定一次，會給你一組參數
2. 把 `comments` 那段的 `enabled` 改成 `true`，`options` 填進 giscus 給你的參數

## 換顏色 / 字體

都在 `quartz.config.yaml` 的 `theme` 區塊，`colors.darkMode` 是目前的深色賽博配色，
`colors.lightMode` 是切換成淺色時用的對照配色。
