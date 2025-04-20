Okay, let's build a simple Tax Calculator Android app with a modern UI using Java and XML. We'll use Material Components for a contemporary look and feel.

**Project Setup (Android Studio)**

1.  **Create a New Project:**
    *   Open Android Studio.
    *   Click "File" -> "New" -> "New Project...".
    *   Choose the "Empty Views Activity" template.
    *   Click "Next".
    *   Configure your project:
        *   **Name:** Tax Calculator (or your preferred name)
        *   **Package name:** `com.yourcompany.taxcalculator` (replace `yourcompany`)
        *   **Save location:** Choose where to save it.
        *   **Language:** Java
        *   **Minimum SDK:** Choose an appropriate API level (e.g., API 21 or higher for good Material Design support).
    *   Click "Finish". Android Studio will set up the basic project structure.

**Step 1: Add Material Components Dependency**

Ensure your app-level `build.gradle` (the one in the `app` directory, not the root project) includes the Material Components library dependency. It's usually included by default in newer Android Studio versions, but double-check:

```gradle
// In app/build.gradle -> dependencies { ... }
implementation 'com.google.android.material:material:1.12.0' // Use the latest version
```

Sync your project after adding/checking the dependency (File -> Sync Project with Gradle Files).

**Step 2: Define Colors (res/values/colors.xml)**

Let's define some basic colors for our theme.

```xml
<?xml version="1.0" encoding="utf-8"?>
<resources>
    <!-- Base colors matching Material 3 theme -->
    <color name="purple_200">#FFBB86FC</color>
    <color name="purple_500">#FF6200EE</color>
    <color name="purple_700">#FF3700B3</color>
    <color name="teal_200">#FF03DAC5</color>
    <color name="teal_700">#FF018786</color>
    <color name="black">#FF000000</color>
    <color name="white">#FFFFFFFF</color>

    <!-- App Specific Colors -->
    <color name="colorPrimary">@color/purple_500</color>
    <color name="colorPrimaryVariant">@color/purple_700</color>
    <color name="colorOnPrimary">@color/white</color>
    <color name="colorSecondary">@color/teal_200</color>
    <color name="colorSecondaryVariant">@color/teal_700</color>
    <color name="colorOnSecondary">@color/black</color>
    <color name="colorSurface">@color/white</color>
    <color name="colorOnSurface">@color/black</color>
    <color name="colorBackground">#F5F5F5</color> <!-- Light gray background -->
    <color name="colorOnBackground">@color/black</color>
    <color name="colorError">#B00020</color>
    <color name="colorOnError">@color/white</color>
    <color name="textColorPrimary">#DE000000</color> <!-- 87% black -->
    <color name="textColorSecondary">#8A000000</color> <!-- 54% black -->
    <color name="textInputOutlineColor">#8A000000</color>
</resources>
```

**Step 3: Define Strings (res/values/strings.xml)**

Centralize all user-facing text.

```xml
<resources>
    <string name="app_name">Tax Calculator</string>

    <!-- UI Labels and Hints -->
    <string name="enter_amount_hint">Enter Amount ($)</string>
    <string name="enter_tax_rate_hint">Enter Tax Rate (%)</string>
    <string name="calculate_button">Calculate Tax</string>
    <string name="tax_amount_label">Tax Amount:</string>
    <string name="total_amount_label">Total Amount (incl. Tax):</string>
    <string name="initial_result_value">$0.00</string>

    <!-- Error Messages -->
    <string name="error_empty_amount">Please enter an amount</string>
    <string name="error_invalid_amount">Invalid amount entered</string>
    <string name="error_empty_rate">Please enter a tax rate</string>
    <string name="error_invalid_rate">Invalid tax rate entered</string>
    <string name="error_negative_rate">Tax rate cannot be negative</string>

</resources>
```

**Step 4: Update Theme (res/values/themes.xml)**

Make sure your app uses a Material Components theme. Replace the contents of `themes.xml` (and potentially `themes.xml (night)`) with something like this:

