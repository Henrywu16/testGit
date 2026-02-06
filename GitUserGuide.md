# Git + GitHub 完整操作手冊

（從零建立專案 → 使用 Token → Push / Pull → 分支 → 版本回復 → 衝突處理 → 公司 SOP）

---

# 目錄

1. 基本觀念
2. 安裝與準備
3. GitHub Token（PAT）建立與使用
4. 從零建立專案（GUI 與 CLI）
5. 日常工作流程（Push / Pull）
6. 分支管理（Branch）
7. Pull Request（PR）流程
8. 版本回復（Revert / Reset）
9. 衝突處理
10. .gitignore 建議
11. 公司標準作業 SOP
12. 常用指令速查表

---

# 一、基本觀念

## 1. Git 三個區域

1. Working Directory（工作區）  
   → 你正在編輯的檔案

2. Staging Area（暫存區）  
   → 準備要提交的變更

3. Repository（版本庫）  
   → 已 commit 的歷史版本

---

## 2. 四個核心動作

- git add → 加入暫存區
- git commit → 建立版本
- git push → 推送到 GitHub
- git pull → 拉取遠端更新

---

# 二、安裝與準備

## 必要工具

- Git
- GitHub 帳號

## 建議工具

- GitHub Desktop（圖形化操作）
- VS Code

---

# 三、GitHub Token（PAT）建立與使用

## 為什麼需要 Token？

GitHub 已停止使用帳號密碼推送  
改為使用：

- Personal Access Token (PAT)
- SSH Key
- GitHub Desktop OAuth

---

## 產生 Token 流程

1. 登入 GitHub
2. 右上角頭像 → Settings
3. Developer settings
4. Personal access tokens
5. Generate new token
6. 設定到期日與權限（repo 權限即可）
7. Generate
8. 複製 Token（只顯示一次）

---

## 使用方式

當 git push 要求登入時：

Username：你的 GitHub 帳號  
Password：貼上 Token（不是 GitHub 密碼）

---

# 四、從零建立專案

---

## A. GUI 方式（GitHub Desktop）

## 1. 建立資料夾與檔案

建立資料夾：
MyProject

建立 README.md：

```md
# MyProject
```

---

## 2. GitHub Desktop 初始化

File → New Repository  
Name：MyProject  
Create Repository

---

## 3. 第一次 Commit

Changes → 填 Summary  
Commit to main

---

## 4. 發佈到 GitHub

Publish repository  
選 Private / Public  
完成

---

---

## B. CLI 命令列方式

## 1. 建立專案

```bash
mkdir MyProject
cd MyProject
echo "# MyProject" > README.md
```

## 2. 初始化 Git

```bash
git init
git add .
git commit -m "Initial commit"
```

## 3. 在 GitHub 建立 repo

到 GitHub 網站 → New repository → 建立 MyProject

## 4. 連接遠端並推送

```bash
git branch -M main
git remote add origin https://github.com/你的帳號/MyProject.git
git push -u origin main
```

登入時貼上 Token

---

# 五、日常工作流程

## 修改後提交

```bash
git add .
git commit -m "描述這次修改"
git push
```

---

## 拉取遠端更新

```bash
git pull
```

建議每天開始工作前先 pull

---

# 六、分支管理（Branch）

## 何時使用分支？

- 新功能開發
- 修 Bug
- 測試實驗功能

---

## 建立分支

```bash
git checkout -b feature/login
```

推送分支：

```bash
git push -u origin feature/login
```

---

## 合併流程

1. push 分支
2. 到 GitHub 建立 Pull Request
3. Review
4. Merge
5. main 更新
6. 本機 git pull

---

# 七、Pull Request（PR）標準流程

```
main
  |
  └── feature/xxx
          |
          └── push
                  |
                  └── Pull Request
                          |
                          └── Review
                                  |
                                  └── Merge
                                          |
                                          └── main 更新
```

---

# 八、版本回復

---

1. 安全方式（推薦）

---

```bash
git log --oneline
git revert <commit_id>
git push
```

會建立一個「反向 commit」，保留歷史紀錄。

---

---

2. Reset（危險）

---

```bash
git reset --mixed HEAD~1
```

模式說明：

- --soft → 保留暫存區
- --mixed → 保留工作區（預設）
- --hard → 直接刪除變更（危險）

⚠ 已 push 的版本不建議 reset 再強推

---

---

3. 查看舊版本（不改歷史）

---

```bash
git checkout <commit_id>
git checkout main
```

---

# 九、衝突處理

當 git pull 發生衝突：

1. 打開衝突檔案
2. 找到 <<<<<<< ======= >>>>>>>
3. 選擇保留內容
4. 存檔

```bash
git add .
git commit -m "Resolve conflict"
git push
```

---

# 十、.gitignore 範例

建立 .gitignore：

```
.env
.vscode/
.vs/
bin/
obj/
node_modules/
*.log
```

---

# 十一、公司標準 SOP（建議流程）

## 每天開始工作

```bash
git checkout main
git pull
git checkout -b feature/功能名稱
```

---

## 每完成一段功能

```bash
git add .
git commit -m "清楚描述修改內容"
git push
```

---

## 結束前

- 確認已 push
- 不要只存在本機

---

# 十二、常用指令速查表

## 狀態

```bash
git status
```

## 查看歷史

```bash
git log --oneline
```

## 分支

```bash
git branch
git checkout main
git checkout -b feature/xxx
```

## 推送

```bash
git push
```

## 拉取

```bash
git pull
```

## 回復

```bash
git revert <commit_id>
git reset --mixed HEAD~1
```

---

# 十三、安全提醒

- Token 不可上傳 GitHub
- .env 一律加入 gitignore
- 公開 repo 禁止放公司機密
- 建議所有功能透過 PR 合併

---

# 完成

你已掌握：

- 專案建立
- Token 使用
- Push / Pull
- 分支管理
- Pull Request
- 版本回復
- 衝突處理
- 公司 Git 作業標準
