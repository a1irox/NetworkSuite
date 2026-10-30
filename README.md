English

A small, portable Windows tool that lets you decide which network adapter (Ethernet, Wi-Fi, USB modem, mobile hotspot, virtual adapter…) your PC uses as its main internet route. No PowerShell, no netsh, no digging through Control Panel.

Why?

When several adapters are active at once, Windows picks the winner using the Interface Metric (lower = higher priority). Windows calculates it automatically, and it often isn't what you want: you plug in Ethernet, yet traffic keeps going through Wi-Fi. There's no built-in screen to change it, and even if you set it by hand, Windows can quietly recalculate it later.

Network Priority Manager fixes both problems: you arrange the adapters visually, and the app also turns off Automatic Metric so your choice sticks.

Features
Live adapter list: every adapter with its connection status and current metric, refreshed automatically.
Drag and drop: the higher a row sits, the higher its priority.
One-click Apply: writes stepped metrics (10, 20, 30…) and disables Automatic Metric. No reboot, no dropped connection.
Priority lock: Windows no longer overrides your order behind your back.
Keep after restart: optionally re-applies your order at every boot.
One-click Restore: your original values are backed up before the first change and can be brought back any time.
New adapter alert: plug in a USB dongle and the app tells you so you can place it in the list.
System tray: keep it running quietly next to the clock.
English / Persian: full UI in both languages, with proper right-to-left layout.
Built-in Help and About.
Quick start
Download the latest zip from the Releases page and extract the whole folder.
Double-click NetworkSuite.exe and accept the UAC (administrator) prompt.
Drag the adapters into the order you want, then press Apply. Done.

Portable: Python is bundled inside the folder, so there is nothing to install. You can even run it from a USB drive.

SmartScreen warning? The app isn't code-signed. Click More info → Run anyway.

Using "Keep after restart"? Put the folder somewhere permanent first (not inside an archive or Temp). If you move it later, press Apply once more to re-register the new path.