```xml
<resources xmlns:tools="http://schemas.android.com/tools">
    <!-- Base application theme. -->
    <style name="Base.Theme.TaxCalculator" parent="Theme.Material3.DayNight.NoActionBar">
        <!-- Primary brand color. -->
        <item name="colorPrimary">@color/colorPrimary</item>
        <item name="colorPrimaryVariant">@color/colorPrimaryVariant</item>
        <item name="colorOnPrimary">@color/colorOnPrimary</item>
        <!-- Secondary brand color. -->
        <item name="colorSecondary">@color/colorSecondary</item>
        <item name="colorSecondaryVariant">@color/colorSecondaryVariant</item>
        <item name="colorOnSecondary">@color/colorOnSecondary</item>
        <!-- Status bar color. -->
        <item name="android:statusBarColor">?attr/colorPrimaryVariant</item>
        <!-- Customize your theme here. -->
        <item name="colorSurface">@color/colorSurface</item>
        <item name="colorOnSurface">@color/colorOnSurface</item>
        <item name="android:colorBackground">@color/colorBackground</item>
        <item name="colorOnBackground">@color/colorOnBackground</item>
        <item name="colorError">@color/colorError</item>
        <item name="colorOnError">@color/colorOnError</item>

        <!-- Set default text colors -->
        <item name="android:textColorPrimary">@color/textColorPrimary</item>
        <item name="android:textColorSecondary">@color/textColorSecondary</item>

        <!-- Style TextInputLayout -->
         <item name="textInputStyle">@style/Widget.MaterialComponents.TextInputLayout.OutlinedBox</item>

        <!-- Style MaterialButton -->
        <item name="materialButtonStyle">@style/Widget.MaterialComponents.Button</item>

    </style>

    <style name="Theme.TaxCalculator" parent="Base.Theme.TaxCalculator" />

    <!-- Optional: Define specific styles if needed -->
    <style name="ResultTextView">
        <item name="android:textSize">18sp</item>
        <item name="android:textColor">@color/textColorPrimary</item>
        <item name="android:layout_marginTop">8dp</item>
    </style>

</resources>
```

*(Make sure to update the `<application>` tag in your `AndroidManifest.xml` to use this theme: `android:theme="@style/Theme.TaxCalculator"`)*

**Step 5: Design the Layout (res/layout/activity_main.xml)**

Use `ConstraintLayout` for flexibility and Material Components (`TextInputLayout`, `TextInputEditText`, `MaterialButton`) for the modern look.

