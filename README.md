سلام وقت بخیر باشه!
در این قسمت راجب به کد های سایتی که طراحی کردم قراره توضیح بدم:

flyto:

- frontend: HTML/CSS/JS ساده (پوشه `frontend/`)
- backend: Node.js + Express (پوشه `backend/`)
- database: SQLite 

flyto/
├── backend/
│   ├── server.js          ورودی اصلی سرور Express
│   ├── db/
│   │   ├── database.js      اتصال به SQLite 
│   │   ├── init.js          ساخت جداول + داده‌های اولیه (seed)
│   │   └── flyto.sqlite   فایل دیتابیس (پس از اجرا ساخته می‌شود)
│   ├── routes/
│   │   ├── auth.js         ثبت‌نام / ورود
│   │   ├── flights.js      جستجوی پرواز
│   │   ├── bookings.js     رزرو + پرداخت
│   │   ├── admin.js        پنل مدیریت (CRUD پروازها، لیست رزروها و کاربران)
│   │   └── newsletter.js   عضویت خبرنامه
│   ├── middleware/auth.js  میان‌افزار احراز هویت JWT
│   ├── package.json
│   └── .env.example
└── frontend/
    ├── index.html           صفحه اصلی سایت
    ├── admin.html           پنل مدیریت
    ├── css/style.css
    └── js/
        ├── app.js           منطق صفحه اصلی (جستجو، ورود، رزرو، پرداخت)
        └── admin.js         منطق پنل مدیریت




برای ران کردن باید
 node.js 
رو دانلود کنیم و روی ویندوز نصب کنیم

و بعد در
 vsکد باید ترمینال رو باز کنیم و :
cd backend
npm install
cp .env.example .env     
npm start

npm install:
تمام پکیج‌ها و وابستگی‌های (dependencies) پروژه که توی فایل package.json تعریف شدن رو نصب می‌کنه (مثل Express، Mongoose، dotenv و غیره). این مرحله معمولاً یه پوشه‌ی node_modules می‌سازه.


cp .env.example .env :
تمام پکیج‌ها و وابستگی‌های (dependencies) پروژه که توی فایل package.json تعریف شدن رو نصب می‌کنه (مثل Express، Mongoose، dotenv و غیره). این مرحله معمولاً یه پوشه‌ی
 node_modules می‌سازه.

npm start:
یه کپی از فایل .env.example می‌سازه و اسمش رو می‌ذاره .env.

فایل .env.example معمولاً یه نمونه/الگو از متغیرهای محیطی مورد نیاز پروژه است (مثل آدرس دیتابیس، پورت، کلید JWT و...) بدون مقدار واقعی.
فایل .env نسخه واقعی‌ایه که باید مقادیر واقعی توش پر بشه (چون .env معمولاً توی .gitignore هست و به گیت‌هاب پوش نمی‌شه، برای امنیت).

پیست کنیم تا سرور روی آدرس بالا بیاد :
http://localhost:4000


frontend:
 جستجوی پرواز داخلی/خارجی با فراخوانی API واقعی
 فرم ورود و ثبت‌نام کاربر (مودال)
 فرم رزرو و پرداخت (مودال با اعتبارسنجی ساده کارت)
 فرم عضویت در خبرنامه

backend:

| Method | Route 
|---|---|---|
| POST | `/api/auth/register` | ثبت‌نام کاربر |
| POST | `/api/auth/login` | ورود کاربر |
| GET  | `/api/auth/me` | اطلاعات کاربر لاگین‌شده |
| GET  | `/api/flights` | جستجوی پرواز (`?type=&from=&to=`) |
| GET  | `/api/flights/:id` | جزئیات یک پرواز |
| POST | `/api/bookings` | ثبت رزرو (نیازمند ورود) |
| GET  | `/api/bookings/me` | لیست رزروهای کاربر |
| POST | `/api/bookings/:id/pay` | پرداخت رزرو (درگاه نمایشی) |
| POST | `/api/newsletter` | عضویت در خبرنامه |
| GET  | `/api/admin/summary` | آمار کلی (فقط مدیر) |
| GET/POST/PUT/DELETE | `/api/admin/flights` | مدیریت پروازها (فقط مدیر) |
| GET | `/api/admin/bookings` | لیست همه رزروها (فقط مدیر) |
| GET | `/api/admin/users` | لیست کاربران (فقط مدیر) |

(SQLite)
جداول: `users`، `flights`، `bookings`، `payments`، `newsletter`

