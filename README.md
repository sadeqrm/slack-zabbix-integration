# 🚀 Slack App for Zabbix Alerts

این راهنما مراحل کامل ساخت یک **Slack App** برای ارسال اعلان‌های Zabbix به کانال یا DM در Slack را توضیح می‌دهد.

---

## 1️⃣ ساخت اپ در Slack
1. به 🌐 [Slack API Apps](https://api.slack.com/apps) بروید.
2. روی **➕ Create New App** کلیک کنید.
3. دو گزینه نمایش داده می‌شود:
   - **📄 From scratch**: ساخت دستی اپ (مناسب شروع ساده یا تنظیمات سفارشی).
   - **⚡ From a manifest**: ساخت اپ از روی فایل YAML/JSON شامل همه تنظیمات (سریع، قابل نسخه‌بندی).
4. گزینه **📄 From scratch** را انتخاب کنید.
5. یک **✏️ App Name** دلخواه (مثلاً `ZabbixAlert`) وارد کنید.
6. Workspace مقصد را انتخاب کنید و اپ را بسازید.

---

## 2️⃣ تنظیم ⚙️ OAuth & Permissions

از منوی اپ وارد **OAuth & Permissions** شوید و اسکوپ‌های زیر را به Bot اضافه کنید:

- 🔑 `chat:write` → اجازه ارسال پیام در کانال‌ها و مکالمات.
- 🔒 `groups:write` → مدیریت Private Channels که بات در آن‌ها حضور دارد و امکان ساخت آن‌ها.
- 💬 `im:write` → شروع Direct Message با افراد.

---

## 3️⃣ نصب اپ روی Workspace
1. از بخش **OAuth & Permissions** یا **Install App**، روی **⬇️ Install to Workspace** کلیک کنید.
2. دسترسی‌ها را بررسی و **✅ Allow** را بزنید.
3. پس از نصب، **🔐 Bot User OAuth Token** با فرمت `xoxb-...` نمایش داده می‌شود. این توکن را برای اتصال در Zabbix نیاز دارید.

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
