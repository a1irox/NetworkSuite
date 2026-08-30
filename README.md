# Network Priority Manager

A small, lightweight Windows tool that lets you decide which network adapter (Wi‑Fi, Ethernet, USB modem, mobile hotspot, etc.) the operating system uses as the default internet route — through a simple drag-and-drop GUI, with no need to manually edit network settings in Control Panel or PowerShell.

## What problem does this solve?

When multiple network adapters are active at the same time (e.g. Wi‑Fi and Ethernet together, or a VPN), Windows decides which one takes priority based on a value called the **Interface Metric**. Windows calculates this value automatically, and it's often not what you actually want (for example, you want Ethernet to be the priority, but Windows keeps favoring Wi‑Fi). There's also no built-in GUI way to change this value manually — it normally requires PowerShell/netsh commands.

This app does that job with a few clicks and a drag-and-drop.

## Features

- **Live adapter list**: every physical network adapter is shown with its current status (connected / disconnected / disabled) and its current Metric. Status refreshes automatically every few seconds.
- **Drag and drop reordering**: drag rows to reorder them; the higher a row sits, the higher its priority.
- **One-click Apply**: clicking Apply sets Interface Metric values in stepped order (10, 20, 30, …) based on the order you arranged, and also disables Windows' Automatic Metric — otherwise Windows recalculates and silently overwrites the metric after a while, undoing the priority you just set.
- **Restore previous settings**: before any change, the original values are backed up automatically; you can revert everything back to how it was before you ever used the app, with one click.
- **New adapter notifications**: when a new network adapter is connected (e.g. a USB dongle), the app notifies you so you can place it in the priority order if you want.
- **Minimize to tray**: the app can keep running in the background from the System Tray without taking up taskbar space.
- **Bilingual (English / Persian)**: the whole UI switches between English and Persian with one button, including full right-to-left (RTL) support for Persian.
- **Built-in Help and About**: a Help section and an About dialog are included in the app itself.

## How it works (technical)