```xml
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:padding="24dp"
    tools:context=".MainActivity">

    <!-- Amount Input Field -->
    <com.google.android.material.textfield.TextInputLayout
        android:id="@+id/textFieldLayoutAmount"
        style="@style/Widget.MaterialComponents.TextInputLayout.OutlinedBox"
        android:layout_width="0dp"
        android:layout_height="wrap_content"
        android:hint="@string/enter_amount_hint"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:boxStrokeColor="@color/colorPrimary"
        app:hintTextColor="@color/colorPrimary"
        app:startIconDrawable="@drawable/ic_money" > <!-- Add an icon (see below) -->

        <com.google.android.material.textfield.TextInputEditText
            android:id="@+id/editTextAmount"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:inputType="numberDecimal"
            android:imeOptions="actionNext" />

    </com.google.android.material.textfield.TextInputLayout>

    <!-- Tax Rate Input Field -->
    <com.google.android.material.textfield.TextInputLayout
        android:id="@+id/textFieldLayoutTaxRate"
        style="@style/Widget.MaterialComponents.TextInputLayout.OutlinedBox"
        android:layout_width="0dp"
        android:layout_height="wrap_content"
        android:layout_marginTop="16dp"
        android:hint="@string/enter_tax_rate_hint"
        app:layout_constraintTop_toBottomOf="@id/textFieldLayoutAmount"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:boxStrokeColor="@color/colorPrimary"
        app:hintTextColor="@color/colorPrimary"
        app:startIconDrawable="@drawable/ic_percent"> <!-- Add an icon (see below) -->


        <com.google.android.material.textfield.TextInputEditText
            android:id="@+id/editTextTaxRate"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:inputType="numberDecimal"
            android:imeOptions="actionDone"/> <!-- Use actionDone for the last input -->

    </com.google.android.material.textfield.TextInputLayout>

    <!-- Calculate Button -->
    <com.google.android.material.button.MaterialButton
        android:id="@+id/buttonCalculate"
        android:layout_width="0dp"
        android:layout_height="wrap_content"
        android:layout_marginTop="24dp"
        android:text="@string/calculate_button"
        android:paddingTop="12dp"
        android:paddingBottom="12dp"
        android:textSize="16sp"
        app:cornerRadius="8dp"
        app:layout_constraintTop_toBottomOf="@id/textFieldLayoutTaxRate"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintEnd_toEndOf="parent" />

    <!-- Results Section -->
    <TextView
        android:id="@+id/textViewTaxAmountLabel"
        style="@style/ResultTextView"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="@string/tax_amount_label"
        android:layout_marginTop="32dp"
        app:layout_constraintTop_toBottomOf="@id/buttonCalculate"
        app:layout_constraintStart_toStartOf="parent" />

    <TextView
        android:id="@+id/textViewTaxAmountResult"
        style="@style/ResultTextView"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="@string/initial_result_value"
        android:textStyle="bold"
        android:layout_marginStart="8dp"
        app:layout_constraintTop_toTopOf="@id/textViewTaxAmountLabel"
        app:layout_constraintBaseline_toBaselineOf="@id/textViewTaxAmountLabel"
        app:layout_constraintStart_toEndOf="@id/textViewTaxAmountLabel"/>

    <TextView
        android:id="@+id/textViewTotalAmountLabel"
        style="@style/ResultTextView"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="@string/total_amount_label"
        android:layout_marginTop="16dp"
        app:layout_constraintTop_toBottomOf="@id/textViewTaxAmountLabel"
        app:layout_constraintStart_toStartOf="parent" />

    <TextView
        android:id="@+id/textViewTotalAmountResult"
        style="@style/ResultTextView"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="@string/initial_result_value"
        android:textStyle="bold"
        android:layout_marginStart="8dp"
        app:layout_constraintTop_toTopOf="@id/textViewTotalAmountLabel"
        app:layout_constraintBaseline_toBaselineOf="@id/textViewTotalAmountLabel"
        app:layout_constraintStart_toEndOf="@id/textViewTotalAmountLabel"/>


</androidx.constraintlayout.widget.ConstraintLayout>
```

**Step 5.1: Add Icons (Optional but Recommended)**

1.  Right-click on the `res/drawable` folder.
2.  Select "New" -> "Vector Asset".
3.  Click on the "Clip Art" icon.
4.  Search for icons like "money" or "attach_money" and "percent" or "percentage".
5.  Choose an icon, customize its name (e.g., `ic_money`, `ic_percent`), color (you can set it to `@color/colorPrimary` or leave it black/grey), and size.
6.  Click "Next" and "Finish". Repeat for the other icon.
7.  These icons are now referenced in the `app:startIconDrawable` attributes in the layout XML.

**Step 6: Implement the Logic (java/your_package_name/MainActivity.java)**

