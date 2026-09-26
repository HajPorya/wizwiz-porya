# تغییرات سازگاری با پنل سنایی 3x-ui v3.x (v3.1.0+)

## تغییرات API

### مسیرهای Inbound
- `/panel/inbound/list` → `/panel/api/inbounds/list`
- `/panel/inbound/add` → `/panel/api/inbounds/add`
- `/panel/inbound/update/:id` → `/panel/api/inbounds/update/:id`
- `/panel/inbound/del/:id` → `/panel/api/inbounds/del/:id`

### مسیرهای Client (تغییر اساسی)
- `/panel/api/inbounds/addClient` → `/panel/api/clients/add` (فرمت JSON جدید)
- `/panel/api/inbounds/updateClient/:uuid` → `/panel/api/clients/update/:email`
- `/panel/api/inbounds/:id/delClient/:uuid` → `/panel/api/clients/del/:email`
- `/panel/api/inbounds/:id/resetClientTraffic/:email` → `/panel/api/clients/resetTraffic/:email`
- `/panel/api/inbounds/clearClientIps/:email` → `/panel/api/clients/clearIps/:email`

### احراز هویت
- پشتیبانی از **Bearer Token** (روش توصیه‌شده v3.x)
- پشتیبانی از **CSRF Token** برای لاگین cookie-based
- فیلد `api_token` به تنظیمات سرور اضافه شد

### فرمت داده
- فیلد `settings` در API v3 به صورت آبجکت JSON برگردانده میشه (نه رشته)
- تابع `parseSettings()` برای سازگاری با هر دو فرمت اضافه شد
- فرمت `addClient` از `{id, settings}` به `{client, inboundIds}` تغییر کرد

## نحوه تنظیم

1. پنل سنایی رو به v3.x آپدیت کنید
2. در پنل: Settings → Authentication → API Token → یک توکن بسازید
3. در ربات: تنظیمات سرور → 🔑 توکن API → توکن رو وارد کنید
4. بدون توکن هم کار میکنه (با CSRF + Cookie) ولی Bearer Token مطمئن‌تره

## توابع جدید
- `panelAuth()` - احراز هویت با Bearer Token یا Cookie+CSRF
- `panelApiRequest()` - ارسال درخواست احراز هویت‌شده به پنل
- `parseSettings()` - پارس فیلد settings (سازگار با v2 و v3)
- `parseStreamSettings()` - پارس فیلد streamSettings
- `getInboundApiPath()` - مسیر API inbound بر اساس نوع سرور
- `getClientApiPath()` - مسیر API client بر اساس نوع سرور

## سازگاری
- سرور نوع "alireza" و "normal" بدون تغییر کار میکنن
- سرور نوع "marzban" بدون تغییر کار میکنه
- فقط سرور نوع "sanaei" مسیرهای جدید v3 رو استفاده میکنه
