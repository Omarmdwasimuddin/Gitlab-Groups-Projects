## GitLab Group ও Project তৈরি → প্রথম Code Push (Local থেকে Remote)

এই ডকুমেন্টেশনে দেখানো হয়েছে কীভাবে GitLab-এ নতুন group ও project তৈরি করে, local মেশিন থেকে একটা কোড push করা যায়। ধাপে ধাপে সহজভাবে লেখা হয়েছে যাতে পরে দেখলে সহজেই মনে পড়ে যায়।

---

## ১️⃣ GitLab-এ Group ও Project তৈরি করা

**ফ্লো:**

```
Groups → New group → Create group
   → Group name: daw
   → Create group
      → Create project → Create blank project
         → Project name: daw
         → "Initialize repository with a README" এর পাশের চেকবক্স — আনচেকড রাখো
            → Create project
```

**গুরুত্বপূর্ণ নোট:** README initialize করার চেকবক্সটা আনচেকড রাখতে হবে। কারণ আমরা নিজেদের local repo থেকে push করব — GitLab যদি নিজেই README দিয়ে repo initialize করে ফেলে, তাহলে push করার সময় remote আর local history-তে conflict হতে পারে (unrelated histories error আসতে পারে)।

![GitLab project creation screenshot](https://imgur.com/hxWEOfV.png)

Group তৈরি করার পর, সেই group-এর ভেতরে project তৈরি করতে হয় — কারণ GitLab-এ group হচ্ছে একটা container, যার ভেতরে একাধিক project রাখা যায় (টিম বা organization-এর জন্য উপযোগী)।

---

## ২️⃣ Local মেশিনে ফোল্ডার সেটআপ (PowerShell)

PowerShell খুলে নিচের কমান্ডগুলো রান করো:

```bash
mkdir gitlab
cd gitlab
code .
```

**ব্যাখ্যা:**

| কমান্ড | কী করে |
|---|---|
| `mkdir gitlab` | `gitlab` নামে একটা নতুন ফোল্ডার তৈরি করে |
| `cd gitlab` | সেই ফোল্ডারের ভেতরে প্রবেশ করে (change directory) |
| `code .` | বর্তমান ফোল্ডারটা VS Code দিয়ে খুলে দেয় |

---

## ৩️⃣ VS Code-এ HTML ফাইল তৈরি করা

1. VS Code-এ `index.html` নামে একটা নতুন ফাইল তৈরি করো।
2. ফাইলের ভেতরে `!` টাইপ করে **Enter** চাপলে Emmet abbreviation থেকে পুরো HTML boilerplate structure অটো-জেনারেট হয়ে যাবে (`<!DOCTYPE html>`, `<head>`, `<body>` সহ)।

---

## ৪️⃣ Git Init ও Push করা (VS Code Terminal)

VS Code-এর টার্মিনাল খুলে নিচের কমান্ডগুলো একটার পর একটা রান করো:

```bash
git init
git add .
git commit -m 'initial'
git remote add origin git@gitlab.com:wasuit-group1/wasimu.it/code-push.git
git branch -M main
git push -u origin main
```

**লাইন বাই লাইন ব্যাখ্যা:**

| কমান্ড | কাজ |
|---|---|
| `git init` | বর্তমান ফোল্ডারকে একটা Git repository হিসেবে initialize করে (`.git` ফোল্ডার তৈরি হয়) |
| `git add .` | ফোল্ডারের সব change/file staging area-তে যোগ করে (commit করার জন্য প্রস্তুত করে) |
| `git commit -m 'initial'` | staged changes গুলো একটা commit হিসেবে save করে, `'initial'` হচ্ছে commit message |
| `git remote add origin <url>` | local repo-কে remote GitLab repo-র সাথে link/connect করে, `origin` নাম দিয়ে |
| `git branch -M main` | বর্তমান branch-এর নাম জোর করে `main`-এ rename করে |
| `git push -u origin main` | local `main` branch-এর commit গুলো remote (`origin`)-এ push করে, আর `-u` ফ্ল্যাগ দিয়ে upstream tracking সেট হয়ে যায় (পরের push গুলোতে শুধু `git push` লিখলেই হবে) |

---

## ৫️⃣ যাচাই করা

GitLab-এ গিয়ে ব্রাউজার reload দিলে দেখবে কোড সফলভাবে push হয়ে গেছে ✅

---

### 🔑 সংক্ষিপ্ত সারাংশ

1. GitLab-এ group → project বানাও (README uninitialized).
2. Local-এ ফোল্ডার বানাও, VS Code দিয়ে খোলো।
3. HTML ফাইল বানাও (Emmet দিয়ে)।
4. Git init → add → commit → remote add → branch rename → push।
5. GitLab-এ reload দিয়ে নিশ্চিত করো।
