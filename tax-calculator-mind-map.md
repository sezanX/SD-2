**প্রজেক্ট: Tax Calculator BD (Android - Java/Kotlin & XML)**

```
Tax Calculator BD (App Root)
│
├── 📁 app (অ্যাপ্লিকেশন মডিউল)
│   │
│   ├── 📁 manifests
│   │   └── 📄 AndroidManifest.xml
│   │       ├── Purpose: অ্যাপের মূল কনফিগারেশন ফাইল।
│   │       ├── Contents:
│   │       │   ├── Package Name, Permissions (e.g., INTERNET, WRITE_EXTERNAL_STORAGE)
│   │       │   ├── Application Theme, Icon, Label
│   │       │   ├── Activity Declarations (MainActivity, DeveloperInfoActivity)
│   │       │   │   └── Intent Filters (LAUNCHER for MainActivity)
│   │       │   └── Provider Declaration (FileProvider for PDF sharing)
│   │       └── How it Works: সিস্টেমকে অ্যাপের গঠন এবং উপাদান সম্পর্কে জানায়।
│   │
│   ├── 📁 java/kotlin (সোর্স কোড)
│   │   └── 📂 com.sezanx.taxcalculatorbd (আপনার প্যাকেজ নাম)
│   │       ├── 📄 MainActivity.kt
│   │       │   ├── Purpose: অ্যাপের প্রধান স্ক্রিন এবং মূল লজিক পরিচালনা করে।
│   │       │   ├── Key Components:
│   │       │   │   ├── ViewBinding (`ActivityMainBinding`)
│   │       │   │   ├── Tax Constants (Slab limits, rates, rebate rules, minimum tax)
│   │       │   │   ├── UI Event Handlers (`setupButtonClickListeners`, `onOptionsItemSelected`)
│   │       │   │   ├── Tax Calculation Logic (`calculateAndDisplayTax`, `getTaxFreeLimit`, `calculateTaxSlabs`, `calculateRebate`)
│   │       │   │   ├── UI Update Logic (`displayResults`, `formatCurrency`)
│   │       │   │   ├── Input Validation (`getInputAsDouble`)
│   │       │   │   ├── PDF Generation & Sharing (`generatePdfReport`, `sharePdf`)
│   │       │   │   ├── Keyboard Management (`hideKeyboard`)
│   │       │   │   └── Options Menu (for Developer Info)
│   │       │   └── How it Works: XML লেআউট ইনফ্লেট করে, ইউজারের ইনপুট নেয়, ট্যাক্স হিসাব করে এবং ফলাফল দেখায়।
│   │       │
│   │       └── 📄 DeveloperInfoActivity.kt
│   │           ├── Purpose: "Developer Info" স্ক্রিন প্রদর্শন করে।
│   │           ├── Key Components:
│   │           │   ├── ViewBinding (`ActivityDeveloperInfoBinding`)
│   │           │   ├── Toolbar setup (`setSupportActionBar`, `setDisplayHomeAsUpEnabled`)
│   │           │   ├── Link Click Handlers (`setupLinkListeners`) for Email, GitHub, LinkedIn
│   │           │   └── Intent usage (`ACTION_SENDTO`, `ACTION_VIEW`) to open external apps.
│   │           └── How it Works: লেআউট দেখায় এবং ইন্টারেক্টিভ লিঙ্ক তৈরি করে।
│   │
│   ├── 📁 res (রিসোর্স)
│   │   │
│   │   ├── 📁 drawable
│   │   │   ├── 📄 ic_check_circle.xml (Vector Drawable for "Filed" status - যদিও বর্তমানে ব্যবহৃত হচ্ছে না)
│   │   │   ├── 📄 dev_profile_pic.png/jpg (Your profile image)
│   │   │   └── 📄 bg_spinner.xml (Spinner এর জন্য কাস্টম ব্যাকগ্রাউন্ড)
│   │   │       └── Purpose: অ্যাপে ব্যবহৃত গ্রাফিকাল অ্যাসেট (আইকন, ছবি, কাস্টম UI উপাদান)।
│   │   │
│   │   ├── 📁 layout
│   │   │   ├── 📄 activity_main.xml
│   │   │   │   ├── Purpose: প্রধান স্ক্রিনের UI গঠন ডিফাইন করে।
│   │   │   │   ├── Structure: CoordinatorLayout > AppBarLayout > MaterialToolbar > NestedScrollView > LinearLayout (for Cards)
│   │   │   │   ├── Cards: Input Card, Results Card, Tax Slabs Card.
│   │   │   │   └── How it Works: XML ট্যাগ ব্যবহার করে UI উপাদান (Buttons, TextViews, EditTexts, Spinners, CardViews) সাজায়।
│   │   │   │
│   │   │   ├── 📄 activity_developer_info.xml
│   │   │   │   ├── Purpose: "Developer Info" স্ক্রিনের UI গঠন ডিফাইন করে।
│   │   │   │   ├── Structure: CoordinatorLayout > AppBarLayout > MaterialToolbar > NestedScrollView > CardView (for info)
│   │   │   │   └── Contents: ImageView (profile pic), TextViews (name, university, contact, links).
│   │   │   │
│   │   │   └── (📄 item_tax_quarter.xml - ডিলিট করা হয়েছে)
│   │   │
│   │   ├── 📁 menu
│   │   │   └── 📄 main_menu.xml
│   │   │       ├── Purpose: MainActivity-তে Options Menu ডিফাইন করে।
│   │   │       └── Contents: Item for "Developer Info".
│   │   │
│   │   ├── 📁 values
│   │   │   ├── 📄 colors.xml
│   │   │   │   └── Purpose: অ্যাপে ব্যবহৃত বিভিন্ন রঙের Hex কোড ডিফাইন করে (e.g., colorPrimary, colorBackground, colorOnSurfacePrimary)।
│   │   │   ├── 📄 strings.xml
│   │   │   │   └── Purpose: অ্যাপে প্রদর্শিত সকল টেক্সট (UI labels, messages, errors, array for spinner) ডিফাইন করে, যা লোকালাইজেশনের জন্য গুরুত্বপূর্ণ।
│   │   │   ├── 📄 themes.xml
│   │   │   │   └── Purpose: অ্যাপের সামগ্রিক লুক এবং ফিল (App Theme), ডিফল্ট কম্পোনেন্ট স্টাইল এবং স্ট্যাটাস বার কনফিগারেশন ডিফাইন করে।
│   │   │   ├── 📄 styles.xml
│   │   │   │   └── Purpose: নির্দিষ্ট UI উপাদান বা টেক্সট অ্যাপিয়ারেন্সের জন্য কাস্টম স্টাইল ডিফাইন করে (e.g., CardTitle, ResultRowLayout, SlabRowLayout)।
│   │   │   └── 📄 attrs.xml
│   │   │       └── Purpose: কাস্টম অ্যাট্রিবিউট ডিফাইন করে (e.g., `statusBarHeight`, যদিও বর্তমানে সরাসরি কোড থেকে হ্যান্ডেল করা হচ্ছে)।
│   │   │
│   │   └── 📁 xml
│   │       └── 📄 provider_paths.xml
│   │           └── Purpose: `FileProvider`-এর জন্য পাথ ডিফাইন করে, যা PDF ফাইল শেয়ার করার সময় অ্যাপের বাইরে ফাইল অ্যাক্সেস করতে সাহায্য করে।
│   │
│   └── 📄 build.gradle (Module: app) বা build.gradle.kts
│       ├── Purpose: এই মডিউলের জন্য বিল্ড কনফিগারেশন, SDK ভার্সন এবং লাইব্রেরি ডিপেন্ডেন্সি ডিফাইন করে।
│       ├── Key Sections:
│       │   ├── `plugins` (e.g., android application, kotlin-android)
│       │   ├── `android` (compileSdk, defaultConfig, buildTypes, compileOptions, buildFeatures like viewBinding)
│       │   └── `dependencies` (appcompat, material, constraintlayout, core-ktx, PDF generation library like iText - যদি যোগ করা হয়, etc.)
│       └── How it Works: Gradle বিল্ড সিস্টেম এই ফাইল ব্যবহার করে অ্যাপ কম্পাইল এবং প্যাকেজ করে।
│
├── 📁 gradle (Gradle Wrapper files)
└── 📄 build.gradle (Project-level) বা build.gradle.kts
    └── Purpose: সম্পূর্ণ প্রজেক্টের জন্য গ্লোবাল বিল্ড কনফিগারেশন এবং রিপোজিটরি ডিফাইন করে।
```