```java
package com.yourcompany.taxcalculator; // Replace with your actual package name

import androidx.appcompat.app.AppCompatActivity;

import android.content.Context;
import android.os.Bundle;
import android.view.View;
import android.view.inputmethod.InputMethodManager;
import android.widget.TextView;
import android.widget.Toast;

import com.google.android.material.button.MaterialButton;
import com.google.android.material.textfield.TextInputEditText;
import com.google.android.material.textfield.TextInputLayout;

import java.text.NumberFormat;
import java.util.Locale;

public class MainActivity extends AppCompatActivity {

    // Declare UI elements
    private TextInputLayout textFieldLayoutAmount;
    private TextInputEditText editTextAmount;
    private TextInputLayout textFieldLayoutTaxRate;
    private TextInputEditText editTextTaxRate;
    private MaterialButton buttonCalculate;
    private TextView textViewTaxAmountResult;
    private TextView textViewTotalAmountResult;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        // Initialize UI elements
        textFieldLayoutAmount = findViewById(R.id.textFieldLayoutAmount);
        editTextAmount = findViewById(R.id.editTextAmount);
        textFieldLayoutTaxRate = findViewById(R.id.textFieldLayoutTaxRate);
        editTextTaxRate = findViewById(R.id.editTextTaxRate);
        buttonCalculate = findViewById(R.id.buttonCalculate);
        textViewTaxAmountResult = findViewById(R.id.textViewTaxAmountResult);
        textViewTotalAmountResult = findViewById(R.id.textViewTotalAmountResult);

        // Set up the button's click listener
        buttonCalculate.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                calculateTax();
                hideKeyboard(v); // Hide keyboard after calculation
            }
        });
    }

    private void calculateTax() {
        // Clear previous errors
        textFieldLayoutAmount.setError(null);
        textFieldLayoutTaxRate.setError(null);

        String amountStr = editTextAmount.getText().toString();
        String rateStr = editTextTaxRate.getText().toString();

        // --- Input Validation ---
        if (amountStr.isEmpty()) {
            textFieldLayoutAmount.setError(getString(R.string.error_empty_amount));
            return;
        }
        if (rateStr.isEmpty()) {
            textFieldLayoutTaxRate.setError(getString(R.string.error_empty_rate));
            return;
        }

        double amount;
        double ratePercent;

        try {
            amount = Double.parseDouble(amountStr);
        } catch (NumberFormatException e) {
            textFieldLayoutAmount.setError(getString(R.string.error_invalid_amount));
            return;
        }

        try {
            ratePercent = Double.parseDouble(rateStr);
        } catch (NumberFormatException e) {
            textFieldLayoutTaxRate.setError(getString(R.string.error_invalid_rate));
            return;
        }

        if (ratePercent < 0) {
             textFieldLayoutTaxRate.setError(getString(R.string.error_negative_rate));
             return;
        }

        // --- Calculation ---
        double taxAmount = amount * (ratePercent / 100.0);
        double totalAmount = amount + taxAmount;

        // --- Formatting Output ---
        // Use NumberFormat for currency formatting based on locale
        NumberFormat currencyFormatter = NumberFormat.getCurrencyInstance(Locale.getDefault());
        // Alternatively, force US Dollars: NumberFormat currencyFormatter = NumberFormat.getCurrencyInstance(Locale.US);

        // --- Display Results ---
        textViewTaxAmountResult.setText(currencyFormatter.format(taxAmount));
        textViewTotalAmountResult.setText(currencyFormatter.format(totalAmount));
    }

    // Helper method to hide the keyboard
    private void hideKeyboard(View view) {
        InputMethodManager imm = (InputMethodManager) getSystemService(Context.INPUT_METHOD_SERVICE);
        if (imm != null && view != null) {
            imm.hideSoftInputFromWindow(view.getWindowToken(), 0);
        }
        // Clear focus to prevent keyboard popping up again on text view tap
        View currentFocus = getCurrentFocus();
        if (currentFocus != null) {
            currentFocus.clearFocus();
        }
    }
}
```

**Explanation:**

1.  **XML Layout (`activity_main.xml`):**
    *   Uses `ConstraintLayout` to position elements relative to each other.
    *   Uses `TextInputLayout` and `TextInputEditText` for Material Design input fields. `TextInputLayout` provides the floating label, hint, error display, and outlined box style.
    *   Uses `MaterialButton` for a styled button.
    *   Uses standard `TextView`s to display the results, styled slightly via the theme/styles.
    *   `android:inputType="numberDecimal"` allows users to enter numbers with decimals.
    *   `android:imeOptions` control the action button on the keyboard (e.g., "Next", "Done").
    *   `app:startIconDrawable` adds helpful icons to the input fields.
    *   Padding and margins create spacing.

2.  **Java Logic (`MainActivity.java`):**
    *   **`onCreate`**: Initializes UI elements using `findViewById` and sets the `OnClickListener` for the button.
    *   **`calculateTax`**:
        *   Gets the text from the input fields.
        *   **Validation**: Checks if fields are empty or contain invalid numbers using `try-catch` for `NumberFormatException`. Uses `setError` on the `TextInputLayout` to display error messages directly with the field. Also checks for negative tax rates.
        *   **Calculation**: Performs the simple tax calculation. Uses `100.0` to ensure floating-point division.
        *   **Formatting**: Uses `NumberFormat.getCurrencyInstance()` to format the output nicely as currency according to the user's device locale.
        *   **Display**: Sets the calculated and formatted values to the result `TextView`s.
    *   **`hideKeyboard`**: A utility function to dismiss the soft keyboard after the calculation for better UX.

**Run the App**

