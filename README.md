[![Deploy Hugo site to Pages](https://github.com/imagician-tw/imagician-tw.github.io/actions/workflows/hugo.yaml/badge.svg?branch=main)](https://github.com/imagician-tw/imagician-tw.github.io/actions/workflows/hugo.yaml)

# imagician 創想符碼

[imagician.tw](https://imagician.tw/) 的原始碼：創想符碼 imagician 官方網站與部落格，並收錄 imagician Taiwan 社群頁面。

使用 [Hugo](https://gohugo.io/)（≥ 0.146）與 [PaperMod](https://github.com/adityatelange/hugo-PaperMod) theme（git submodule，位於 `themes/PaperMod`）。

## 結構

- `content/_index.md`：首頁文案（標語、導覽項目）。
- `content/posts/`：文章。
- `content/community/`：imagician Taiwan 社群頁面；舊網址 `/about/`、`/meetup/`、`/resources/` 以 `aliases` 轉到這裡。
- `layouts/home.html`：首頁版型（含圓線動畫）。
- `assets/css/extended/imagician.css`：配色、襯線標題與首頁樣式；列表在 hover／鍵盤聚焦時維持位置不動，保留連結變色。
- `static/images/og-image.png`：Facebook／X 分享卡片共用縮圖（1200×630）。

## 分享卡片

每頁的 `og:title` 為頁面標題，`og:description` 依序取 front matter 的 `description`，沒有時取內文前幾句。縮圖固定為 `og-image.png`；個別文章可在 front matter 設定 `cover.image` 覆蓋。

## 社群連結與分享

- `hugo.toml` 的 `params.communityLinks` 控制全站頁尾連結；Facebook、Luma 已設定，X 暫留空。`url` 留空時不顯示，補上網址後即會出現，不需要修改版型。
- 文章頁使用 Facebook／X 的文字分享連結；社群、學習資源等一般頁面不顯示分享列。Luma 是活動頁連結，不作為文章分享按鈕。
- 學習資源維護於 `content/community/resources.md`。現有兩篇 2025 鐵人賽文章已移除，未設定轉址；舊文章網址會回傳 404，原始內容仍可從 Git 歷史取回。

## 如何貢獻

### 前置需求

```shell
brew install hugo
git clone --recurse-submodules git@github.com:imagician-tw/imagician-tw.github.io.git
# 已 clone 過：git submodule update --init
```

### 步驟

1. Fork 並 clone 專案。
2. 新增文章：
   ```shell
   hugo new posts/YOUR_ARTICLE_TITLE.md
   ```
3. 啟動預覽伺服器，於 <http://localhost:1313/> 檢視：
   ```shell
   make server
   ```
4. 確認可建置：
   ```shell
   make build
   ```
5. 發 pull request 到 [imagician-tw/imagician-tw.github.io](https://github.com/imagician-tw/imagician-tw.github.io)。推上 `main` 後由 GitHub Actions 部署到 GitHub Pages。

### 更新 PaperMod

```shell
git submodule update --remote themes/PaperMod
```

更新後先本機建置確認，再提交 submodule 的新 commit。