**মূল ফাংশন এবং তাদের কাজ (উদাহরণ `MainActivity.kt` থেকে):**

*   **`onCreate(savedInstanceState: Bundle?)`:**
    *   Activity তৈরি হওয়ার সময় প্রথম কল হয়।
    *   ViewBinding ব্যবহার করে লেআউট ইনফ্লেট করে (`ActivityMainBinding.inflate`)।
    *   `setContentView(binding.root)` দিয়ে UI সেট করে।
    *   `setSupportActionBar(binding.toolbar)` দিয়ে Toolbar সেট করে।
    *   `setupTaxpayerCategorySpinner()` কল করে Spinner পপুলেট করে।
    *   `setupButtonClickListeners()` কল করে বাটন লিসেনার সেট করে।

*   **`onCreateOptionsMenu(menu: Menu?)` / `onOptionsItemSelected(item: MenuItem)`:**
    *   Toolbar-এ Options Menu তৈরি এবং তার আইটেম ক্লিক হ্যান্ডেল করে (যেমন Developer Info পেজে যাওয়া)।

*   **`setupTaxpayerCategorySpinner()`:**
    *   `strings.xml`-এর `taxpayer_categories` array থেকে ডেটা নিয়ে Spinner-এ আইটেম যোগ করে।

*   **`setupButtonClickListeners()`:**
    *   "Calculate Tax", "Year", "Generate PDF" বাটনগুলোর জন্য `setOnClickListener` সেট করে।

