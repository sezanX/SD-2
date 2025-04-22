ঠিক আছে। ব্যবহারকারীর অনুরোধ অনুযায়ী, আমরা "Registration Fee" কার্ড বাদ দেব এবং "Percentage Tax" কার্ডটিকে আয়কর স্ল্যাব দেখানোর জন্য পরিবর্তন করবো।

**করণীয়:**

1.  **`res/layout/item_tax_quarter.xml` ফাইলটি ডিলিট করুন:**
    *   প্রজেক্ট উইন্ডোতে `res/layout` ফোল্ডারে যান।
    *   `item_tax_quarter.xml` ফাইলটির উপর রাইট-ক্লিক করে `Delete` সিলেক্ট করুন এবং কনফার্ম করুন।

2.  **নিচের ফাইলগুলোর সম্পূর্ণ কনটেন্ট ডিলিট করুন:**
    *   `res/values/strings.xml`
    *   `res/layout/activity_main.xml`
    *   `MainActivity.kt` (আপনার প্যাকেজের ভিতরে থাকা ফাইলটি)

3.  **`res/values/styles.xml` ফাইলটি খুলুন** এবং বিদ্যমান কনটেন্ট ডিলিট না করে নতুন স্টাইল যোগ করুন (অথবা যদি চান, এই ফাইলটিও ডিলিট করে নিচের সম্পূর্ণ কোড পেস্ট করতে পারেন)।

---

**ফাইল ১: `res/values/strings.xml` (সম্পূর্ণ আপডেট)**

```xml
<resources>
    <!-- App Info -->
    <string name="app_name">Tax Calculator BD</string>

    <!-- Toolbar -->
    <string name="tax_index_title">Tax Index</string>
    <string name="default_year">2024</string> <!-- পরে পরিবর্তন করা যেতে পারে -->

    <!-- Input Card -->
    <string name="income_details">Income Details</string>
    <string name="basic_salary_annual">Basic Salary (Annual)</string>
    <string name="bonus_annual">Bonus (Annual)</string>
    <string name="other_income_annual">Other Taxable Income (Annual)</string>
    <string name="investment_details">Investment for Rebate</string>
    <string name="investment_amount">Total Eligible Investment</string>
    <string name="hint_enter_amount">Enter Amount (BDT)</string>
    <string name="calculate_tax">Calculate Tax</string>

    <!-- Results Card -->
    <string name="tax_summary">Tax Summary</string>
    <string name="gross_taxable_income">Gross Taxable Income:</string> <!-- পরিবর্তন করা হয়েছে -->
    <string name="tax_payable_before_rebate">Tax Payable (Before Rebate):</string>
    <string name="investment_rebate">Investment Rebate:</string>
    <string name="net_tax_payable">Net Tax Payable:</string>
    <string name="result_placeholder">BDT 0.00</string>
    <string name="generate_pdf">Generate PDF Report</string>

    <!-- Income Tax Slab Display -->
    <string name="income_tax_slabs_title">Income Tax Slabs (AY 2024-25)</string> <!-- Assessment Year অনুযায়ী আপডেট করুন -->
    <string name="income_range_header">Income Range (BDT)</string>
    <string name="tax_rate_header">Tax Rate</string>
    <!-- **** নিচের স্ল্যাব এবং টাকার পরিমাণ অবশ্যই NBR সার্কুলার অনুযায়ী যাচাই করুন **** -->
    <string name="slab_1_range">Up to 350,000</string>
    <string name="slab_1_rate">0%</string>
    <string name="slab_2_range">Next 100,000</string>
    <string name="slab_2_rate">5%</string>
    <string name="slab_3_range">Next 400,000</string> <!-- NBR নিয়ম অনুযায়ী চেক করুন -->
    <string name="slab_3_rate">10%</string>
    <string name="slab_4_range">Next 500,000</string> <!-- NBR নিয়ম অনুযায়ী চেক করুন -->
    <string name="slab_4_rate">15%</string>
    <string name="slab_5_range">Next 600,000</string> <!-- NBR নিয়ম অনুযায়ী চেক করুন -->
    <string name="slab_5_rate">20%</string>
    <string name="slab_6_range">On Remaining Amount</string>
    <string name="slab_6_rate">25%</string>
    <string name="note_verify_slabs">Note: Slabs are indicative. Verify with official NBR circulars.</string>
    <string name="note_slabs_general">Note: These slabs apply to general individual taxpayers (male/other). Rules may differ for females, senior citizens, etc.</string>

    <!-- Error Messages -->
    <string name="error_invalid_input">Please enter a valid number</string>
    <string name="error_field_required">This field is required</string>

</resources>
```

---

