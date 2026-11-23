<div align="center">

# AURA — متجر إلكتروني متكامل

**واجهة متجر + لوحة إدارة + قواعد أمان Firestore — بدون خادم، بدون أدوات بناء**

![HTML5](https://img.shields.io/badge/HTML5-E34F26?logo=html5&logoColor=white)
![CSS3](https://img.shields.io/badge/CSS3-1572B6?logo=css3&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-ES%20Modules-F7DF1E?logo=javascript&logoColor=black)
![Firebase](https://img.shields.io/badge/Firebase-Firestore%20%2B%20Auth-FFCA28?logo=firebase&logoColor=black)
![RTL](https://img.shields.io/badge/RTL-Arabic%20%2F%20English-1f4a3c)

[العربية](#-العربية) · [English](#-english)

</div>

---

## 🇸🇦 العربية

### نظرة عامة

**AURA** متجر إلكتروني خفيف وسريع يعمل بالكامل من المتصفح فوق **Firebase**. يتكوّن من صفحتين مستقلتين:

| الملف | الوصف |
|---|---|
| `index.html` | واجهة العميل: تصفح المنتجات، السلة، الطلب، وتتبع الطلب |
| `admin.html` | لوحة الإدارة: الطلبات، المنتجات، التقارير، الإعدادات |
| `firestore.rules` | قواعد أمان Firestore |

الدفع **عند الاستلام (COD)**، والعملة **الليرة السورية الجديدة**، والواجهة **ثنائية اللغة (عربي/إنجليزي)** مع دعم كامل لاتجاه RTL.

### المزايا

**واجهة العميل**
- تصميم فاخر متجاوب مع الجوال، مع شريط علوي ثابت وبطاقات منتجات أنيقة.
- بحث ذكي يتجاهل اختلاف الهمزات والتاء المربوطة والتشكيل.
- تصنيفات وفرز (الأحدث، السعر) وفلتر العروض والمفضلة.
- نافذة عرض سريع لكل منتج مع **رابط مباشر ومشاركة** (`#product=<id>`).
- سلة محفوظة في الجهاز، وطلب كضيف بدون تسجيل.
- اختيار المحافظة مع **رسوم توصيل لكل محافظة** و**توصيل مجاني فوق مبلغ محدد**.
- تتبع الطلب برقم الطلب، مع حفظ آخر 5 طلبات في الجهاز.
- زر واتساب عائم، وشريط إعلان، وإمكانية إيقاف استقبال الطلبات مؤقتاً — كلها تُدار من لوحة الإدارة.
- تنبيه «متبقي X فقط» عند قلة المخزون.

**لوحة الإدارة**
- تسجيل دخول بالبريد وكلمة المرور مع «نسيت كلمة المرور».
- **طلبات لحظية** مع صوت وإشعار متصفح عند وصول طلب جديد.
- تغيير حالة الطلب (معلّق، مؤكد، قيد التوصيل، مكتمل، ملغي) مع **خصم المخزون وإعادته تلقائياً** داخل معاملة (Transaction) آمنة.
- تفاصيل الطلب: واتساب برسالة جاهزة، طباعة فاتورة، ملاحظة داخلية، سجل تغيّر الحالات.
- علامة ⚠ تكشف الطلبات التي يختلف مجموعها أو أسعارها عن أسعار المنتجات الحالية.
- إدارة المنتجات: إضافة، تعديل، حذف، **إخفاء دون حذف**، وتعديل المخزون مباشرة من الجدول.
- ضغط صور المنتجات تلقائياً (WebP حتى 100KB) أو استخدام رابط صورة.
- تقارير: طلبات اليوم، آخر 7 أيام، مخطط، أكثر المنتجات طلباً، وتصدير CSV.
- إعدادات المتجر: رسوم التوصيل، رسوم المحافظات، التوصيل المجاني، رقم واتساب، نص الإعلان، حد تنبيه المخزون، وإيقاف/تشغيل الطلبات.

### التقنيات

- HTML5 / CSS3 / JavaScript (ES Modules) — بدون إطار عمل وبدون خطوة بناء
- Firebase Web SDK (Firestore + Authentication) عبر CDN
- خطوط Cairo و Plus Jakarta Sans من Google Fonts

### هيكل المشروع

```
.
├── index.html        # واجهة العميل
├── admin.html        # لوحة الإدارة
├── firestore.rules   # قواعد أمان Firestore
└── README.md
```

### التشغيل السريع

#### 1) إنشاء مشروع Firebase
1. أنشئ مشروعاً من [Firebase Console](https://console.firebase.google.com).
2. فعّل **Firestore Database**.
3. فعّل **Authentication ← Email/Password**، وأنشئ حساب المدير يدوياً، ثم **عطّل التسجيل الذاتي** إن توفّر الخيار.
4. أضف تطبيق ويب (`</>`) وانسخ إعدادات `firebaseConfig`.

#### 2) ربط الإعدادات
ضع نسخة `firebaseConfig` الخاصة بك في الموضعين التاليين:
- `index.html` ← داخل `<script type="module">` في آخر الملف.
- `admin.html` ← داخل `<script type="module">`.

#### 3) تعيين المدير ونشر القواعد (بهذا الترتيب)
1. من **Authentication** انسخ **UID** حساب المدير.
2. في Firestore أنشئ مجموعة `admins` ومستنداً **معرّفه = UID** (يمكن تركه بلا حقول).
3. الصق محتوى `firestore.rules` في **Firestore ← Rules** وانشره.

> ⚠️ لا تنشر القواعد قبل إنشاء مستند `admins/<UID>`، وإلا ستفقد صلاحية الإدارة.

#### 4) إضافة المحتوى
افتح `admin.html` وسجّل الدخول، ثم:
1. من **الإعدادات** احفظ رسوم التوصيل ورقم واتساب.
2. من **المنتجات** أضف أول منتج.

#### 5) التشغيل محلياً
بسبب استخدام ES Modules شغّل خادماً محلياً بدل فتح الملف مباشرة:

```bash
npx serve .
# أو
python3 -m http.server 8080
```

### النشر على GitHub Pages

1. ارفع الملفات إلى مستودع جديد.
2. من **Settings ← Pages** اختر الفرع `main` والمجلد `/ (root)`.
3. أضف نطاق GitHub Pages (`username.github.io`) إلى **Authentication ← Settings ← Authorized domains** في Firebase.
4. المتجر على الرابط الرئيسي، والإدارة على `/admin.html`.

### نموذج البيانات (Firestore)

| المجموعة | الاستخدام | القراءة | الكتابة |
|---|---|---|---|
| `products` | المنتجات | الجميع | المدير |
| `settings/store` | إعدادات المتجر | الجميع | المدير |
| `orders` | الطلبات (بيانات شخصية) | المدير فقط | إنشاء من الزائر، والباقي للمدير |
| `tracking` | حالة الطلب فقط للتتبع العام | بالرقم | إنشاء من الزائر، والتحديث للمدير |
| `admins` | قائمة المديرين | المدير نفسه | ممنوع من العميل |

**حقول `settings/store`:** `deliveryFee`, `deliveryFees` (خريطة المحافظة ← الرسم), `freeShippingOver`, `lowStockThreshold`, `whatsapp`, `announcement`, `storeOpen`, `currency`.

**حقول المنتج:** `nameAr`, `nameEn`, `descriptionAr`, `descriptionEn`, `price`, `oldPrice`, `category`, `stock`, `isNew`, `image`, `active`.

التصنيفات المدعومة: `electronics`, `fashion`, `accessories`, `homeCategory`.

### الأمان

- مفاتيح Firebase في الواجهة **غير سرية بطبيعتها**؛ الحماية الفعلية تأتي من `firestore.rules`.
- الإدارة مقيّدة بمستند `admins/<UID>` وليس بمجرد تسجيل الدخول.
- بيانات الزبائن (الاسم والهاتف والعنوان) لا تُقرأ إلا من المدير، والتتبع العام يكشف الحالة فقط.
- رقم الطلب عشوائي (96 بتاً) ولا يمكن تخمينه.
- **يُنصح بشدة:** تقييد مفتاح API بنطاقات موقعك من Google Cloud Console (HTTP referrers)، وتفعيل **Firebase App Check** لتقليل الطلبات الوهمية.
- أسعار الطلب تُرسل من المتصفح؛ تحقّق من علامة ⚠ في الإدارة قبل تأكيد أي طلب، ويُفضّل لاحقاً نقل الحساب إلى Cloud Function.

### القيود المعروفة وخارطة الطريق

- [ ] خيارات المنتج (المقاس واللون) وصور متعددة
- [ ] إدارة التصنيفات من لوحة الإدارة
- [ ] نقل الصور إلى Firebase Storage (يتطلب خطة Blaze)
- [ ] إشعارات الدفع (FCM) وتحويل لوحة الإدارة إلى PWA
- [ ] التحقق من الأسعار على الخادم (Cloud Functions)
- [ ] أكواد الخصم وتقييمات حقيقية للمنتجات

### المساهمة

المساهمات مرحّب بها: افتح **Issue** لمناقشة التغيير، ثم أرسل **Pull Request**.

### الترخيص

اختر ترخيصاً مناسباً (مثل MIT) وأضف ملف `LICENSE` إلى المستودع.

---

## 🇬🇧 English

### Overview

**AURA** is a lightweight, serverless e-commerce store that runs entirely in the browser on top of **Firebase**. It ships as two standalone pages plus security rules:

| File | Purpose |
|---|---|
| `index.html` | Customer storefront: browse, cart, checkout, order tracking |
| `admin.html` | Admin dashboard: orders, products, reports, settings |
| `firestore.rules` | Firestore security rules |

Payment is **Cash on Delivery**, the currency is the **new Syrian pound**, and the UI is **bilingual (Arabic/English)** with full RTL support.

### Features

**Storefront**
- Premium responsive design with a sticky glass header and refined product cards.
- Arabic-aware search (normalizes hamza, ta marbuta and diacritics).
- Categories, sorting, offers filter and wishlist.
- Quick-view modal with **deep links and sharing** (`#product=<id>`).
- Persistent cart, guest checkout with no sign-up.
- Governorate selector with **per-governorate delivery fees** and a **free-delivery threshold**.
- Order tracking by order number, plus the last 5 orders remembered on the device.
- Floating WhatsApp button, announcement bar and a "pause orders" switch, all controlled from the admin.
- "Only X left" low-stock label.

**Admin dashboard**
- Email/password login with password reset.
- **Real-time orders** with sound and browser notifications.
- Status workflow (pending, confirmed, shipping, completed, cancelled) with **automatic stock deduction and restoration** inside a Firestore transaction.
- Order details: WhatsApp with a prefilled message, printable invoice, internal notes and a status history.
- ⚠ flag for orders whose totals or prices differ from current product prices.
- Product management: add, edit, delete, **hide without deleting**, inline stock editing.
- Automatic image compression (WebP up to 100KB) or image URLs.
- Reports: today's orders, last 7 days chart, top products and CSV export.
- Store settings: delivery fees, per-governorate fees, free delivery threshold, WhatsApp number, announcement text, low-stock threshold and an orders on/off switch.

### Tech stack

- HTML5 / CSS3 / vanilla JavaScript (ES Modules): no framework, no build step
- Firebase Web SDK (Firestore + Authentication) via CDN
- Cairo and Plus Jakarta Sans from Google Fonts

### Project structure

```
.
├── index.html        # storefront
├── admin.html        # admin dashboard
├── firestore.rules   # Firestore security rules
└── README.md
```

### Getting started

#### 1) Create a Firebase project
1. Create a project in the [Firebase Console](https://console.firebase.google.com).
2. Enable **Firestore Database**.
3. Enable **Authentication, Email/Password**, create the admin user manually and **disable self sign-up** if available.
4. Register a web app (`</>`) and copy its `firebaseConfig`.

#### 2) Wire up your config
Paste your `firebaseConfig` in both places:
- `index.html`, inside the final `<script type="module">`.
- `admin.html`, inside its `<script type="module">`.

#### 3) Set the admin and publish the rules (in this order)
1. Copy the admin's **UID** from **Authentication**.
2. In Firestore create a collection `admins` with a document whose **ID equals that UID** (no fields required).
3. Paste `firestore.rules` into **Firestore, Rules** and publish.

> ⚠️ Do not publish the rules before creating `admins/<UID>`, or you will lock yourself out of the admin.

#### 4) Add content
Open `admin.html`, sign in, then save your delivery fee and WhatsApp number under **Settings**, and add your first product under **Products**.

#### 5) Run locally
ES Modules need a web server (do not open the files via `file://`):

```bash
npx serve .
# or
python3 -m http.server 8080
```

### Deploy to GitHub Pages

1. Push the files to a new repository.
2. Go to **Settings, Pages**, choose branch `main` and folder `/ (root)`.
3. Add your Pages domain (`username.github.io`) to **Authentication, Settings, Authorized domains** in Firebase.
4. The store is served at the root URL and the admin at `/admin.html`.

### Data model (Firestore)

| Collection | Purpose | Read | Write |
|---|---|---|---|
| `products` | Catalog | Public | Admin |
| `settings/store` | Store settings | Public | Admin |
| `orders` | Orders (personal data) | Admin only | Guest create, admin for the rest |
| `tracking` | Status-only public tracking | By code | Guest create, admin update |
| `admins` | Admin allow-list | Self | Blocked from clients |

**`settings/store` fields:** `deliveryFee`, `deliveryFees` (governorate → fee map), `freeShippingOver`, `lowStockThreshold`, `whatsapp`, `announcement`, `storeOpen`, `currency`.

**Product fields:** `nameAr`, `nameEn`, `descriptionAr`, `descriptionEn`, `price`, `oldPrice`, `category`, `stock`, `isNew`, `image`, `active`.

Supported categories: `electronics`, `fashion`, `accessories`, `homeCategory`.

### Security

- Firebase keys in client code are **public by design**; real protection comes from `firestore.rules`.
- Admin access is tied to an `admins/<UID>` document, not to merely being signed in.
- Customer data (name, phone, address) is readable only by the admin; public tracking exposes the status only.
- Order numbers are random (96 bits) and not guessable.
- **Strongly recommended:** restrict the API key to your domains (HTTP referrers) in Google Cloud Console, and enable **Firebase App Check** to reduce fake orders.
- Order prices are sent from the browser; check the ⚠ flag in the admin before confirming an order, and consider moving order creation to a Cloud Function later.

### Known limitations and roadmap

- [ ] Product variants (size/color) and multiple images
- [ ] Category management from the admin
- [ ] Move images to Firebase Storage (requires the Blaze plan)
- [ ] Push notifications (FCM) and an installable admin PWA
- [ ] Server-side price validation (Cloud Functions)
- [ ] Discount codes and real product reviews

### Contributing

Contributions are welcome: open an **Issue** to discuss a change, then send a **Pull Request**.

### License

Choose a license (for example MIT) and add a `LICENSE` file to the repository.
