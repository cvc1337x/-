توجيه سريع لنشر هذا المشروع (HTML ثابت) وتهيئة الدومين

الخطوات قبل النشر (ضروري)
- افتح `index.html` و`auth-callback.html` وضع قيمة `Application (client) ID` الناتجة من Azure بدل `YOUR_CLIENT_ID_HERE`.
- تأكد أن Redirect URI في Azure App Registration يطابق عنوان الاستضافة (مثال: `https://yourdomain.com/` أو `https://yourdomain.com/auth-callback.html`).

تشغيل محلي للاختبار
1) من المجلد المشروع شغّل سيرفر HTTP بسيط (Python):

```powershell
# داخل المجلد c:\Users\LENOVO\Downloads\1
python -m http.server 5500
# أو
py -3 -m http.server 5500
```
ثم افتح: http://localhost:5500/

نشر عبر GitHub + Netlify (موصى به للمبتدئين)
1. ارفع المشروع إلى GitHub:
```bash
cd path/to/project
git init
git add .
git commit -m "initial"
# أنشئ مستودع على GitHub ثم:
git remote add origin https://github.com/YOUR_USERNAME/YOUR_REPO.git
git branch -M main
git push -u origin main
```
2. في Netlify:
- سجّل دخولك إلى https://app.netlify.com
- New site → Import from Git → اختر GitHub ثم المستودع
- اضبط Build settings (لموقع ثابت لا تحتاج build، اتركها فارغة) وPublish directory = `/`
- انشر الموقع، Netlify سيعطيك عنوانًا مثل `yoursite.netlify.app`.
- لإضافة دومين مخصص: Site settings → Domain management → Add custom domain → اتبع تعليمات DNS (CNAME أو A records).
- Netlify يصدر شهادة TLS تلقائياً.

نشر عبر GitHub Pages (بدون Netlify)
- ضع المشروع على فرع `main` ثم في إعدادات المستودع GitHub → Pages → اختَر `main` و`/(root)`.
- إذا تريد دومين مخصص أضف ملف `CNAME` في root يحتوي `yourdomain.com` ثم عدل DNS كما في الوثيقة.

نشر عبر Azure Static Web Apps (مناسب إذا تستخدم Azure AD)
- في Azure Portal أنشئ `Static Web App` واربطه بالمستودع GitHub (يوجد Action يجرّب البناء والنشر تلقائياً).
- بعد النشر: من لوحة Static Web App → Custom domains → أضف الدومين واتبّع تعليمات DNS.
- عدّل Redirect URI في App Registration إلى الدومين المنشور (مثال: `https://yourdomain.com/`).

نقطة مهمة حول OAuth Redirect
- Redirect URI المسجّل في Azure AD يجب أن يكون مطابقًا تمامًا للعنوان المستخدم في التطبيق (بروتوكول، hostname، path).
- مثال: إذا استخدمت Netlify وعنوان الموقع `https://myapp.netlify.app` سجّل `https://myapp.netlify.app/` أو `https://myapp.netlify.app/auth-callback.html` حسب إعدادك.

استخدام ngrok لاختبار رابط عام مؤقت (بدون نشر)
- ثبت ngrok وابدأ:
```powershell
ngrok http 5500
```
- انسخ الرابط العام `https://xxxxxx.ngrok.io` واستخدمه كـ Redirect URI مؤقت في Azure.

ماذا أستطيع أفعله لك الآن؟
- أ) أساعدك برفع المشروع إلى GitHub (أعطني اسم المستخدم واسم المستودع أو فعّل GitHub CLI محليًا).
- ب) أجهز نشرًا على Netlify (أرشدك حيث تدخل وتمدني بصلاحيات أو أتولى الخطوات إن منحت الوصول).
- ج) أجهز Azure Static Web App (أحتاج صلاحيات Azure أو أوجّهك خطوة بخطوة).

أخبرني أي خيار تريده لأقدّم الأوامر الدقيقة أو أكمّل الإعداد عوضك.