Connect a device or start an emulator and run the app from Android Studio (Shift+F10 or the Run button). You should see your modern-looking Tax Calculator!Okay, let's build a simple Tax Calculator Android app with a modern UI using Java and XML. We'll use Material Components for a contemporary look and feel.

**Project Setup (Android Studio)**

1.  **Create a New Project:**
    *   Open Android Studio.
    *   Click "File" -> "New" -> "New Project...".
    *   Choose the "Empty Views Activity" template.
    *   Click "Next".
    *   Configure your project:
        *   **Name:** Tax Calculator (or your preferred name)
        *   **Package name:** `com.yourcompany.taxcalculator` (replace `yourcompany`)
        *   **Save location:** Choose where to save it.
        *   **Language:** Java
        *   **Minimum SDK:** Choose an appropriate API level (e.g., API 21 or higher for good Material Design support).
    *   Click "Finish". Android Studio will set up the basic project structure.

**Step 1: Add Material Components Dependency**

Ensure your app-level `build.gradle` (the one in the `app` directory, not the root project) includes the Material Components library dependency. It's usually included by default in newer Android Studio versions, but double-check:

```gradle
// In app/build.gradle -> dependencies { ... }
implementation 'com.google.android.material:material:1.12.0' // Use the latest version
```

Sync your project after adding/checking the dependency (File -> Sync Project with Gradle Files).

**Step 2: Define Colors (res/values/colors.xml)**

Let's define some basic colors for our theme.

```xml
<?xml version="1.0" encoding="utf-8"?>
<resources>
    <!-- Base colors matching Material 3 theme -->
    <color name="purple_200">#FFBB86FC</color>
    <color name="purple_500">#FF6200EE</color>
    <color name="purple_700">#FF3700B3</color>
    <color name="teal_200">#FF03DAC5</color>
    <color name="teal_700">#FF018786</color>
    <color name="black">#FF000000</color>
    <color name="white">#FFFFFFFF</color>

    <!-- App Specific Colors -->
    <color name="colorPrimary">@color/purple_500</color>
    <color name="colorPrimaryVariant">@color/purple_700</color>
    <color name="colorOnPrimary">@color/white</color>
    <color name="colorSecondary">@color/teal_200</color>
    <color name="colorSecondaryVariant">@color/teal_700</color>
    <color name="colorOnSecondary">@color/black</color>
    <color name="colorSurface">@color/white</color>
    <color name="colorOnSurface">@color/black</color>
    <color name="colorBackground">#F5F5F5</color> <!-- Light gray background -->
    <color name="colorOnBackground">@color/black</color>
    <color name="colorError">#B00020</color>
    <color name="colorOnError">@color/white</color>
    <color name="textColorPrimary">#DE000000</color> <!-- 87% black -->
    <color name="textColorSecondary">#8A000000</color> <!-- 54% black -->
    <color name="textInputOutlineColor">#8A000000</color>
</resources>
```

**Step 3: Define Strings (res/values/strings.xml)**

Centralize all user-facing text.

```xml
<resources>
    <string name="app_name">Tax Calculator</string>

    <!-- UI Labels and Hints -->
    <string name="enter_amount_hint">Enter Amount ($)</string>
    <string name="enter_tax_rate_hint">Enter Tax Rate (%)</string>
    <string name="calculate_button">Calculate Tax</string>
    <string name="tax_amount_label">Tax Amount:</string>
    <string name="total_amount_label">Total Amount (incl. Tax):</string>
    <string name="initial_result_value">$0.00</string>

    <!-- Error Messages -->
    <string name="error_empty_amount">Please enter an amount</string>
    <string name="error_invalid_amount">Invalid amount entered</string>
    <string name="error_empty_rate">Please enter a tax rate</string>
    <string name="error_invalid_rate">Invalid tax rate entered</string>
    <string name="error_negative_rate">Tax rate cannot be negative</string>

</resources>
```

**Step 4: Update Theme (res/values/themes.xml)**

Make sure your app uses a Material Components theme. Replace the contents of `themes.xml` (and potentially `themes.xml (night)`) with something like this:

```xml
<resources xmlns:tools="http://schemas.android.com/tools">
    <!-- Base application theme. -->
    <style name="Base.Theme.TaxCalculator" parent="Theme.Material3.DayNight.NoActionBar">
        <!-- Primary brand color. -->
        <item name="colorPrimary">@color/colorPrimary</item>
        <item name="colorPrimaryVariant">@color/colorPrimaryVariant</item>
        <item name="colorOnPrimary">@color/colorOnPrimary</item>
        <!-- Secondary brand color. -->
        <item name="colorSecondary">@color/colorSecondary</item>
        <item name="colorSecondaryVariant">@color/colorSecondaryVariant</item>
        <item name="colorOnSecondary">@color/colorOnSecondary</item>
        <!-- Status bar color. -->
        <item name="android:statusBarColor">?attr/colorPrimaryVariant</item>
        <!-- Customize your theme here. -->
        <item name="colorSurface">@color/colorSurface</item>
        <item name="colorOnSurface">@color/colorOnSurface</item>
        <item name="android:colorBackground">@color/colorBackground</item>
        <item name="colorOnBackground">@color/colorOnBackground</item>
        <item name="colorError">@color/colorError</item>
        <item name="colorOnError">@color/colorOnError</item>

        <!-- Set default text colors -->
        <item name="android:textColorPrimary">@color/textColorPrimary</item>
        <item name="android:textColorSecondary">@color/textColorSecondary</item>

        <!-- Style TextInputLayout -->
         <item name="textInputStyle">@style/Widget.MaterialComponents.TextInputLayout.OutlinedBox</item>

        <!-- Style MaterialButton -->
        <item name="materialButtonStyle">@style/Widget.MaterialComponents.Button</item>

    </style>

    <style name="Theme.TaxCalculator" parent="Base.Theme.TaxCalculator" />

    <!-- Optional: Define specific styles if needed -->
    <style name="ResultTextView">
        <item name="android:textSize">18sp</item>
        <item name="android:textColor">@color/textColorPrimary</item>
        <item name="android:layout_marginTop">8dp</item>
    </style>

</resources>
```

*(Make sure to update the `<application>` tag in your `AndroidManifest.xml` to use this theme: `android:theme="@style/Theme.TaxCalculator"`)*

**Step 5: Design the Layout (res/layout/activity_main.xml)**

Use `ConstraintLayout` for flexibility and Material Components (`TextInputLayout`, `TextInputEditText`, `MaterialButton`) for the modern look.

```xml
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:padding="24dp"
    tools:context=".MainActivity">

    <!-- Amount Input Field -->
    <com.google.android.material.textfield.TextInputLayout
        android:id="@+id/textFieldLayoutAmount"
        style="@style/Widget.MaterialComponents.TextInputLayout.OutlinedBox"
        android:layout_width="0dp"
        android:layout_height="wrap_content"
        android:hint="@string/enter_amount_hint"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:boxStrokeColor="@color/colorPrimary"
        app:hintTextColor="@color/colorPrimary"
        app:startIconDrawable="@drawable/ic_money" > <!-- Add an icon (see below) -->

        <com.google.android.material.textfield.TextInputEditText
            android:id="@+id/editTextAmount"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:inputType="numberDecimal"
            android:imeOptions="actionNext" />

    </com.google.android.material.textfield.TextInputLayout>

    <!-- Tax Rate Input Field -->
    <com.google.android.material.textfield.TextInputLayout
        android:id="@+id/textFieldLayoutTaxRate"
        style="@style/Widget.MaterialComponents.TextInputLayout.OutlinedBox"
        android:layout_width="0dp"
        android:layout_height="wrap_content"
        android:layout_marginTop="16dp"
        android:hint="@string/enter_tax_rate_hint"
        app:layout_constraintTop_toBottomOf="@id/textFieldLayoutAmount"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:boxStrokeColor="@color/colorPrimary"
        app:hintTextColor="@color/colorPrimary"
        app:startIconDrawable="@drawable/ic_percent"> <!-- Add an icon (see below) -->


        <com.google.android.material.textfield.TextInputEditText
            android:id="@+id/editTextTaxRate"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:inputType="numberDecimal"
            android:imeOptions="actionDone"/> <!-- Use actionDone for the last input -->

    </com.google.android.material.textfield.TextInputLayout>

    <!-- Calculate Button -->
    <com.google.android.material.button.MaterialButton
        android:id="@+id/buttonCalculate"
        android:layout_width="0dp"
        android:layout_height="wrap_content"
        android:layout_marginTop="24dp"
        android:text="@string/calculate_button"
        android:paddingTop="12dp"
        android:paddingBottom="12dp"
        android:textSize="16sp"
        app:cornerRadius="8dp"
        app:layout_constraintTop_toBottomOf="@id/textFieldLayoutTaxRate"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintEnd_toEndOf="parent" />

    <!-- Results Section -->
    <TextView
        android:id="@+id/textViewTaxAmountLabel"
        style="@style/ResultTextView"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="@string/tax_amount_label"
        android:layout_marginTop="32dp"
        app:layout_constraintTop_toBottomOf="@id/buttonCalculate"
        app:layout_constraintStart_toStartOf="parent" />

    <TextView
        android:id="@+id/textViewTaxAmountResult"
        style="@style/ResultTextView"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="@string/initial_result_value"
        android:textStyle="bold"
        android:layout_marginStart="8dp"
        app:layout_constraintTop_toTopOf="@id/textViewTaxAmountLabel"
        app:layout_constraintBaseline_toBaselineOf="@id/textViewTaxAmountLabel"
        app:layout_constraintStart_toEndOf="@id/textViewTaxAmountLabel"/>

    <TextView
        android:id="@+id/textViewTotalAmountLabel"
        style="@style/ResultTextView"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="@string/total_amount_label"
        android:layout_marginTop="16dp"
        app:layout_constraintTop_toBottomOf="@id/textViewTaxAmountLabel"
        app:layout_constraintStart_toStartOf="parent" />

    <TextView
        android:id="@+id/textViewTotalAmountResult"
        style="@style/ResultTextView"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="@string/initial_result_value"
        android:textStyle="bold"
        android:layout_marginStart="8dp"
        app:layout_constraintTop_toTopOf="@id/textViewTotalAmountLabel"
        app:layout_constraintBaseline_toBaselineOf="@id/textViewTotalAmountLabel"
        app:layout_constraintStart_toEndOf="@id/textViewTotalAmountLabel"/>


</androidx.constraintlayout.widget.ConstraintLayout>
```