- The app is written in **PowerShell + WPF**; the GUI is defined in XAML and loaded directly inside the script itself (no separate file).
- Reading and changing adapter state is done through native Windows cmdlets like `Get-NetAdapter` and `Set-NetIPInterface` — no drivers or third-party tools are installed.
- Since changing the Interface Metric requires administrator rights, the app self-elevates via a UAC prompt as soon as it starts.
- Settings (adapter order and the backup of original values) are stored as JSON files under `%APPDATA%\NetworkSuite\`, not in the registry.
- To run without a console window, a separate exe launcher (`NetworkSuite.exe`) starts PowerShell in the background, hidden.

## Installation & Usage

1. Put all release files (`NetworkSuite.exe`, `NetworkSuite.ps1`, `icon.ico`) in the same folder — these three files must always stay together.
2. Double-click `NetworkSuite.exe`.
3. Accept the UAC (administrator) prompt — without this permission the app can't change network priority.
4. If Windows Defender/SmartScreen shows an "unrecognized app" warning (since the file isn't code-signed), click **More info → Run anyway**.

If the app doesn't open or you run into an issue, run `NetworkSuite_Debug.bat`; it keeps a console window open so you can see the exact error text. A full error log is always saved here as well:
`%TEMP%\NetworkSuite_error.log`

## Requirements

- Windows 8 / Server 2012 or newer (due to the dependency on the `NetAdapter` module)
- Administrator access

## File structure

| File | Role |
|---|---|
| `NetworkSuite.exe` | Main launcher — run this |
| `NetworkSuite.ps1` | The app's full logic and GUI |
| `icon.ico` | App icon (window, taskbar, tray) |
| `NetworkSuite_Debug.bat` | Troubleshooting run with a visible console |

## Credits

Made by A1iRoX with the help of AI.

--------------------------------------------------------------------------------------------------------------------------------------------

# Network Priority Manager

ابزاری کوچک و سبک برای ویندوز که بهت اجازه می‌ده تعیین کنی سیستم‌عامل کدوم کارت شبکه (Wi‑Fi، اترنت، مودم USB، هات‌اسپات موبایل و ...) رو به‌عنوان مسیر پیش‌فرض اینترنت انتخاب کنه — با یه رابط گرافیکی ساده و درگ-اند-دراپ، بدون نیاز به دستکاری دستی تنظیمات شبکه در Control Panel یا PowerShell.

## این برنامه چه مشکلی رو حل می‌کنه؟

وقتی چند کارت شبکه هم‌زمان فعال باشن (مثلاً Wi‑Fi و اترنت با هم، یا یه VPN)، ویندوز خودش بر اساس یه مقدار به اسم **Interface Metric** تصمیم می‌گیره کدوم رو در اولویت بذاره. این مقدار رو خود ویندوز به‌صورت خودکار حساب می‌کنه و اغلب دقیقاً همون چیزی نیست که کاربر می‌خواد (مثلاً می‌خوای اترنت اولویت اول باشه ولی ویندوز Wi‑Fi رو ترجیح می‌ده). تغییر دستی این مقدار هم از طریق رابط گرافیکی ویندوز عملاً امکان‌پذیر نیست و باید با دستورات PowerShell/netsh انجام بشه.

این برنامه این کار رو با چند تا کلیک و درگ-اند-دراپ انجام می‌ده.

## امکانات

- **نمایش زنده‌ی کارت‌های شبکه**: هر کارت شبکه‌ی فیزیکی با وضعیت فعلیش (متصل / قطع / غیرفعال) و مقدار Metric فعلی‌اش نشون داده می‌شه. وضعیت هر چند ثانیه یک‌بار خودکار به‌روزرسانی می‌شه.
- **درگ اند دراپ برای اولویت‌بندی**: ردیف‌ها رو بکش و جابه‌جا کن؛ هر چی بالاتر باشه اولویت بیشتری داره.
- **Apply یک‌کلیکی**: با زدن دکمه‌ی اعمال، مقادیر Metric بر اساس ترتیبی که چیدی به‌صورت پلکانی (۱۰، ۲۰، ۳۰، ...) تنظیم می‌شن و علاوه بر این، قابلیت محاسبه‌ی خودکار Metric توسط ویندوز (Automatic Metric) غیرفعال می‌شه — چون در غیر این صورت ویندوز بعد از مدتی دوباره مقدار رو خودش بازمحاسبه و بازنویسی می‌کنه و اولویتی که تعیین کردی از بین می‌ره.
- **بازگردانی تنظیمات قبلی**: قبل از هر تغییر، مقادیر اصلی به‌صورت خودکار بکاپ گرفته می‌شن؛ هر وقت خواستی می‌تونی با یک کلیک همه چیز رو به حالت اولیه (قبل از استفاده از برنامه) برگردونی.
- **اعلان کارت شبکه‌ی جدید**: وقتی یه کارت شبکه‌ی جدید وصل بشه (مثلاً یه دانگل USB)، برنامه بهت اطلاع می‌ده تا اگه خواستی جایگاهش رو در اولویت‌بندی تنظیم کنی.
- **کوچک کردن به تری**: برنامه می‌تونه در پس‌زمینه و در System Tray به کارش ادامه بده، بدون اینکه در نوار وظیفه اشغال فضا کنه.
- **دوزبانه (فارسی / انگلیسی)**: کل رابط کاربری با یه دکمه بین فارسی و انگلیسی سوییچ می‌شه، همراه با پشتیبانی کامل از راست‌به‌چپ (RTL) برای فارسی.
- **راهنما و درباره‌ی برنامه**: داخل خود برنامه یه بخش Help و About هست.

## نحوه‌ی کارکرد (فنی)

- برنامه با **PowerShell + WPF** نوشته شده؛ رابط گرافیکی با XAML تعریف شده و مستقیم داخل خود اسکریپت لود می‌شه (بدون فایل جدا).
- برای خوندن و تغییر وضعیت کارت‌های شبکه از cmdletهای بومی ویندوز مثل `Get-NetAdapter` و `Set-NetIPInterface` استفاده می‌شه؛ یعنی هیچ درایور یا ابزار جانبی نصب نمی‌شه.
- چون تغییر Interface Metric نیاز به دسترسی مدیر داره، برنامه به‌محض اجرا خودش با UAC درخواست دسترسی Administrator می‌کنه (self-elevation).
- تنظیمات (ترتیب کارت‌ها و بکاپ مقادیر اصلی) به‌صورت فایل JSON در `%APPDATA%\NetworkSuite\` ذخیره می‌شن، نه در رجیستری.
- برای اجرای بدون پنجره‌ی کنسول، یه لانچر exe جدا (`NetworkSuite.exe`) پاورشل رو در پس‌زمینه و به‌صورت مخفی صدا می‌زنه.

## نصب و اجرا

1. تمام فایل‌های ریلیز (`NetworkSuite.exe`, `NetworkSuite.ps1`, `icon.ico`) رو در یه پوشه‌ی مشترک قرار بده — این سه فایل باید همیشه کنار هم باشن.
2. روی `NetworkSuite.exe` دابل‌کلیک کن.
3. درخواست UAC (دسترسی مدیر) رو تأیید کن — بدون این دسترسی امکان تغییر اولویت شبکه وجود نداره.
4. اگه ویندوز/دیفندر هشدار "ناشناس" یا SmartScreen نشون داد (چون فایل امضای دیجیتال نداره)، روی **More info → Run anyway** بزن.

اگه برنامه باز نشد یا با مشکلی مواجه شدی، فایل `NetworkSuite_Debug.bat` رو اجرا کن؛ این فایل پنجره‌ی کنسول رو باز نگه می‌داره تا متن دقیق خطا رو ببینی. لاگ کامل خطاها هم همیشه در این مسیر ذخیره می‌شه:
`%TEMP%\NetworkSuite_error.log`

## نیازمندی‌ها

- ویندوز ۸ / Server 2012 یا جدیدتر (به‌خاطر وابستگی به ماژول `NetAdapter`)
- دسترسی Administrator

## ساختار فایل‌ها

| فایل | نقش |
|---|---|
| `NetworkSuite.exe` | لانچر اصلی — همینو اجرا کن |
| `NetworkSuite.ps1` | کل منطق و رابط گرافیکی برنامه |
| `icon.ico` | آیکون برنامه (پنجره، تسک‌بار، تری) |
| `NetworkSuite_Debug.bat` | اجرای عیب‌یابی با پنجره‌ی کنسول باز |

## سازنده

ساخته‌شده توسط A1iRoX با کمک هوش مصنوعی.
