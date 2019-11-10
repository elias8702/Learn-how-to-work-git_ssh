<div dir=rtl>

# متصل شدن به گیت‌هاب به وسیله SSH

برای اتصال به گیت هاب این امکان دارید که از `SSH` استفاده کنید

## درباره `SSH`

به وسیله پروتکل `SSH` می‌توانید از راه دور به سرور متصل و تایید هویت شود، نیاز به نام کاربری یا رمزعبور برای متصل شدن به گیت‌هاب ندارید.

وقتی که از `SSH` استفاده می‌کنید یک جفت کلید به وسیله برنامه ‍‍`ssh-agent ` ساخته می‌شود. همین کلید ها هم در اکانت گیت هاب استفاده می‌شود. با اضافه کردن این جفت کلیدها `SSH` تضمین می‌کند که از لایه امنیتی بیشتری برخوردار است. 

برای استفاده از `SSH`، که مخازن ما از روش `SAML single sign-on` استفاده می‌کند باید برای اولین بار تایید هویت شوید.

اگرطی یک سال از جفت کلید استفاده نکنید گیت هاب به صورت خودکار این اتصال را برای احتیاط امنیتی خذف می کند.


## چک کردن وجود کلیدها برای `SSH`

قبل از ساختن کلیدهای `SSH` باید چک کنیم کلید دیگری وجود نداشته باشد.


ترمینال را باز کنید 


دستور `ls -al ~/.ssh` برای دیدن کلیدهای موجود بزنید


به طور پیش فرض نام‌های کلید عمومی به صورت زیر است:
<div dir=ltr>

* id_dsa.pub
* id_ecdsa.pub
* id_ed25519.pub
* id_rsa.pub

<div dir=rtl>

اگر جفت کلید عمومی و خصوصی موجود نبود باید از کلید جدید ایجاد کنید

## ساخت کلیدهای `SSH`

ترمینال را باز کنید

دستور زیر را اجرا کنید

<div dir=ltr>

```
ssh-keygen -t rsa -b 4096 -C "ایمیل خود را وارد کنید"
```

<div dir=rtl>

این دستور با استفاده ایمیل یک جفت کلید جدید همانند برچسب پایین ایجاد می کند.



<div dir=ltr>

```
> Generating public/private rsa key pair.
```

<div dir=rtl>


هنگامی که همچین پیامی  "Enter a file in which to save the key" نمایش داده شد برروی کلید `Enter`کلید کنید


<div dir=ltr>

```
> Enter a file in which to save the key (/home/you/.ssh/id_rsa): [Press enter]
```

<div dir=rtl>

یک رمز عبور برای جفت کلیدها تایپ کنید


<div dir=ltr>

```
> Enter passphrase (empty for no passphrase): [Type a passphrase]> Enter same passphrase again: [Type passphrase again]

```

<div dir=rtl>

## اضافه کردن اس‌اس‌اچ به  ‍‍`ssh-agent ` 

برنامه  ‍‍`ssh-agent ` را در پشت صحنه اجرا کنید


<div dir=ltr>

```
$ eval "$(ssh-agent -s)"
> Agent pid 59566

```

<div dir=rtl>

کلید خصوصی خود را به اس‌اس‌اچ اضافه کنید. اگر کلید خود را با نامی دیگرایجاد کرداید یا کلید از قبل موجود دارید `id_rsa` را با نام دیگر جایگزین کنید




<div dir=ltr>

```
$ ssh-add ~/.ssh/id_rsa

```

<div dir=rtl>


# اضافه کردن جفت کلید به اکانت گیت هاب

جفت کلید خود را کپی کنید

اگر نام جفت کلید متفات است نام ان را تغییر بدهید تا با تنظیم فعلی مطابقت داشته باشد، خط جدید و فاصله در دستور اضافه نکنید.


<div dir=ltr>

```
$ sudo apt-get install xclip
# Downloads and installs xclip. If you don't have `apt-get`, you might need to use another installer (like `yum`)
# برنامه  xclip را دانلود و نصب می‌کند اگر از نصاب  `apt-get` استفاده نمی‌کنید با استفاده از `yum` اینکار را انجام دهید
$ xclip -sel clip < ~/.ssh/id_rsa.pub
# Copies the contents of the id_rsa.pub file to your clipboard
# محتوای فایل id_rsa.pub را در کلیدبوردتان کپی می کند
```

<div dir=rtl>

درگوشه سمت راست، بالا صفحه روی عکس اکانت خود کلید کنید و سپس رو تنظیمات کلید کنید



![pic1](https://help.github.com/assets/images/help/settings/userbar-account-settings.png "Settings")

در نوار کناری تنظیمات کاربری بر روی  `SSH` و   `GPG keys` کلید کنید


![pic1](https://help.github.com/assets/images/help/settings/settings-sidebar-ssh-keys.png "SSH and GPG keys")

برروی  `New SSH key`  و  `Add SSH key`  کلید کنید


![pic1](https://help.github.com/assets/images/help/settings/ssh-add-ssh-key.png "ssh-add-ssh-key.png")


درقسمت عنوان هر توصیفی برای کلید خود دارید بنویسید. و کلید را در فیلد `key`  برزید


![pic1](https://help.github.com/assets/images/help/settings/ssh-key-paste.png "Paste your key")


برروی `Add SSH key`  کلید کنید


![pic1](https://help.github.com/assets/images/help/settings/ssh-add-key.png "key")

در صورت درخواست رمز خود را تایید کنید

![pic1](https://help.github.com/assets/images/help/settings/sudo_mode_popup.png "GitHub password")

[ترجمه شده](https://help.github.com/en/github/authenticating-to-github/connecting-to-github-with-ssh)


