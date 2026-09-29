# nutc-test-office — Nexus 2.0 測試處室公告站

Nexus 2.0 專題用的**測試公告站**。所有內容都是虛構測試資料，不是任何學校的正式公告。

網址：https://aznitro.github.io/nutc-test-office/
列表頁（資料流從這裡抓）：https://aznitro.github.io/nutc-test-office/p/403-1015-716-1.html

## 為什麼仿校網結構

讓 Power Automate 資料流用**同一套規則**抓教務處和測試站：

| 地方 | 校網 | 測試站 |
|---|---|---|
| 列表頁 | `/p/403-1015-716-1.php` | `/p/403-1015-716-1.html` |
| 公告頁網址 | `/p/406-1015-編號,r716.php` | `/p/406-1015-編號,r716.html` |
| 內文 | 「最後更新日期」之後、「瀏覽數」之前 | 同 |
| 附件 | `<ul class="mptattach">` 裡的 `<a href="...">` | 同（href 是站內路徑 `/nutc-test-office/var/file/...`） |

頁面上沒有任何學校的標誌或名稱，每頁頂端都有「測試站」標示。

## 怎麼新增／修改公告（開發者按鈕）

每頁上方有「開發者工具」列：

- **＋ 新增貼文**：開 GitHub 新增檔案頁，檔名（編號）和範本已帶好，改標題、內文後按 Commit。
- **⇪ 上傳附件**：把 PDF 上傳到 `var/file/test/attach/`，再到貼文的 `attachments` 填檔名。
- **✎ 編輯本篇**（公告頁才有）：改內容後 Commit，用來測試「內文變了 → 待更新」。

Commit 後約 1 分鐘網站更新（GitHub Actions 的 pages build）。

## 貼文格式（`_news/編號.md`）

```yaml
---
title: "【測試】標題"
date: 2026-09-01 09:30:00 +0800
updated: 2026-09-01        # 最後更新日期；改內容時一起改
views: 0
attachments:               # 沒附件就整段拿掉
  - name: 【測試】附件名稱.pdf
    file: 檔名.pdf         # 放在 var/file/test/attach/
---
內文（Markdown）
```

檔名就是公告編號（例如 `100006.md` → `/p/406-1015-100006,r716.html`）。

## 目前的測試公告

| 編號 | 標題 | 用途 |
|---|---|---|
| 100001 | 加退選時程公告（有 PDF） | 一般公告＋附件轉文字 |
| 100002 | 停修申請期限說明 | 純內文 |
| 100003 | 跨校選課申請注意事項（有 PDF） | 附件 |
| 100004 | 選課系統維護暫停服務通知 | 短公告 |
| 100005 | 加選截止提醒 | **故意寫錯日期（9/31）**，測「疑似錯誤」提醒 |

## 開啟 GitHub Pages（只要做一次）

Settings → Pages → Build and deployment → Source：Deploy from a branch → Branch：`main`、資料夾 `/ (root)` → Save。
