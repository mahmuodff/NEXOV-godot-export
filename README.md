# استخدام android_source.zip في مشروع جودوت

يستخدم عند بناء المشروع بـ **Gradle** (مثلاً لتصدير AAB، أو عند استخدام plugins). للتصدير العادي إلى APK بدون Gradle لا حاجة له.

## الخطوات

1. افتح مجلد مشروعك (المجلد اللي فيه `project.godot`).
2. أنشئ المجلدين `android` وبداخله `build`، فيصير المسار `مشروعك/android/build/`.
3. فك `android_source.zip` داخل `build/` بحيث تكون الملفات مباشرة داخله (مثل `build.gradle` و`src` و`libs`)، مو داخل مجلد إضافي.
4. أنشئ ملف نصي اسمه `.build_version` داخل مجلد `android/` (مو داخل `build/`)، واكتب فيه إصدار محركك فقط، مثل `4.7.2.stable`.
5. أنشئ ملف فاضي اسمه `.gdignore` داخل `android/build/`.
6. افتح المشروع في جودوت، وفي Export preset فعّل **Use Gradle Build**.

## الشكل النهائي

```
مشروعك/
├── project.godot
└── android/
    ├── .build_version
    └── build/
        ├── .gdignore
        ├── build.gradle
        ├── src/
        └── libs/
```

لو تشتغل من الجوال، نفس الخطوات تسويها بمدير الملفات، وتحط المجلد داخل مجلد المشروع.

## فايدة الملفين الصغيرين

- `.build_version`: يخبر جودوت بإصدار الـ Build Template المثبّت. لو اختلف عن إصدار المحرك يعطيك تحذير تعيد التثبيت.
- `.gdignore`: يخلي جودوت يتجاهل مجلد `android/build/` فلا يفحص ملفات Java وGradle كأنها جزء من اللعبة.

## ملاحظات

- لو غيّرت القالب لاحقاً (إصدار جديد أو أعدت البناء)، احذف مجلد `android/build/` وأعد الخطوات.
- الـ Build Template لازم يكون من نفس إصدار المحرك المستخدم.
- مكتبات arm32 وarm64 موجودة داخل `android_source.zip` لأنه مبني بـ `generate_android_binaries=yes`.