Requirements
Windows 8 / Server 2012 or newer
Administrator rights (the app asks for them itself)
What's in the folder
Item	Purpose
NetworkSuite.exe	Launcher, run this
app\	The program itself
python\	Bundled Python runtime (don't delete)
NetworkSuite_Debug.bat	Runs the app with a visible console for troubleshooting
Troubleshooting
App doesn't open? Run NetworkSuite_Debug.bat and read the error text.
Full log: %TEMP%\NetworkSuite_error.log
An adapter wouldn't change? Some virtual or driver-locked adapters block metric changes.
Settings are stored as JSON files in %APPDATA%\NetworkSuite\, not in the registry. Uses only built-in Windows cmdlets (Get-NetAdapter, Set-NetIPInterface); no drivers are installed.
Links

Telegram channel · Report a bug · Support the project

Made by A1iRoX with the help of AI.

<a id="فارسی"></a>

<div dir="rtl" align="right">
فارسی

یه ابزار کوچیک و پرتابل برای ویندوز که بهت اجازه می‌ده تعیین کنی کامپیوترت اول از کدوم کارت شبکه (اترنت، وای‌فای، مودم USB، هات‌اسپات موبایل، آداپتور مجازی و...) برای اینترنت استفاده کنه. بدون PowerShell، بدون netsh و بدون گشتن تو Control Panel.

چرا لازمه؟

وقتی چند کارت شبکه هم‌زمان فعال باشن، ویندوز با یه عدد به اسم Interface Metric تصمیم می‌گیره کدوم اول باشه (عدد کمتر = اولویت بیشتر). این عدد خودکار حساب می‌شه و اغلب اون چیزی نیست که می‌خوای: کابل اترنت رو وصل می‌کنی ولی ترافیک هنوز از وای‌فای می‌ره. راه گرافیکی برای تغییرش وجود نداره، و حتی اگه دستی عوضش کنی، ویندوز بعداً بی‌صدا دوباره حسابش می‌کنه.

Network Priority Manager هر دو مشکل رو حل می‌کنه: ترتیب کارت‌ها رو تصویری می‌چینی، و برنامه Automatic Metric رو هم خاموش می‌کنه تا انتخابت ثابت بمونه.

امکانات
وضعیت زنده‌ی کارت‌ها: همه‌ی کارت‌ها با وضعیت اتصال و متریک فعلی، با به‌روزرسانی خودکار.
درگ و دراپ: هر ردیف بالاتر باشه، اولویتش بیشتره.
اعمال با یک کلیک: متریک‌ها به‌صورت پلکانی (۱۰، ۲۰، ۳۰...) نوشته می‌شن و Automatic Metric خاموش می‌شه. بدون ری‌استارت و بدون قطعی اینترنت.
قفل اولویت: ویندوز دیگه خودسرانه ترتیب رو عوض نمی‌کنه.
ماندگاری بعد از ری‌استارت: اگه بخوای، ترتیب هر بار موقع بوت دوباره اعمال می‌شه.
بازگردانی با یک کلیک: مقادیر اصلی قبل از اولین تغییر بکاپ گرفته می‌شن و هر وقت خواستی برمی‌گردن.
اعلان کارت جدید: دانگل USB وصل کنی، برنامه خبرت می‌کنه تا جایگاهش رو تعیین کنی.
سینی سیستم (Tray): بی‌سروصدا کنار ساعت اجرا می‌مونه.
فارسی / انگلیسی: کل رابط به هر دو زبان، با پشتیبانی کامل راست‌به‌چپ.
راهنما و درباره‌ی برنامه داخل خود برنامه.
شروع سریع

۱. آخرین نسخه‌ی زیپ رو از صفحه‌ی Releases دانلود کن و کل پوشه رو Extract کن. ۲. روی NetworkSuite.exe دابل‌کلیک کن و درخواست UAC (دسترسی مدیر) رو تأیید کن. ۳. کارت‌ها رو به ترتیب دلخواه بکش و دکمه‌ی اعمال رو بزن. تمام!

پرتابل: پایتون داخل همون پوشه هست و چیزی نیاز به نصب نداره. حتی از روی فلش هم اجرا می‌شه.

هشدار SmartScreen؟ برنامه امضای دیجیتال نداره. روی More info ← Run anyway بزن.

از «ماندگاری بعد از ری‌استارت» استفاده می‌کنی؟ اول پوشه رو یه جای ثابت بذار (نه داخل آرشیو یا Temp). اگه بعداً جابه‌جاش کردی، یه بار دیگه اعمال رو بزن تا مسیر جدید ثبت بشه.

نیازمندی‌ها
ویندوز ۸ / Server 2012 یا جدیدتر
دسترسی Administrator (برنامه خودش درخواستش می‌کنه)
داخل پوشه چیه؟
مورد	نقش
NetworkSuite.exe	لانچر؛ همینو اجرا کن
app\	خود برنامه
python\	پایتون همراه برنامه (پاک نکن)
NetworkSuite_Debug.bat	اجرای عیب‌یابی با پنجره‌ی کنسول باز
رفع اشکال
برنامه باز نمی‌شه؟ NetworkSuite_Debug.bat رو اجرا کن و متن خطا رو ببین.
لاگ کامل: %TEMP%\NetworkSuite_error.log
یه کارت تغییر نکرد؟ بعضی کارت‌های مجازی یا قفل‌شده توسط درایور اجازه‌ی تغییر متریک نمی‌دن.
تنظیمات به‌صورت فایل JSON در %APPDATA%\NetworkSuite\ ذخیره می‌شه، نه در رجیستری. فقط از cmdletهای خود ویندوز (Get-NetAdapter و Set-NetIPInterface) استفاده می‌شه و هیچ درایوری نصب نمی‌شه.
لینک‌ها

کانال تلگرام · گزارش باگ · حمایت مالی

ساخته‌شده توسط A1iRoX با کمک هوش مصنوعی.