**ফাইল ২: `res/values/styles.xml` (সম্পূর্ণ আপডেট - আগেরগুলো সহ)**

```xml
<?xml version="1.0" encoding="utf-8"?>
<resources>
    <!-- Text Appearance Styles -->
    <style name="TextAppearance.App.CardTitle" parent="TextAppearance.MaterialComponents.Subtitle1">
         <item name="android:textColor">@color/colorOnSurfacePrimary</item>
         <item name="android:textStyle">bold</item> <!-- Make card titles bold -->
    </style>
    <style name="TextAppearance.App.CardSecondary" parent="TextAppearance.MaterialComponents.Body2">
         <item name="android:textColor">@color/colorOnSurfaceSecondary</item>
    </style>
     <style name="TextAppearance.App.CardTertiary" parent="TextAppearance.MaterialComponents.Caption">
         <item name="android:textColor">@color/colorOnSurfaceTertiary</item>
    </style>

    <style name="TextAppearance.App.StatusFiled" parent="TextAppearance.MaterialComponents.Body2">
         <item name="android:textColor">@color/colorStatusFiled</item>
    </style>
     <style name="TextAppearance.App.StatusPending" parent="TextAppearance.MaterialComponents.Body2">
         <item name="android:textColor">@color/colorStatusPending</item>
    </style>

    <!-- Result Row Styles -->
     <style name="ResultRowLayout">
        <item name="android:layout_width">match_parent</item>
        <item name="android:layout_height">wrap_content</item>
        <item name="android:orientation">horizontal</item>
        <item name="android:paddingTop">6dp</item>
         <item name="android:paddingBottom">6dp</item>
    </style>
     <style name="ResultLabelText" parent="TextAppearance.MaterialComponents.Body1">
        <item name="android:layout_width">0dp</item>
        <item name="android:layout_height">wrap_content</item>
        <item name="android:layout_weight">1</item>
        <item name="android:textColor">@color/colorOnSurfaceSecondary</item>
    </style>
     <style name="ResultValueText" parent="TextAppearance.MaterialComponents.Body1">
        <item name="android:layout_width">wrap_content</item>
        <item name="android:layout_height">wrap_content</item>
        <item name="android:gravity">end</item>
        <item name="android:textColor">@color/colorOnSurfacePrimary</item>
         <item name="android:minWidth">100dp</item> <!-- Helps align values -->
         <item name="android:textStyle">bold</item>
    </style>
    <!-- Style for the final net tax value -->
    <style name="ResultValueText.Final" parent="ResultValueText">
         <item name="android:textStyle">bold</item>
         <item name="android:textAppearance">@style/TextAppearance.MaterialComponents.Subtitle1</item>
    </style>

     <!-- Divider Style -->
     <style name="AppDivider">
        <item name="android:layout_width">match_parent</item>
        <item name="android:layout_height">1dp</item>
        <item name="android:background">@color/divider_color</item>
         <item name="android:layout_marginTop">8dp</item>
         <item name="android:layout_marginBottom">8dp</item>
     </style>

    <!-- Styles for Tax Slab Display (New) -->
    <style name="SlabRowLayout">
        <item name="android:layout_width">match_parent</item>
        <item name="android:layout_height">wrap_content</item>
        <item name="android:orientation">horizontal</item>
        <item name="android:paddingTop">4dp</item>
        <item name="android:paddingBottom">4dp</item>
    </style>

    <style name="SlabRangeText" parent="TextAppearance.App.CardSecondary">
        <item name="android:layout_width">0dp</item>
        <item name="android:layout_weight">2</item> <!-- Give more weight to range text -->
        <item name="android:layout_height">wrap_content</item>
    </style>

    <style name="SlabRateText" parent="TextAppearance.App.CardSecondary">
        <item name="android:layout_width">0dp</item>
        <item name="android:layout_weight">1</item> <!-- Less weight to rate text -->
        <item name="android:layout_height">wrap_content</item>
        <item name="android:gravity">end</item> <!-- Align rate to the right -->
        <item name="android:textStyle">bold</item>
    </style>

</resources>
```

---

**ফাইল ৩: `res/layout/activity_main.xml` (সম্পূর্ণ আপডেট)**

