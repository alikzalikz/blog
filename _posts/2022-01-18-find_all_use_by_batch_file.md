---
title: "پیدا کردن تمام خطوط استفاده شده در فایل‌ها توسط Bath script"
date: 2022-01-15T09:00:00-00:00
categories:
  - Trick
tags:
  - bat
  - windows
  - batch
  - script
---

فرض کنید موارد استفاده از سرویس‌هایی که دارید را می‌خواهید در یک پروژه بزرگ پیدا کنید که این پروژه خود شامل زیرپروژه های مختلف است.  
جستجو عادی به ازای هر سرویس حتی با ابزارها بسیار زمانبر است.  
راه حل ساده تر که بسیار سریع نیز است، استفاده از `Batch Script` است که امکان جستجو در تمام فایل‌ها را می‌دهد.  

بدین منظور از کد زیر استفاده می‌کنیم که لیست سرویس‌ها مورد نظر را به عنوان ورودی می‌گیرد.  


```batch
@ECHO OFF

for /f "delims=" %%x in (%1) do (
	echo:
	echo SERVICE NAME:  %%x 
	echo:
	d:
	cd d:\Workspaces\folder\other
	findstr /S /M %%x *.cs 2>nul | findstr /V myFile.cs | findstr /V myFolder
)
c:
cd c:\Users\user\Desktop
```

در کد بالا:  
  - for : همان حلقه است که به ازای %1 که آدرس ورودی فایل مورد نظر است، انجام می‌شود
  - %%x : هر خط از فایل خوانده شده است
  - echo : برای چاپ در کنسول استفاده می‌شود
  - d: cd ... : برای رفتن به دایرکتوری دیگر استفاده می‌شود. حتما باید اول با d: به درایو مورد نظر رفت و سپس آدرس آن را با cd وارد کرد
  - findstr : برای پیدا کردن در متن فایل ها استفاده می‌شود که پارامترهای مختلف را دارد
  - *.cs : تمام فایل‌ها با فرمت cs
  - 2>nul : اگر به خطا خورد به پردازش بقیه ادامه می‌دهد
  - /V : فایل یا پوشه که در ادامه می‌آید را درنظر نمی‌گیرد و پردازش نمی‌کند

در انتها فایل را با فرمت `.bat` ذخیره کنید و آن را در cmd با آدرس فایل txt خود که مقادیر مورد نظر برای جستجو در آن نوشته شده است، اجرا کنید.  

نمونه فایل ورودی :  

```
test
ali
mohammad
```

با تشکر از دوست خوبم `مرتضی بهجت` برای تهیه کد بالا  

اطلاعات بیشتر:  
[microsoft](https://docs.microsoft.com/en-us/windows-server/administration/windows-commands/windows-commands)  