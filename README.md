# 共用記事本設定步驟

## 1. 建立 Supabase 專案(免費)
到 https://supabase.com 註冊並建立專案。

## 2. 在 SQL Editor 貼上並執行
```sql
create table notes(
  id uuid primary key default gen_random_uuid(),
  title text, body text, drawing text,
  atts jsonb default '[]',
  created_at timestamptz default now()
);
alter table notes enable row level security;
create policy "public all" on notes for all using (true) with check (true);

insert into storage.buckets (id, name, public) values ('notes','notes',true);
create policy "public files" on storage.objects for all
  using (bucket_id='notes') with check (bucket_id='notes');
```

## 3. 填入設定
Project Settings → API,複製 Project URL 與 anon public key,貼到 index.html 最上方的 `CFG`。

## 4. 發佈到 GitHub Pages
1. GitHub 建立公開 repository,上傳 index.html(與本檔)。
2. Settings → Pages → Branch 選 main、資料夾 `/ (root)` → Save。
3. 約一分鐘後網址為 `https://你的帳號.github.io/repository名稱/`。

## 注意
任何知道網址的人都能新增、編輯、刪除記事與檔案,請勿放機密資料。
