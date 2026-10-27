[![Deploy Hugo site to Pages](https://github.com/imagician-tw/imagician-tw.github.io/actions/workflows/hugo.yaml/badge.svg?branch=main)](https://github.com/imagician-tw/imagician-tw.github.io/actions/workflows/hugo.yaml)

# imagician 創想符碼

[imagician.tw](https://imagician.tw/) 的原始碼：創想符碼 imagician 官方網站與部落格，並收錄 imagician Taiwan 社群頁面。

使用 [Hugo](https://gohugo.io/)（≥ 0.146）與 [PaperMod](https://github.com/adityatelange/hugo-PaperMod) theme（git submodule，位於 `themes/PaperMod`）。

## 結構

- `content/_index.md`：首頁文案（標語、三項教學理念、社群與學習資源入口）。
- `content/posts/`：文章。
- `content/community/`：imagician Taiwan 社群頁面；舊網址 `/about/`、`/meetup/`、`/resources/` 以 `aliases` 轉到這裡。
- `layouts/home.html`：首頁版型（含圓線動畫）。
- `assets/css/extended/imagician.css`：配色、襯線標題與首頁樣式；列表在 hover／鍵盤聚焦時維持位置不動，保留連結變色。
- `static/images/og-image.png`：Facebook／X 分享卡片共用縮圖（1200×630）。

## 首頁教學理念

首頁主視覺在「懂得如何想像，就能學會施展魔法」下方呈現兩句理念引言，與標語相隔 1.25rem；引言字級為原設定減少 4px（桌機 18.8px、手機 11.2px）。三組圖示、短句與說明獨立呈現於主視覺下方，不另設「教學理念」標籤或三項中標。文字維護於 `content/_index.md` 的 `philosophy.intro` 與 `philosophy.items`；線條圖示由 `layouts/home.html` 繪製，僅作裝飾，不作為連結。

理念區最大寬度為 1120px，視窗寬度 ≥ 1100px 時呈現三欄，其餘為單欄；不改變一般文章的閱讀寬度。下方保留社群與學習資源入口，並明示實體小聚暫停中。這版尚未加入課程介紹或報名入口。

主視覺最低高度隨視窗調整於 340–500px，並依大圓底緣預留空間。大圓與藍色旋轉線共用 `--im-orbit-size: min(100vmin, 900px)`，藍線沿大圓邊界旋轉；大圓底緣與下方理念區塊的間距以 `clamp(16px, 2.5vw, 40px)` 隨視窗調整，桌機三欄版（≥ 1100px）再增加 5px，統一由 `--im-orbit-gap` 控制，不以裁切或淡出隱藏底緣。品牌區上方留白為 `calc(1.5rem + 20px)`，使品牌區及後續內容整體下移 20px，頂端導覽列不動；「程式與 AI 教育」與大標題間隔 2rem，兩句引言相隔 0.5rem。短句與說明使用內文字型。

## 字級

桌機版（視窗寬度 ≥ 601px）所有字級統一放大 50%（原始大小的 1.5 倍），手機版（≤ 600px）維持原大小。縮放設定集中在 `assets/css/extended/imagician.css` 的桌機字級區塊，由 `--im-font-scale: 1.5` 控制；僅調整字級，不縮放頁面或間距。首頁英文標題可超出內文欄寬並保持置中，避免放大後拆字換行。

PaperMod 的固定字級在此覆寫，不直接修改 theme submodule。新增 `px`、`rem` 或 `clamp()` 字級時，需同步加入桌機縮放規則；`em` 字級會隨父層放大，不需重複套用倍率。

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