```xml
<?xml version="1.0" encoding="utf-8"?>
<androidx.coordinatorlayout.widget.CoordinatorLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:background="@color/colorBackground"
    tools:context=".MainActivity">

    <!-- AppBar contains the Toolbar -->
    <com.google.android.material.appbar.AppBarLayout
        android:id="@+id/appBarLayout"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:background="@android:color/transparent"
        app:elevation="0dp">

        <com.google.android.material.appbar.MaterialToolbar
            android:id="@+id/toolbar"
            style="@style/Widget.App.Toolbar"
            android:layout_width="match_parent"
            android:layout_height="?attr/actionBarSize">

            <!-- Use ConstraintLayout inside Toolbar for positioning -->
            <androidx.constraintlayout.widget.ConstraintLayout
                android:layout_width="match_parent"
                android:layout_height="match_parent">

                <TextView
                    android:id="@+id/toolbar_title"
                    android:layout_width="wrap_content"
                    android:layout_height="wrap_content"
                    android:text="@string/tax_index_title"
                    android:textAppearance="@style/TextAppearance.MaterialComponents.Headline6"
                    android:textColor="@color/colorOnSurfacePrimary"
                    app:layout_constraintTop_toTopOf="parent"
                    app:layout_constraintBottom_toBottomOf="parent"
                    app:layout_constraintStart_toStartOf="parent"/>

                <com.google.android.material.button.MaterialButton
                    android:id="@+id/buttonYear"
                    style="@style/Widget.App.YearButton"
                    android:layout_width="wrap_content"
                    android:layout_height="wrap_content"
                    android:layout_marginEnd="16dp"
                    android:text="@string/default_year"
                    app:layout_constraintTop_toTopOf="parent"
                    app:layout_constraintBottom_toBottomOf="parent"
                    app:layout_constraintEnd_toEndOf="parent"/>

            </androidx.constraintlayout.widget.ConstraintLayout>

        </com.google.android.material.appbar.MaterialToolbar>

    </com.google.android.material.appbar.AppBarLayout>

    <!-- Scrollable Content Area -->
    <androidx.core.widget.NestedScrollView
        android:id="@+id/nestedScrollView"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        app:layout_behavior="@string/appbar_scrolling_view_behavior">

        <!-- Linear Layout to stack cards vertically -->
        <LinearLayout
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:orientation="vertical"
            android:paddingStart="16dp"
            android:paddingEnd="16dp"
            android:paddingTop="16dp"
            android:paddingBottom="16dp"
            android:clipToPadding="false">

            <!-- Input Section Card -->
            <com.google.android.material.card.MaterialCardView
                android:id="@+id/cardInput"
                style="@style/Widget.App.CardView"
                android:layout_width="match_parent"
                android:layout_height="wrap_content"
                android:layout_marginBottom="16dp">

                <LinearLayout
                    android:layout_width="match_parent"
                    android:layout_height="wrap_content"
                    android:orientation="vertical"
                    android:padding="16dp">

                    <TextView
                        android:layout_width="wrap_content"
                        android:layout_height="wrap_content"
                        android:text="@string/income_details"
                        android:textAppearance="@style/TextAppearance.App.CardTitle"
                        android:layout_marginBottom="16dp"/>

                    <!-- Basic Salary Input -->
                    <com.google.android.material.textfield.TextInputLayout
                        android:id="@+id/layoutBasicSalary"
                        style="@style/Widget.App.TextInputLayout"
                        android:layout_width="match_parent"
                        android:layout_height="wrap_content"
                        android:hint="@string/basic_salary_annual"
                        android:layout_marginBottom="12dp">
                        <com.google.android.material.textfield.TextInputEditText
                            android:id="@+id/editBasicSalary"
                            android:layout_width="match_parent"
                            android:layout_height="wrap_content"
                            android:inputType="numberDecimal"
                            android:imeOptions="actionNext"/>
                    </com.google.android.material.textfield.TextInputLayout>

                     <!-- Bonus Input -->
                     <com.google.android.material.textfield.TextInputLayout
                        android:id="@+id/layoutBonus"
                         style="@style/Widget.App.TextInputLayout"
                        android:layout_width="match_parent"
                        android:layout_height="wrap_content"
                        android:hint="@string/bonus_annual"
                        android:layout_marginBottom="12dp">
                        <com.google.android.material.textfield.TextInputEditText
                            android:id="@+id/editBonus"
                            android:layout_width="match_parent"
                            android:layout_height="wrap_content"
                            android:inputType="numberDecimal"
                            android:imeOptions="actionNext"/>
                    </com.google.android.material.textfield.TextInputLayout>

                    <!-- Other Income Input -->
                    <com.google.android.material.textfield.TextInputLayout
                        android:id="@+id/layoutOtherIncome"
                        style="@style/Widget.App.TextInputLayout"
                        android:layout_width="match_parent"
                        android:layout_height="wrap_content"
                        android:hint="@string/other_income_annual"
                        android:layout_marginBottom="16dp">
                        <com.google.android.material.textfield.TextInputEditText
                            android:id="@+id/editOtherIncome"
                            android:layout_width="match_parent"
                            android:layout_height="wrap_content"
                            android:inputType="numberDecimal"
                            android:imeOptions="actionNext"/>
                    </com.google.android.material.textfield.TextInputLayout>

                    <!-- Investment Section Title -->
                    <TextView
                        android:layout_width="wrap_content"
                        android:layout_height="wrap_content"
                        android:text="@string/investment_details"
                        android:textAppearance="@style/TextAppearance.App.CardTitle"
                        android:layout_marginBottom="16dp"/>

                    <!-- Investment Input -->
                     <com.google.android.material.textfield.TextInputLayout
                        android:id="@+id/layoutInvestment"
                        style="@style/Widget.App.TextInputLayout"
                        android:layout_width="match_parent"
                        android:layout_height="wrap_content"
                        android:hint="@string/investment_amount"
                        android:layout_marginBottom="16dp">
                        <com.google.android.material.textfield.TextInputEditText
                            android:id="@+id/editInvestment"
                            android:layout_width="match_parent"
                            android:layout_height="wrap_content"
                            android:inputType="numberDecimal"
                            android:imeOptions="actionDone"/> <!-- Action Done for last field -->
                    </com.google.android.material.textfield.TextInputLayout>

                    <!-- Calculate Button -->
                    <com.google.android.material.button.MaterialButton
                        android:id="@+id/buttonCalculate"
                        style="@style/Widget.App.Button"
                        android:layout_width="match_parent"
                        android:layout_height="wrap_content"
                        android:layout_marginTop="8dp"
                        android:text="@string/calculate_tax"/>

                </LinearLayout>

            </com.google.android.material.card.MaterialCardView>


            <!-- Results Section Card (Initially Hidden) -->
            <com.google.android.material.card.MaterialCardView
                android:id="@+id/cardResults"
                style="@style/Widget.App.CardView"
                android:layout_width="match_parent"
                android:layout_height="wrap_content"
                android:layout_marginBottom="16dp"
                android:visibility="gone" <!-- Hide initially -->
                tools:visibility="visible"> <!-- Show in preview -->

                <LinearLayout
                    android:layout_width="match_parent"
                    android:layout_height="wrap_content"
                    android:orientation="vertical"
                    android:padding="16dp">

                     <TextView
                        android:layout_width="wrap_content"
                        android:layout_height="wrap_content"
                        android:text="@string/tax_summary"
                        android:textAppearance="@style/TextAppearance.App.CardTitle"
                        android:layout_marginBottom="16dp"/>

                    <!-- Gross Taxable Income Result -->
                    <LinearLayout style="@style/ResultRowLayout">
                        <TextView style="@style/ResultLabelText" android:text="@string/gross_taxable_income"/>
                        <TextView android:id="@+id/textGrossIncomeResult" style="@style/ResultValueText" tools:text="BDT 1,200,000.00"/>
                    </LinearLayout>

                     <!-- Tax Before Rebate Result -->
                     <LinearLayout style="@style/ResultRowLayout">
                        <TextView style="@style/ResultLabelText" android:text="@string/tax_payable_before_rebate"/>
                        <TextView android:id="@+id/textTaxBeforeRebateResult" style="@style/ResultValueText" tools:text="BDT 85,000.00"/>
                    </LinearLayout>

                     <!-- Investment Rebate Result -->
                    <LinearLayout style="@style/ResultRowLayout">
                        <TextView style="@style/ResultLabelText" android:text="@string/investment_rebate"/>
                        <TextView android:id="@+id/textInvestmentRebateResult" style="@style/ResultValueText" tools:text="BDT 15,000.00"/>
                    </LinearLayout>

                    <!-- Divider -->
                    <View style="@style/AppDivider"/>

                    <!-- Net Tax Payable Result -->
                    <LinearLayout style="@style/ResultRowLayout">
                        <TextView style="@style/ResultLabelText" android:text="@string/net_tax_payable"/>
                        <TextView android:id="@+id/textNetTaxPayableResult" style="@style/ResultValueText.Final" tools:text="BDT 70,000.00"/>
                    </LinearLayout>

                     <!-- Generate PDF Button -->
                     <com.google.android.material.button.MaterialButton
                        android:id="@+id/buttonGeneratePdf"
                        style="@style/Widget.App.Button.Outlined"
                        android:layout_width="match_parent"
                        android:layout_height="wrap_content"
                        android:layout_marginTop="24dp"
                        android:text="@string/generate_pdf"/>

                </LinearLayout>
            </com.google.android.material.card.MaterialCardView>


            <!-- Income Tax Slabs Card (Modified from Percentage Tax) -->
            <com.google.android.material.card.MaterialCardView
                android:id="@+id/cardTaxSlabs"
                style="@style/Widget.App.CardView"
                android:layout_width="match_parent"
                android:layout_height="wrap_content"
                android:layout_marginBottom="16dp"> <!-- Margin at the very bottom -->

                 <LinearLayout
                    android:layout_width="match_parent"
                    android:layout_height="wrap_content"
                    android:orientation="vertical"
                    android:padding="16dp">
                    <TextView
                         android:textAppearance="@style/TextAppearance.App.CardTitle"
                        android:layout_width="wrap_content"
                        android:layout_height="wrap_content"
                         android:layout_marginBottom="8dp"
                        android:text="@string/income_tax_slabs_title"/> <!-- Updated Title -->

                    <!-- Tax Slab Display Section -->
                    <LinearLayout
                         android:layout_width="match_parent"
                         android:layout_height="wrap_content"
                         android:orientation="horizontal"
                         android:layout_marginTop="8dp"
                         android:layout_marginBottom="4dp">
                         <TextView
                             style="@style/TextAppearance.App.CardSecondary"
                             android:layout_width="0dp"
                             android:layout_weight="2"
                             android:layout_height="wrap_content"
                             android:textStyle="bold"
                             android:text="@string/income_range_header"/>
                         <TextView
                             style="@style/TextAppearance.App.CardSecondary"
                             android:layout_width="0dp"
                             android:layout_weight="1"
                             android:gravity="end"
                             android:layout_height="wrap_content"
                             android:textStyle="bold"
                             android:text="@string/tax_rate_header"/>
                     </LinearLayout>
                     <View style="@style/AppDivider" android:layout_marginTop="4dp" android:layout_marginBottom="8dp"/>

                     <!-- Slab 1 -->
                     <LinearLayout style="@style/SlabRowLayout">
                         <TextView style="@style/SlabRangeText" android:text="@string/slab_1_range"/>
                         <TextView style="@style/SlabRateText" android:text="@string/slab_1_rate"/>
                     </LinearLayout>
                     <!-- Slab 2 -->
                     <LinearLayout style="@style/SlabRowLayout">
                         <TextView style="@style/SlabRangeText" android:text="@string/slab_2_range"/>
                         <TextView style="@style/SlabRateText" android:text="@string/slab_2_rate"/>
                     </LinearLayout>
                      <!-- Slab 3 -->
                     <LinearLayout style="@style/SlabRowLayout">
                         <TextView style="@style/SlabRangeText" android:text="@string/slab_3_range"/>
                         <TextView style="@style/SlabRateText" android:text="@string/slab_3_rate"/>
                     </LinearLayout>
                      <!-- Slab 4 -->
                     <LinearLayout style="@style/SlabRowLayout">
                         <TextView style="@style/SlabRangeText" android:text="@string/slab_4_range"/>
                         <TextView style="@style/SlabRateText" android:text="@string/slab_4_rate"/>
                     </LinearLayout>
                      <!-- Slab 5 -->
                     <LinearLayout style="@style/SlabRowLayout">
                         <TextView style="@style/SlabRangeText" android:text="@string/slab_5_range"/>
                         <TextView style="@style/SlabRateText" android:text="@string/slab_5_rate"/>
                     </LinearLayout>
                      <!-- Slab 6 -->
                     <LinearLayout style="@style/SlabRowLayout">
                         <TextView style="@style/SlabRangeText" android:text="@string/slab_6_range"/>
                         <TextView style="@style/SlabRateText" android:text="@string/slab_6_rate"/>
                     </LinearLayout>

                    <!-- Optional Notes -->
                     <TextView
                         style="@style/TextAppearance.App.CardTertiary"
                         android:layout_width="match_parent"
                         android:layout_height="wrap_content"
                         android:layout_marginTop="12dp"
                         android:text="@string/note_verify_slabs"/>
                     <TextView
                         style="@style/TextAppearance.App.CardTertiary"
                         android:layout_width="match_parent"
                         android:layout_height="wrap_content"
                         android:layout_marginTop="4dp"
                         android:text="@string/note_slabs_general"/>

                </LinearLayout>
            </com.google.android.material.card.MaterialCardView>

        </LinearLayout>

    </androidx.core.widget.NestedScrollView>

</androidx.coordinatorlayout.widget.CoordinatorLayout>
```

