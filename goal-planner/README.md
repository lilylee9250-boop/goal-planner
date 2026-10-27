# 理財目標規劃器

以 PV（現值）、FV（終值）、PMT（每期投入）為核心的理財目標試算網站。純靜態單頁（HTML + CSS + JavaScript），無需建置、無外部相依。

## 功能
- 設定目標金額、年限、通膨率，自動換算名目目標
- 依目前資金、每月投入、預期報酬預估 FV 與達成率
- 缺口建議：所需 PMT、所需年限（NPER）、所需報酬率（RATE）、所需一次投入（PV）
- 報酬率情境壓力測試與里程碑表
- 自動支援淺色／深色模式；輸入值會存在瀏覽器 localStorage

## 專案結構
```
goal-planner/
├── public/
│   ├── index.html      # 整個網站
│   └── _headers        # Cloudflare 安全標頭
├── .github/workflows/deploy.yml   # 選用：GitHub Actions 自動部署
├── wrangler.toml
├── .gitignore
├── LICENSE
└── README.md
```

## 本機預覽
直接用瀏覽器開啟 `public/index.html`，或：
```
npx wrangler pages dev public
```

## 上傳到 GitHub
```
cd goal-planner
git init
git add .
git commit -m "Initial commit"
git branch -M main
git remote add origin https://github.com/<你的帳號>/goal-planner.git
git push -u origin main
```
（先在 GitHub 建立一個空的 repository，不要勾選 README。）

## 部署到 Cloudflare Pages

### 方法 A：連接 GitHub（推薦）
1. Cloudflare Dashboard → Workers & Pages → Create → Pages → Connect to Git
2. 選擇此 repository
3. Build command 留空；Build output directory 填 `public`
4. Save and Deploy，之後每次 push 都會自動部署

### 方法 B：GitHub Actions
保留 `.github/workflows/deploy.yml`，並在 repo 的 Secrets 設定 `CLOUDFLARE_API_TOKEN` 與 `CLOUDFLARE_ACCOUNT_ID`。第一次需先在 Cloudflare 建立名為 `goal-planner` 的 Pages 專案（或改 workflow 內的專案名稱）。

### 方法 C：指令直接部署
```
npx wrangler pages deploy public --project-name=goal-planner
```

## 免責聲明
本工具僅供試算與教育用途，報酬率為假設值，不代表實際投資結果，也不構成投資建議。
