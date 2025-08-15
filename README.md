# 📥 Maktabkhooneh Downloader

## مقدمه

[Maktabkhooneh](https://maktabkhooneh.org) یکی از بزرگ‌ترین پلتفرم‌های MOOC فارسی است که دوره‌های خود را از بهترین دانشگاه‌های ایران، مانند [دانشگاه صنعتی شریف](http://sharif.edu) گردآوری می‌کند.

این پروژه به شما کمک می‌کند تا ویدیوهای دوره‌ها را به صورت **Batch** دانلود کنید.
برای دسترسی به لینک‌های ویدیو، نیاز به حساب کاربری مکتب‌خونه دارید.

---

## ✨ ویژگی‌ها

* **ورژن ۱** – نسخه اصلی بر پایه **Selenium + geckodriver** (پشتیبانی از نسخه‌های قدیمی‌تر سایت)
* **ورژن ۲** – نسخه بازنویسی شده با **Playwright** (سریع‌تر، پایدارتر، بدون نیاز به geckodriver)

---

## 📦 نصب وابستگی‌ها

### نسخه ۱ (قدیمی - Selenium)

```bash
pip install -r requirements.txt
```

همچنین نیاز دارید **geckodriver** نصب کنید تا Selenium بتواند مرورگر Firefox را کنترل کند.

---

### نسخه ۲ (جدید - Playwright)

```bash
pip install -r v2/requirements-v2.txt
playwright install
```

---

## ▶️ نحوه اجرا

### نسخه ۱ – Selenium

```bash
python maktabkhooneh-dl.py -u <USERNAME> -p <PASSWORD> <COURSE_SLUG>
```

مثال:

```bash
python maktabkhooneh-dl.py -u test@example.com -p 123456 آموزش-رایگان-تحلیل-هوشمند-تصاویر-زیست-پزشکی-mk1070
```

---

### نسخه ۲ – Playwright

```bash
python v2/maktabkhone-dl-v2.py -u <USERNAME> -p <PASSWORD> <COURSE_URL>
```

مثال:

```bash
python v2/maktabkhone-dl-v2.py -u test@example.com -p 123456 https://maktabkhooneh.org/course/آموزش-کالی-Linux-mk4021
```

---

## 🛠 گزینه‌ها

| گزینه کوتاه   | گزینه کامل            | توضیح                                                          |
| ------------- | --------------------- | -------------------------------------------------------------- |
| `-u USERNAME` | `--username USERNAME` | ایمیل یا شماره موبایلی که با آن وارد مکتب‌خونه می‌شوید         |
| `-p PASSWORD` | `--password PASSWORD` | رمز عبور                                                       |
| `-i`          | `--interactive`       | انتخاب تعاملی جلسات برای دانلود                                |
| `-q QUALITY`  | `--quality QUALITY`   | کیفیت ویدیو (`H` برای کیفیت بالا، `L` برای پایین – پیش‌فرض: H) |
| -             | `--path PATH`         | مسیر ذخیره‌سازی فایل‌ها (پیش‌فرض: پوشه جاری)                   |

---

## 📂 ساختار پروژه

```
.
├── maktabkhooneh           # نسخه ۱ (Selenium)
│   ├── course.py
│   ├── __init__.py
│   ├── maktabkhooneh_dl.py
│   └── parser.py
├── maktabkhooneh-dl.py     # اسکریپت اصلی نسخه ۱
├── README.md
├── requirements.txt
└── v2                      # نسخه ۲ (Playwright)
    ├── maktabkhone-dl-v2.py
    └── requirements-v2.txt
```

---

## 💡 نکات

* پیشنهاد می‌شود از **نسخه ۲** استفاده کنید مگر این که نیاز به پشتیبانی از ساختار قدیمی مکتب‌خونه داشته باشید.
* نسخه ۲ سرعت بالاتر، مدیریت خطای بهتر، و عدم نیاز به نصب geckodriver دارد.
* قبل از اجرای نسخه ۲ حتماً دستور `playwright install` را اجرا کنید.
* در صورتی که قالب مکتب خونه اپدیت شده باشد شما در نسخه ۲ کافیست  قسمت سلکتور‌ها و اپدیت کنید یعنی قسمت زیر:
```python
# -------------------- سلکتور ها --------------------
# سلکتورها در صفحه دوره 
CHAPTER_SELECTOR = "div[id^='course-chapter-']" 
CHAPTER_TITLE_SELECTOR = "div[title^='فصل'] span.text-xl" 
LESSON_SELECTOR = "a.group[href*='/ویدیو-']"
LESSON_TITLE_SELECTOR = "div.BaseChapterContentUnitTitle > span[title]"
# سلکتور دکمه دانلود در صفحه جلسه 
DOWNLOAD_SELECTOR = ".unit-content--download a[download]"
# سلکتور دکمه ورود
LOGIN_BUTTON_SELECTOR = "button#login.button[type='button']"

# -------------------- پایان سلکتور --------------------

```


