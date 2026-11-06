مشروع تطبيق تمارين الترتيب - Android Studio

محتويات المشروع:
- app/src/main/assets/index.html : ملف HTML المرفق بعد وضعه داخل أصول التطبيق.
- MainActivity.java : WebView مع WebViewAssetLoader وصلاحية الميكروفون وملفات الصور/JSON.
- AndroidManifest.xml : صلاحية تسجيل الصوت فقط؛ لا يحتاج التطبيق صلاحيات تخزين عامة.

طريقة إنشاء APK:
1) فك ضغط ArrangeTeacherApp.zip.
2) افتح Android Studio واختر Open ثم اختر مجلد ArrangeTeacherApp.
3) انتظر Gradle Sync، وثبّت Android SDK Platform 35 إذا طلبه Android Studio.
4) من القائمة Build اختر Build APK(s).
5) ملف APK التجريبي يظهر عادة في app/build/outputs/apk/debug/app-debug.apk.

ملاحظات:
- تم تقديم ملفات assets من خلال WebViewAssetLoader على أصل HTTPS محلي موثوق؛ هذا أنسب من file:// لواجهات getUserMedia/MediaRecorder الحديثة.
- لا يحتاج تشغيل HTML والصور المحلية إلى إنترنت. لا توجد روابط CDN في ملف HTML المرفق.
- الميكروفون يطلب إذن أندرويد عند أول محاولة تسجيل، ثم يمنح WebView إذن Audio Capture.
- اختيار الصور واستيراد JSON يعمل عبر منتقي ملفات أندرويد.
- بيانات localStorage مرتبطة بأصل التطبيق المحلي وتبقى عادة بعد إغلاق التطبيق، وتحذف عند مسح بيانات التطبيق أو إلغاء تثبيته.
- تصدير النسخة الاحتياطية من Blob download قد يختلف سلوكه بين إصدارات WebView؛ اختبر زر التصدير على الهاتف المستهدف. الاستيراد واختيار الصور يستخدمان منتقي الملفات.
- يجب اختبار التسجيل فعلياً على جهاز أندرويد بعد البناء، لأن سلوك MediaRecorder يعتمد أيضاً على إصدار Android System WebView.

بناء APK عبر GitHub Actions (بدون Android Studio):
1) ارفع محتوى المجلد (بما فيه .github) إلى مستودع GitHub.
2) من تبويب Actions شغّل Build APK، ثم نزّل ملف ArrangeTeacher-APK من Artifacts.

تحديث: زر التصدير صار يفتح منتقي حفظ أندرويد لاختيار مكان ملف arrange-backup.json.

تحسينات النسخة 2: وضع التحدي (الخطأ يُحتسب مع اهتزاز وصوت)، نجوم النتيجة، إصلاح ظهور الواجهة تحت شريط الحالة في أندرويد 15، وضبط لوحة المفاتيح.
