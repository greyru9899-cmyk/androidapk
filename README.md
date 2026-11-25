# নখাপাড়া সরকারি প্রাথমিক বিদ্যালয় — Android অ্যাপ (ফোন, ট্যাবলেট, Google TV)

এই প্রজেক্টে সাইটের HTML ফাইলটি (`app/src/main/assets/site/index.html`) একটি WebView-তে
পূর্ণ স্ক্রিনে চালানো হয়। ওয়েব সাইটের ফাইলে কোনো পরিবর্তন করা হয়নি। অ্যাপের জন্য
আলাদা স্তর (`app/src/main/assets/app/app-start.js`) শুধু অ্যাপের ভেতরে যোগ হয়:

| চাহিদা | কীভাবে করা হয়েছে |
|---|---|
| প্রতিটি সেকশন একটি করে, বড় পর্দায় | সাইটের ট্যাব-ব্যবস্থায় একবারে একটি সেকশন দেখায়; অ্যাপে সেটি পুরো প্রস্থে ও বড় লেখায় দেখানো হয় |
| মোবাইল ও Google TV-তে রেসপনসিভ | ফোন/ট্যাবলেটে `মোবাইল`/`ট্যাব` ভিউ, Google TV-তে `টিভি` ভিউ স্বয়ংক্রিয়ভাবে বেছে নেওয়া হয় |
| হ্যাম্বার্গার মেনু বড় করে দেখানো | মেনু পূর্ণ স্ক্রিনে খোলে, বোতামগুলো ৩৪ px লেখা ও বড় টাচ/রিমোট-টার্গেট সহ |
| রিমোট কন্ট্রোল (D-pad) | তীর বোতাম দিয়ে কাছের বোতামে ফোকাস যায়, OK চাপলে সক্রিয় হয়, হলুদ ফোকাস-রিং দেখায় |
| Back বোতাম | মেনু খোলা থাকলে সেটি বন্ধ হয়; অন্য সেকশনে থাকলে ড্যাশবোর্ডে ফেরে; ড্যাশবোর্ডে থাকলে অ্যাপ বন্ধ হয় |
| ফাইল ডাউনলোড ও প্রিন্ট | ডাউনলোড `Downloads` ফোল্ডারে যায়; `window.print()` সিস্টেমের প্রিন্ট ডায়ালগ খোলে |
| ফাইল আপলোড, ক্যামেরা, মাইক্রোফোন | অ্যান্ড্রয়েডের অনুমতি চেয়ে সাইটে দেওয়া হয় |

## ১. প্রয়োজনীয় সফটওয়্যার

- **Android Studio** (Koala 2024.1 বা নতুন)। এতে JDK 17 থাকে।
- **Android SDK Platform 34** (Android Studio-র SDK Manager থেকে ইনস্টল করুন)।

## ২. প্রজেক্ট খোলা

1. Android Studio-তে **File → Open** করে `NakhaparaSchoolAndroid` ফোল্ডারটি বেছে নিন।
2. প্রথমবার Gradle sync নিজে থেকে চলবে এবং `gradle-wrapper.jar` তৈরি করবে। ইন্টারনেট লাগবে।
3. কোনো error থাকলে **Build → Clean Project**, তারপর **Build → Rebuild Project** চালান।

## ৩. চালানো ও পরীক্ষা

- **ফোনে:** ফোনের Developer options-এ USB debugging চালু করে ফোন কানেক্ট করুন, তারপর ▶ (Run) চাপুন।
- **Google TV / Android TV (এমুলেটর):** Device Manager → Create device → **TV** → Google TV image (API 34) বেছে চালান।
  এমুলেটরে রিমোটের তীর কী (↑ ↓ ← →) ও Enter দিয়ে পরীক্ষা করুন।

পরীক্ষার তালিকা:
- অ্যাপ খুললে TV-তে টিভি ভিউ আসে, ফোনে মোবাইল ভিউ।
- ☰ (উপরে ডানে) চাপলে বড় মেনু আসে; একটি সেকশন বাছলে মেনু বন্ধ হয় এবং শুধু সেই সেকশন দেখা যায়।
- Back চাপলে মেনু বন্ধ হয়, তারপর ড্যাশবোর্ডে ফেরা যায়।
- কোনো রিপোর্ট বা ফাইল ডাউনলোড করলে Downloads-এ ফাইল আসে।
- "প্রিন্ট" চাপলে সিস্টেম প্রিন্ট ডায়ালগ খোলে। (প্রিন্ট-প্রিভিউ আলাদা উইন্ডোয় খোলে; সেটি একবার নিশ্চিত করে নিন।)

## ৪. APK / AAB তৈরি

- পরীক্ষার জন্য: **Build → Build App Bundle(s) / APK(s) → Build APK(s)**।
  ফলাফল: `app/build/outputs/apk/debug/app-debug.apk`।
- Play Store-এ দিতে: **Build → Generate Signed App Bundle / APK**, নতুন keystore বানান এবং সেটি নিরাপদে রাখুন।

## ৫. সাইট আপডেট করা