**Step 5.1: Add Icons (Optional but Recommended)**

1.  Right-click on the `res/drawable` folder.
2.  Select "New" -> "Vector Asset".
3.  Click on the "Clip Art" icon.
4.  Search for icons like "money" or "attach_money" and "percent" or "percentage".
5.  Choose an icon, customize its name (e.g., `ic_money`, `ic_percent`), color (you can set it to `@color/colorPrimary` or leave it black/grey), and size.
6.  Click "Next" and "Finish". Repeat for the other icon.
7.  These icons are now referenced in the `app:startIconDrawable` attributes in the layout XML.

**Step 6: Implement the Logic (java/your_package_name/MainActivity.java)**

```java
package com.yourcompany.taxcalculator; // Replace with your actual package name

import androidx.appcompat.app.AppCompatActivity;

import android.content.Context;
import android.os.Bundle;
import android.view.View;
import android.view.inputmethod.InputMethodManager;
import android.widget.TextView;
import android.widget.Toast;

import com.google.android.material.button.MaterialButton;
import com.google.android.material.textfield.TextInputEditText;
import com.google.android.material.textfield.TextInputLayout;

import java.text.NumberFormat;
import java.util.Locale;

public class MainActivity extends AppCompatActivity {

    // Declare UI elements
    private TextInputLayout textFieldLayoutAmount;
    private TextInputEditText editTextAmount;
    private TextInputLayout textFieldLayoutTaxRate;
    private TextInputEditText editTextTaxRate;
    private MaterialButton buttonCalculate;
    private TextView textViewTaxAmountResult;
    private TextView textViewTotalAmountResult;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        // Initialize UI elements
        textFieldLayoutAmount = findViewById(R.id.textFieldLayoutAmount);
        editTextAmount = findViewById(R.id.editTextAmount);
        textFieldLayoutTaxRate = findViewById(R.id.textFieldLayoutTaxRate);
        editTextTaxRate = findViewById(R.id.editTextTaxRate);
        buttonCalculate = findViewById(R.id.buttonCalculate);
        textViewTaxAmountResult = findViewById(R.id.textViewTaxAmountResult);
        textViewTotalAmountResult = findViewById(R.id.textViewTotalAmountResult);

        // Set up the button's click listener
        buttonCalculate.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                calculateTax();
                hideKeyboard(v); // Hide keyboard after calculation
            }
        });
    }

    private void calculateTax() {
        // Clear previous errors
        textFieldLayoutAmount.setError(null);
        textFieldLayoutTaxRate.setError(null);

        String amountStr = editTextAmount.getText().toString();
        String rateStr = editTextTaxRate.getText().toString();

        // --- Input Validation ---
        if (amountStr.isEmpty()) {
            textFieldLayoutAmount.setError(getString(R.string.error_empty_amount));
            return;
        }
        if (rateStr.isEmpty()) {
            textFieldLayoutTaxRate.setError(getString(R.string.error_empty_rate));
            return;
        }

        double amount;
        double ratePercent;

        try {
            amount = Double.parseDouble(amountStr);
        } catch (NumberFormatException e) {
            textFieldLayoutAmount.setError(getString(R.string.error_invalid_amount));
            return;
        }

        try {
            ratePercent = Double.parseDouble(rateStr);
        } catch (NumberFormatException e) {
            textFieldLayoutTaxRate.setError(getString(R.string.error_invalid_rate));
            return;
        }

        if (ratePercent < 0) {
             textFieldLayoutTaxRate.setError(getString(R.string.error_negative_rate));
             return;
        }

        // --- Calculation ---
        double taxAmount = amount * (ratePercent / 100.0);
        double totalAmount = amount + taxAmount;

        // --- Formatting Output ---
        // Use NumberFormat for currency formatting based on locale
        NumberFormat currencyFormatter = NumberFormat.getCurrencyInstance(Locale.getDefault());
        // Alternatively, force US Dollars: NumberFormat currencyFormatter = NumberFormat.getCurrencyInstance(Locale.US);

        // --- Display Results ---
        textViewTaxAmountResult.setText(currencyFormatter.format(taxAmount));
        textViewTotalAmountResult.setText(currencyFormatter.format(totalAmount));
    }

    // Helper method to hide the keyboard
    private void hideKeyboard(View view) {
        InputMethodManager imm = (InputMethodManager) getSystemService(Context.INPUT_METHOD_SERVICE);
        if (imm != null && view != null) {
            imm.hideSoftInputFromWindow(view.getWindowToken(), 0);
        }
        // Clear focus to prevent keyboard popping up again on text view tap
        View currentFocus = getCurrentFocus();
        if (currentFocus != null) {
            currentFocus.clearFocus();
        }
    }
}
```