---

**ফাইল ৪: `MainActivity.kt` (সম্পূর্ণ আপডেট)**

```kotlin
package com.sezanx.taxcalculatorbd // <<<--- আপনার সঠিক প্যাকেজ নাম নিশ্চিত করুন

import android.annotation.SuppressLint
import android.content.Context
import android.os.Bundle
import android.view.View
import android.view.inputmethod.InputMethodManager
import android.widget.Toast
import androidx.appcompat.app.AppCompatActivity // AppCompatActivity ব্যবহার করুন
import androidx.core.content.ContextCompat
import com.google.android.material.textfield.TextInputEditText
import com.google.android.material.textfield.TextInputLayout
// জেনারেটেড বাইন্ডিং ক্লাস ইম্পোর্ট করুন
import com.sezanx.taxcalculatorbd.databinding.ActivityMainBinding
// ItemTaxQuarterBinding ইম্পোর্ট এর দরকার নেই কারণ ফাইলটি ডিলিট করা হয়েছে
import java.text.NumberFormat
import java.util.Locale
import java.util.Currency // Currency সেট করার জন্য দরকার

class MainActivity : AppCompatActivity() {

    // বাইন্ডিং ভেরিয়েবল ডিক্লেয়ার করুন
    private lateinit var binding: ActivityMainBinding

    // --- START: Bangladesh Tax Constants (EXAMPLES - MUST BE VERIFIED & UPDATED with NBR Rules!) ---
    // General case (Assumes Male/Other - needs adjustment for Female/Third Gender/Disabled/etc.)
    // Based on common understanding for FY 2023-2024 / Assessment Year 2024-2025
    // **** ATTENTION: THESE ARE ESTIMATES - VERIFY WITH OFFICIAL NBR RULES ****
    private val SLAB1_LIMIT = 350000.0 // Tax Free limit
    private val SLAB2_LIMIT = SLAB1_LIMIT + 100000.0 // Next 100k @ 5%
    private val SLAB3_LIMIT = SLAB2_LIMIT + 400000.0 // Next 400k @ 10% (Check NBR - common source conflict, might be 300k?)
    private val SLAB4_LIMIT = SLAB3_LIMIT + 500000.0 // Next 500k @ 15% (Check NBR)
    private val SLAB5_LIMIT = SLAB4_LIMIT + 600000.0 // Next 600k @ 20% (Check NBR)
    // Remainder above SLAB5_LIMIT @ 25%

    private val SLAB1_RATE = 0.0
    private val SLAB2_RATE = 0.05 // 5%
    private val SLAB3_RATE = 0.10 // 10%
    private val SLAB4_RATE = 0.15 // 15%
    private val SLAB5_RATE = 0.20 // 20%
    private val SLAB6_RATE = 0.25 // 25%

    // Investment Rebate Constants (EXAMPLES - MUST BE VERIFIED & UPDATED with NBR Rules!)
    // NBR rules state rebate = 15% of eligible investment.
    // Eligible investment = Lower of (Actual Investment, 20% of Taxable Income, 1 Crore BDT)
    private val MAX_INVESTMENT_ELIGIBLE_PERCENTAGE = 0.20 // 20% of Total Taxable Income
    private val MAX_INVESTMENT_ELIGIBLE_ABSOLUTE = 10000000.0 // 1 Crore BDT absolute ceiling for eligibility base
    private val REBATE_RATE = 0.15 // 15% on eligible investment

    // Minimum Tax (EXAMPLES - MUST BE VERIFIED based on location: Dhaka/Ctg City Corp, Other City Corp, Other Areas)
    private val MINIMUM_TAX_DHAKA_CTG = 5000.0
    private val MINIMUM_TAX_OTHER_CITY = 4000.0
    private val MINIMUM_TAX_OTHER_AREA = 3000.0
    // --- END: Bangladesh Tax Constants ---


    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)

        // --- ভিউ বাইন্ডিং ব্যবহার করে লেআউট ইনফ্লেট করুন ---
        binding = ActivityMainBinding.inflate(layoutInflater)
        setContentView(binding.root) // বাইন্ডিং রুটকে কনটেন্ট ভিউ হিসেবে সেট করুন
        // --- ভিউ বাইন্ডিং সেটআপ শেষ ---

        setupButtonClickListeners()
        // updateStaticCardsData() ফাংশনটির আর দরকার নেই কারণ স্ট্যাটিক কার্ড বাদ দেওয়া হয়েছে
    }

    // ক্লিক করা যায় এমন এলিমেন্টগুলোর জন্য লিসেনার সেটআপ করুন
    private fun setupButtonClickListeners() {
        // Calculate Button Listener
        binding.buttonCalculate.setOnClickListener { view ->
            hideKeyboard(view)
            calculateAndDisplayTax()
        }

        // Year Button Listener (Placeholder)
        binding.buttonYear.setOnClickListener {
            // TODO: Year Selection Dialog ইমপ্লিমেন্ট করুন
            Toast.makeText(this, "Year selection feature coming soon!", Toast.LENGTH_SHORT).show()
        }

        // Generate PDF Button Listener (Placeholder)
        binding.buttonGeneratePdf.setOnClickListener {
            // TODO: PDF Generation Logic ইমপ্লিমেন্ট করুন
            // TODO: স্টোরেজ পারমিশন হ্যান্ডেল করুন
            Toast.makeText(this, "PDF generation feature coming soon!", Toast.LENGTH_SHORT).show()
        }
    }

    // --- Calculation Logic ---

    private fun calculateAndDisplayTax() {
        // 1. ইনপুট নিন এবং ভ্যালিডেট করুন
        val basicSalary = getInputAsDouble(binding.editBasicSalary, binding.layoutBasicSalary, true) ?: return
        val bonus = getInputAsDouble(binding.editBonus, binding.layoutBonus) ?: return
        val otherIncome = getInputAsDouble(binding.editOtherIncome, binding.layoutOtherIncome) ?: return
        val investment = getInputAsDouble(binding.editInvestment, binding.layoutInvestment) ?: return

        // --- START: Apply Exemptions (খুব সাধারণ উদাহরণ - আসল নিয়ম প্রয়োজন) ---
        // TODO: Basic Salary / Limits অনুযায়ী আসল NBR নিয়ম ইমপ্লিমেন্ট করুন
        val houseRentExemption = (basicSalary * 0.5).coerceAtMost(300000.0)
        val medicalExemption = (basicSalary * 0.1).coerceAtMost(120000.0)
        val conveyanceExemption = 30000.0 // আপাতত প্রযোজ্য ধরা হচ্ছে

        val totalIncomeBeforeExemptions = basicSalary + bonus + otherIncome
        val taxableIncome = (totalIncomeBeforeExemptions - houseRentExemption - medicalExemption - conveyanceExemption).coerceAtLeast(0.0)
        // *** এই এক্সজেম্পশন লজিকটি শুধুমাত্র প্লেসহোল্ডার, সঠিক ইমপ্লিমেন্টেশন দরকার ***


        // 3. Taxable Income এর উপর স্ল্যাব অনুযায়ী ট্যাক্স গণনা করুন
        val taxBeforeRebate = calculateTaxSlabs(taxableIncome)

        // 4. Taxable Income এবং Investment এর উপর ভিত্তি করে Rebate গণনা করুন
        val investmentRebate = calculateRebate(taxableIncome, investment)

        // 5. Minimum tax এর আগে Net Tax Payable গণনা করুন
        var netTaxPayable = (taxBeforeRebate - investmentRebate).coerceAtLeast(0.0)

        // 6. Minimum Tax প্রয়োগ করুন (উদাহরণ)
        // TODO: Minimum tax নির্ধারণের জন্য ব্যবহারকারীর location/status সিলেক্ট করার UI যোগ করুন
        val minimumTax = MINIMUM_TAX_OTHER_AREA // সর্বনিম্ন ডিফল্ট ধরা হচ্ছে
        if (taxableIncome > SLAB1_LIMIT) {
             netTaxPayable = netTaxPayable.coerceAtLeast(minimumTax)
        } else {
             netTaxPayable = 0.0 // করমুক্ত সীমার নিচে আয় হলে ট্যাক্স শূন্য
        }


        // 7. ফলাফল প্রদর্শন করুন
        displayResults(taxableIncome, taxBeforeRebate, investmentRebate, netTaxPayable)
    }

    // ট্যাক্স স্ল্যাব অনুযায়ী ট্যাক্স গণনা (উদাহরণ - অবশ্যই NBR নিয়ম অনুযায়ী যাচাই করুন)
    private fun calculateTaxSlabs(income: Double): Double {
        if (income <= SLAB1_LIMIT) return 0.0
        var tax = 0.0
        var remainingIncome = income - SLAB1_LIMIT

        var taxableInSlab = remainingIncome.coerceAtMost(SLAB2_LIMIT - SLAB1_LIMIT)
        tax += taxableInSlab * SLAB2_RATE
        remainingIncome -= taxableInSlab
        if (remainingIncome <= 0) return tax

        taxableInSlab = remainingIncome.coerceAtMost(SLAB3_LIMIT - SLAB2_LIMIT)
        tax += taxableInSlab * SLAB3_RATE
        remainingIncome -= taxableInSlab
        if (remainingIncome <= 0) return tax

        taxableInSlab = remainingIncome.coerceAtMost(SLAB4_LIMIT - SLAB3_LIMIT)
        tax += taxableInSlab * SLAB4_RATE
        remainingIncome -= taxableInSlab
        if (remainingIncome <= 0) return tax

        taxableInSlab = remainingIncome.coerceAtMost(SLAB5_LIMIT - SLAB4_LIMIT)
        tax += taxableInSlab * SLAB5_RATE
        remainingIncome -= taxableInSlab
        if (remainingIncome <= 0) return tax

        if (remainingIncome > 0) {
            tax += remainingIncome * SLAB6_RATE
        }
        return tax
    }

    // ইনভেস্টমেন্ট রিবেট গণনা (উদাহরণ - অবশ্যই NBR নিয়ম অনুযায়ী যাচাই করুন)
    private fun calculateRebate(taxableIncome: Double, actualInvestment: Double): Double {
        if (taxableIncome <= SLAB1_LIMIT) return 0.0

        val maxEligibleBase = (taxableIncome * MAX_INVESTMENT_ELIGIBLE_PERCENTAGE)
                                .coerceAtMost(MAX_INVESTMENT_ELIGIBLE_ABSOLUTE)
        val investmentForRebateCalc = actualInvestment.coerceAtMost(maxEligibleBase)
        val calculatedRebate = investmentForRebateCalc * REBATE_RATE
        return calculatedRebate
    }


    // --- UI Update & Helpers ---

    // রেজাল্ট কার্ডে গণনা করা ফলাফল প্রদর্শন করুন
    private fun displayResults(taxableIncome: Double, taxBeforeRebate: Double, rebate: Double, netTax: Double) {
        binding.textGrossIncomeResult.text = formatCurrency(taxableIncome) // Taxable Income দেখানো হচ্ছে
        binding.textTaxBeforeRebateResult.text = formatCurrency(taxBeforeRebate)
        binding.textInvestmentRebateResult.text = formatCurrency(rebate)
        binding.textNetTaxPayableResult.text = formatCurrency(netTax)

        binding.cardResults.visibility = View.VISIBLE // রেজাল্ট কার্ড দৃশ্যমান করুন

        // Optional: Scroll down to show results card
        binding.nestedScrollView.post {
             binding.nestedScrollView.smoothScrollTo(0, binding.cardResults.top)
        }
    }

    /**
     * EditText থেকে ইনপুট নিয়ে Double? হিসেবে রিটার্ন করে এবং ভ্যালিডেট করে।
     * ইনভ্যালিড বা আবশ্যক ফিল্ড খালি থাকলে TextInputLayout এ এরর দেখায়।
     */
    private fun getInputAsDouble(editText: TextInputEditText, textInputLayout: TextInputLayout, isRequired: Boolean = false): Double? {
        val inputText = editText.text.toString().trim().replace(",", "") // কমা থাকলে বাদ দিন
        textInputLayout.error = null

        if (inputText.isEmpty()) {
            return if (isRequired) {
                textInputLayout.error = getString(R.string.error_field_required)
                null
            } else {
                0.0
            }
        }
        return try {
            inputText.toDouble()
        } catch (e: NumberFormatException) {
            textInputLayout.error = getString(R.string.error_invalid_input)
            null
        }
    }

    // ডাবল ভ্যালুকে BDT কারেন্সি স্ট্রিং এ ফরম্যাট করে
    private fun formatCurrency(value: Double): String {
        return try {
            val format = NumberFormat.getCurrencyInstance(Locale("bn", "BD")) // বাংলা লোকাল
            // val format = NumberFormat.getCurrencyInstance(Locale("en", "IN")) // বিকল্প
            format.currency = Currency.getInstance("BDT")
            format.maximumFractionDigits = 2
            format.minimumFractionDigits = 2
            format.format(value)
        } catch (e: Exception) {
            System.err.println("Currency formatting error: ${e.message}")
            String.format(Locale.US, "BDT %.2f", value) // ফলব্যাক
        }
    }

    // সফট কীবোর্ড হাইড করে
    private fun hideKeyboard(view: View) {
        val imm = getSystemService(Context.INPUT_METHOD_SERVICE) as? InputMethodManager
        imm?.hideSoftInputFromWindow(view.windowToken, 0)
        currentFocus?.clearFocus()
    }
}
```

---

**এরপর যা করতে হবে:**

1.  নিশ্চিত করুন আপনি `res/layout/item_tax_quarter.xml` ফাইলটি ডিলিট করেছেন।
2.  উপরের ফাইলগুলোর কনটেন্ট সম্পূর্ণরূপে কপি করে আপনার প্রজেক্টের সংশ্লিষ্ট ফাইলগুলোতে পেস্ট করুন (আগের কনটেন্ট ডিলিট করার পর)।
3.  **Build -> Clean Project** করুন।
4.  **Build -> Rebuild Project** করুন।
5.  অ্যাপটি রান করুন।

এখন আপনার অ্যাপে আর Registration Fee কার্ড থাকবে না এবং আগের কোয়ার্টার কার্ডের জায়গায় ইনকাম ট্যাক্স স্ল্যাবের একটি তালিকা দেখাবে।