- নতুন সাইটের ফাইল হলে `app/src/main/assets/site/index.html` ফাইলটি প্রতিস্থাপন করুন (নামটি একই থাকবে)।
- অ্যাপের বড় পর্দার স্টাইল বা রিমোট-নেভিগেশন বদলাতে `app/src/main/assets/app/app-start.js` সম্পাদনা করুন।
  এই ফাইল শুধু অ্যাপে চলে, ওয়েব সাইটে নয়।
- সাইটের ভেতরের ব্যবহারের `ngps101_preferred_device_view` সেটিংটি অ্যাপ নিজে থেকেই `tv` করে, যদি ব্যবহারকারী আগে কোনো ভিউ বেছে না থাকেন।

## ৬. গুরুত্বপূর্ণ বিষয়

- **ইন্টারনেট দরকার।** সাইট Tailwind, Google Fonts, Firebase ও অন্যান্য লাইব্রেরি ইন্টারনেট থেকে লোড করে।
  অফলাইনে লেআউট ভেঙে যেতে পারে। অফলাইন সমর্থন চাইলে এই লাইব্রেরিগুলো অ্যাপের assets-এ নামিয়ে নিতে হবে।
- **Firebase Sign-in:** অ্যাপ সাইটটি `https://appassets.androidplatform.net` ঠিকানায় চালায়। Firebase Authentication ব্যবহার করলে
  Firebase Console → Authentication → Settings → **Authorized domains**-এ `appassets.androidplatform.net` যোগ করুন।
- **Google TV Play Store:** টিভি অ্যাপের জন্য আলাদা ব্যানার (`tv_banner.xml`, ১৮০ × ৩২০ dp) ও 1920×1080 স্ক্রিনশট লাগে।
  এগুলো Play Console-এ আপলোড করতে হবে।
- এই প্রজেক্ট তৈরির সময় Android SDK ছিল না, তাই Kotlin কোড কম্পাইল করে যাচাই করা হয়নি। প্রথম Build-এ
  কোনো error দেখালে সেটির বার্তা পাঠালে ঠিক করে দেওয়া যাবে।

## ৭. GitHub Actions দিয়ে অনলাইনে APK / AAB তৈরি

প্রজেক্টে `.github/workflows/android-build.yml` ফাইলটি আছে। এটি GitHub-এর সার্ভারে অ্যাপ বানায়,
তাই আপনার কম্পিউটারে Android Studio বা SDK লাগে না।

**ধাপ ১: GitHub-এ প্রজেক্ট রাখা**
1. GitHub-এ নতুন একটি repository বানান (Private রাখতে পারেন)।
2. এই `NakhaparaSchoolAndroid` ফোল্ডারের ভেতরে নিচের কমান্ড চালান:
   ```
   git init
   git add .
   git commit -m "Android app"
   git branch -M main
   git remote add origin https://github.com/আপনার-নাম/repo-নাম.git
   git push -u origin main
   ```
3. Push করলেই **Actions** ট্যাবে build শুরু হবে।

**ধাপ ২: Debug APK নামানো (সাইনিং ছাড়া, পরীক্ষার জন্য)**
- Actions → চালানো build → **Artifacts** থেকে `nakhapara-school-debug-apk` ডাউনলোড করুন।
- APK টি ফোনে বা TV-তে ইনস্টল করে পরীক্ষা করতে পারবেন।

**ধাপ ৩: Google Play-র জন্য সাইন করা build (ঐচ্ছিক)**
Play Store-এ দিতে হলে একটি upload key লাগবে। এটি একবারই বানাতে হয়:
```
keytool -genkeypair -v -keystore upload-key.jks -keyalg RSA -keysize 2048 -validity 10000 -alias upload
```
তারপর keystore-কে base64-এ বদলান (macOS/Linux): `base64 -w0 upload-key.jks`
(macOS-এ `-w0` না থাকলে `base64 upload-key.jks | tr -d '\n'`)।

GitHub repository → **Settings → Secrets and variables → Actions** এ এই চারটি secret যোগ করুন:

| Secret | কী দিতে হবে |
|---|---|
| `ANDROID_KEYSTORE_BASE64` | উপরে base64-এ বদলানো keystore-এর লেখা |
| `ANDROID_KEYSTORE_PASSWORD` | keystore-এর পাসওয়ার্ড |
| `ANDROID_KEY_ALIAS` | উপরের কমান্ডে দেওয়া alias (যেমন `upload`) |
| `ANDROID_KEY_PASSWORD` | key-এর পাসওয়ার্ড |

এরপর build চালালে **nakhapara-school-release-aab** (Play Store-এ আপলোডের জন্য) ও
**nakhapara-school-release-apk** artifact তৈরি হবে। প্রতিটি build-এ `versionCode` স্বয়ংক্রিয়ভাবে বাড়ে
(GitHub run number), তাই Play-তে নতুন সংস্করণ আপলোড করতে কোনো সমস্যা হবে না।

**গুরুত্বপূর্ণ:** `upload-key.jks` ফাইল ও পাসওয়ার্ড কোথাও নিরাপদে রাখুন। এগুলো হারিয়ে গেলে ভবিষ্যতে
একই অ্যাপের আপডেট দেওয়া কঠিন হবে। এই ফাইল কখনো GitHub repository-তে commit করবেন না।