**Explanation:**

1.  **XML Layout (`activity_main.xml`):**
    *   Uses `ConstraintLayout` to position elements relative to each other.
    *   Uses `TextInputLayout` and `TextInputEditText` for Material Design input fields. `TextInputLayout` provides the floating label, hint, error display, and outlined box style.
    *   Uses `MaterialButton` for a styled button.
    *   Uses standard `TextView`s to display the results, styled slightly via the theme/styles.
    *   `android:inputType="numberDecimal"` allows users to enter numbers with decimals.
    *   `android:imeOptions` control the action button on the keyboard (e.g., "Next", "Done").
    *   `app:startIconDrawable` adds helpful icons to the input fields.
    *   Padding and margins create spacing.

2.  **Java Logic (`MainActivity.java`):**
    *   **`onCreate`**: Initializes UI elements using `findViewById` and sets the `OnClickListener` for the button.
    *   **`calculateTax`**:
        *   Gets the text from the input fields.
        *   **Validation**: Checks if fields are empty or contain invalid numbers using `try-catch` for `NumberFormatException`. Uses `setError` on the `TextInputLayout` to display error messages directly with the field. Also checks for negative tax rates.
        *   **Calculation**: Performs the simple tax calculation. Uses `100.0` to ensure floating-point division.
        *   **Formatting**: Uses `NumberFormat.getCurrencyInstance()` to format the output nicely as currency according to the user's device locale.
        *   **Display**: Sets the calculated and formatted values to the result `TextView`s.
    *   **`hideKeyboard`**: A utility function to dismiss the soft keyboard after the calculation for better UX.

**Run the App**

Connect a device or start an emulator and run the app from Android Studio (Shift+F10 or the Run button). You should see your modern-looking Tax Calculator!