*   **`calculateAndDisplayTax()`:**
    *   প্রধান ক্যালকুলেশন ফাংশন।
    *   `getInputAsDouble()` দিয়ে ইনপুট ভ্যালু নেয়।
    *   `getTaxFreeLimit()` কল করে করমুক্ত সীমা বের করে।
    *   `calculateTaxSlabs()` এবং `calculateRebate()` কল করে ট্যাক্স ও রিবেট গণনা করে।
    *   সর্বনিম্ন ট্যাক্স বিবেচনা করে।
    *   `displayResults()` দিয়ে ফলাফল দেখায়।

*   **`getTaxFreeLimit(): Double`:**
    *   Spinner-এ সিলেক্ট করা ক্যাটাগরি অনুযায়ী সঠিক করমুক্ত আয়ের সীমা রিটার্ন করে।

*   **`calculateTaxSlabs(income: Double): Double`:**
    *   দেওয়া আয়ের (করমুক্ত সীমা বাদ দেওয়ার পর) উপর ট্যাক্স স্ল্যাব প্রয়োগ করে মোট ট্যাক্স গণনা করে।

*   **`calculateRebate(taxableIncome: Double, actualInvestment: Double): Double`:**
    *   যোগ্য বিনিয়োগের উপর নির্দিষ্ট হারে রিবেট গণনা করে।

*   **`displayResults(...)`:**
    *   গণনা করা ফলাফল (ট্যাক্সেবল ইনকাম, ট্যাক্স, রিবেট, নেট ট্যাক্স) UI-তে (TextViews) দেখায় এবং Result Card দৃশ্যমান করে।

*   **`getInputAsDouble(...): Double?`:**
    *   `TextInputEditText` থেকে টেক্সট নিয়ে সেটিকে ডাবল নাম্বারে কনভার্ট করে। খালি থাকলে বা ভুল ফরম্যাট হলে এরর দেখায় এবং `null` রিটার্ন করে।

*   **`formatCurrency(value: Double): String`:**
    *   ডাবল ভ্যালুকে BDT কারেন্সি ফরম্যাটে স্ট্রিং হিসেবে দেখায়।

*   **`hideKeyboard(view: View)`:**
    *   সফট কীবোর্ড লুকিয়ে ফেলে।

*   **`generatePdfReport()` / `sharePdf(fileUri: Uri)` (যদি PDF ফিচার থাকে):**
    *   PDF ডকুমেন্ট তৈরি করে, সেভ করে এবং শেয়ার করার জন্য Intent তৈরি করে। `FileProvider` ব্যবহার করে।
