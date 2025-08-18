# 🚀 Slack App for Zabbix Alerts

این راهنما مراحل کامل ساخت یک **Slack App** برای ارسال اعلان‌های Zabbix به کانال یا DM در Slack را توضیح می‌دهد.

---

## 1️⃣ ساخت اپ در Slack
1. به 🌐 [Slack API Apps](https://api.slack.com/apps) بروید.  
   <p align="center">
     <img src="https://github.com/user-attachments/assets/d1e2c555-d3ce-41ca-bffd-d4a02117038f" alt="step1" width="600" />
   </p>

2. روی **➕ Create New App** کلیک کنید.  
   <p align="center">
     <img src="https://github.com/user-attachments/assets/48a90475-fa7c-4ebf-84c6-bd18d099fb89" alt="step2" width="700" />
   </p>

3. دو گزینه نمایش داده می‌شود:
   - **📄 From scratch**: ساخت دستی اپ (مناسب شروع ساده یا تنظیمات سفارشی).
   - **⚡ From a manifest**: ساخت اپ از روی فایل YAML/JSON شامل همه تنظیمات (سریع، قابل نسخه‌بندی).

   <p align="center">
     <img src="https://github.com/user-attachments/assets/4bd2c725-2108-43e0-899d-cd266f04b632" alt="step3" width="600" />
   </p>

4. گزینه **📄 From scratch** را انتخاب کنید.  
5. یک **✏️ App Name** دلخواه (مثلاً `ZabbixAlert`) وارد کنید و Workspace مقصد را انتخاب کنید.  

   <p align="center">
     <img src="https://github.com/user-attachments/assets/129c1b11-2463-43ec-8ff9-8a7cfeab9421" alt="step4" width="400" />
   </p>

---

## 2️⃣ تنظیم ⚙️ OAuth & Permissions
از منوی اپ وارد **OAuth & Permissions** شوید و اسکوپ‌های زیر را به Bot اضافه کنید:

<p align="center">
  <img src="https://github.com/user-attachments/assets/59cb24ab-a359-4a74-bd00-2eb5a8693919" alt="oauth" width="600" />
</p>

- 🔑 `chat:write` → اجازه ارسال پیام در کانال‌ها و مکالمات.  
- 🔒 `groups:write` → مدیریت Private Channels که بات در آن‌ها حضور دارد و امکان ساخت آن‌ها.  
- 💬 `im:write` → شروع Direct Message با افراد.  

---

## 3️⃣ نصب اپ روی Workspace
1. از بخش **OAuth & Permissions** یا **Install App**، روی **⬇️ Install to Workspace** کلیک کنید.  
   <p align="center">
     <img src="https://github.com/user-attachments/assets/7957e02b-4e9a-485a-8a66-b709dd60b3ff" alt="install1" width="600" />
   </p>

2. دسترسی‌ها را بررسی و **✅ Allow** را بزنید.  
   <p align="center">
     <img src="https://github.com/user-attachments/assets/c51c822e-cd99-433a-bca8-cc6bf4bbb9b1" alt="install2" width="500" />
   </p>

3. پس از نصب، **🔐 Bot User OAuth Token** با فرمت `xoxb-...` نمایش داده می‌شود. این توکن را برای اتصال در Zabbix نیاز دارید.  

<p align="center">
  <img src="https://github.com/user-attachments/assets/38b67cb4-da8b-42ee-8998-7c0d6becefe0" alt="token" width="600" />
</p>

> ⚠️ **نکته:** اگر نصب اپ محدود به ادمین است، باید تایید ادمین گرفته شود.

---

## 4️⃣ ساخت کانال و اضافه‌کردن اپ
1. در Slack یک کانال جدید برای اعلان‌ها بسازید (📢 Public یا 🔒 Private).
2. اپ را به کانال Invite کنید:
   - از **Channel Details → Integrations → Add an app** استفاده کنید.
   - یا در کادر پیام بنویسید ⌨️ `@ZabbixAlert` و گزینه *Invite to channel* را بزنید.

---

## 5️⃣ اتصال Zabbix به Slack
1. در تنظیمات Zabbix → Media، **🔐 Bot User OAuth Token** (`xoxb-...`) را قرار دهید.  
2. **Channel ID** مقصد را مشخص کنید:
   - 📌 استفاده از **Channel ID** (به‌جای نام کانال) توصیه می‌شود تا در صورت تغییر نام کانال، اتصال از کار نیفتد.
   - برای گرفتن Channel ID می‌توانید از Slack API (`conversations.list`) یا از جزئیات کانال استفاده کنید.

---

## ✅ چک‌لیست سریع
- [x] ✨ ساخت اپ در https://api.slack.com/apps → **From scratch**
- [x] 🔑 تنظیم اسکوپ‌های Bot (`chat:write`, `groups:write`, `im:write`)
- [x] 📥 نصب اپ و گرفتن **Bot User OAuth Token**
- [x] 🏷️ ساخت کانال و Invite کردن اپ
- [x] 🔗 قرار دادن Token و Channel ID در Zabbix

---

## 🛠️ مشکلات رایج
- ❌ پیام ارسال نمی‌شود → بررسی کنید بات حتماً به کانال **invite** شده باشد و اسکوپ `chat:write` دارد.
- ❌ ارسال به Private Channel → مطمئن شوید بات به کانال Private دعوت شده است و اسکوپ `groups:write` دارد.
- ❌ تغییر نام کانال → اگر به‌جای ID از نام استفاده کرده باشید، اتصال می‌شکند.
