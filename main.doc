## Bangladesh Tax Calculator - Android App Documentation

**Version:** 1.0 (Based on development interaction)

**Last Updated:** April 23, 2024

---

### 1. Introduction

The Bangladesh Tax Calculator is an Android application designed to help individual taxpayers in Bangladesh estimate their annual income tax liability based on the rules and regulations set forth by the National Board of Revenue (NBR). The app provides a user-friendly interface to input income details, select taxpayer category, input investment information, and view a calculated tax summary. It also includes features to display current tax slabs, generate a PDF summary report, and view developer information.

**Target Audience:** Individual taxpayers in Bangladesh (Salaried individuals, Professionals, Business owners calculating personal tax).

**Technology Stack:**

*   **Platform:** Android
*   **Language:** Kotlin
*   **UI:** XML Layouts with Material Design Components
*   **Architecture:** Basic Activity-based structure with View Binding
*   **Core Libraries:** AppCompat, Material Components, FileProvider, AndroidX Core

---

### 2. Features

*   **Income Input:** Allows users to input annual Basic Salary, Bonus, and Other Taxable Income.
*   **Taxpayer Category Selection:** Provides a dropdown (Spinner) to select the taxpayer category (General, Female, Senior Citizen, Person with Disability, Third Gender, Freedom Fighter) which affects the tax-free income threshold.
*   **Investment Input:** Allows users to input their total eligible investment amount for tax rebate calculation.
*   **Tax Calculation:** Calculates Gross Taxable Income, Tax Payable before Rebate, Investment Rebate, and Net Tax Payable based on user input and predefined rules (needs verification with NBR circulars).
*   **Tax Slab Display:** Shows the applicable income tax slabs and rates for the selected assessment year (currently displays general structure, dynamically updates the first slab's range based on category).
*   **Tax Summary Display:** Presents the calculated results in a clear, card-based format.
*   **PDF Report Generation & Sharing:** Generates a simple PDF summary of the calculated tax details and allows sharing via standard Android share intents.
*   **Developer Information Page:** Includes a dedicated page with developer details and contact links (Email, GitHub, LinkedIn).
*   **Modern UI:** Utilizes Material Design Components for a clean and intuitive user experience.

---

### 3. Project Structure (Key Components)

*   **`app/src/main/java/com/sezanx/taxcalculatorbd/`** (Package Name)
    *   **`MainActivity.kt`:** The main screen of the application. Handles user input, calculation logic, UI updates, PDF generation trigger, and navigation to Developer Info.
    *   **`DeveloperInfoActivity.kt`:** Displays information about the developer, including links. Handles link clicks.
*   **`app/src/main/res/`**
    *   **`layout/`**
        *   **`activity_main.xml`:** Defines the UI structure for the main calculator screen using `CoordinatorLayout`, `AppBarLayout`, `NestedScrollView`, `MaterialCardView`, `TextInputLayout`, `Spinner`, `MaterialButton`, etc. Includes the layout for the Tax Slabs card.
        *   **`activity_developer_info.xml`:** Defines the UI for the Developer Information screen using `CoordinatorLayout`, `AppBarLayout`, `MaterialCardView`, `ShapeableImageView`, `TextView`, etc.
    *   **`values/`**
        *   **`colors.xml`:** Defines the color palette used throughout the application.
        *   **`strings.xml`:** Contains all user-facing text strings, including labels, hints, button texts, taxpayer categories, tax slab ranges/rates, error messages, developer info, etc. This makes the app localization-ready.
        *   **`themes.xml`:** Defines the base application theme (inheriting from `Theme.Material3...`) and specifies default styles for various Material Components (`MaterialCardView`, `MaterialButton`, `TextInputLayout`, `Toolbar`).
        *   **`styles.xml`:** Contains additional reusable styles for text appearances (`TextAppearance.App.*`), layout elements (`ResultRowLayout`, `SlabRowLayout`, `AppDivider`), etc.
    *   **`drawable/`**
        *   **`ic_check_circle.xml`:** (Vector Drawable) Green checkmark icon (potentially used if status tracking was kept).
        *   **`bg_spinner.xml`:** (Shape Drawable) Defines the background shape and border for the taxpayer category Spinner.
        *   **`dev_profile_pic.jpg/png`:** Developer's profile picture placed here.
    *   **`menu/`**
        *   **`main_menu.xml`:** Defines the options menu (e.g., three dots in the toolbar) containing the "Developer Info" item.
    *   **`xml/`**
        *   **`provider_paths.xml`:** Defines accessible file paths for the `FileProvider` used for sharing the generated PDF.
*   **`app/build.gradle` (or `build.gradle.kts`)**
    *   Contains dependencies for core AndroidX libraries, Material Components, and potentially others. Enables View Binding.
*   **`app/src/main/AndroidManifest.xml`**
    *   Declares application components (`MainActivity`, `DeveloperInfoActivity`), permissions (like `INTERNET`), the `FileProvider`, and sets the application theme and launcher activity.

---

### 4. Core Algorithms & Logic (`MainActivity.kt`)

#### 4.1. Tax Calculation Flow (`calculateAndDisplayTax` function)

1.  **Get Input:** Retrieves values from `TextInputEditText` fields for Basic Salary, Bonus, Other Income, and Investment using the `getInputAsDouble` helper function. This function handles basic validation (non-empty for required fields, numeric format) and returns `null` on error.
2.  **Calculate Total Income:** Sums up Basic Salary, Bonus, and Other Income.
3.  **Apply Exemptions (Placeholder):** Calculates *example* exemptions for House Rent, Medical, and Conveyance based on Basic Salary and predefined limits. **This section MUST be updated with accurate NBR rules.**
4.  **Calculate Gross Taxable Income:** Subtracts calculated exemptions from Total Income. Ensures the result is not negative.
5.  **Get Tax-Free Limit:** Calls `getTaxFreeLimit()` function, which checks the selected item position in the `spinnerTaxpayerCategory` and returns the corresponding tax-free income threshold based on predefined constants (e.g., `TAX_FREE_LIMIT_GENERAL`, `TAX_FREE_LIMIT_FEMALE_SENIOR`).
6.  **Calculate Tax Before Rebate (`calculateTaxSlabs`):**
    *   Checks if Taxable Income is below the determined Tax-Free Limit. If yes, returns 0 tax.
    *   If above the limit, subtracts the Tax-Free Limit from the Taxable Income to get the income subject to slabs.
    *   Iteratively calculates tax for each slab:
        *   Determines the amount of income falling into the current slab (`coerceAtMost`).
        *   Applies the corresponding slab rate (`SLAB_RATE_X`).
        *   Adds the calculated tax for the slab to the total tax.
        *   Subtracts the taxed amount from the remaining income.
        *   Moves to the next slab until all remaining income is taxed at the highest rate.
    *   **Note:** The slab amounts (`SLAB_AMOUNT_X`) represent the *size* of each slab *after* the tax-free limit (e.g., first 100,000, next 400,000). These **must be verified** with NBR rules.
7.  **Calculate Investment Rebate (`calculateRebate`):**
    *   Checks if Taxable Income is below the Tax-Free Limit. If yes, returns 0 rebate.
    *   Determines the maximum base for eligible investment: the *lower* of (Taxable Income * Max Percentage, Max Absolute Amount).
    *   Determines the actual investment amount considered for rebate: the *lower* of (User's Input Investment, Max Eligible Base).
    *   Calculates the rebate by applying the Rebate Rate (e.g., 15%) to the investment amount considered.
    *   **(Verification Needed):** Check if there's an absolute cap on the final rebate amount itself.
8.  **Calculate Net Tax Payable:** Subtracts the Investment Rebate from the Tax Payable Before Rebate. Ensures the result is not negative (`coerceAtLeast(0.0)`).
9.  **Apply Minimum Tax:**
    *   Checks if Taxable Income is above the Tax-Free Limit.
    *   If yes, compares the calculated Net Tax Payable with the applicable Minimum Tax (currently hardcoded, **needs logic based on user's location/status**). The final Net Tax Payable is the *higher* of the calculated tax or the minimum tax (`coerceAtLeast(minimumTax)`).
    *   If Taxable Income is below the limit, Net Tax Payable is 0.
10. **Store Results:** Stores the calculated `taxableIncome`, `taxBeforeRebate`, `investmentRebate`, and `netTaxPayable` in class member variables (`lastCalculated...`) for later use by the PDF generation function.
11. **Display Results (`displayResults`):** Updates the `TextViews` in the "Tax Summary" card (`cardResults`) with the formatted currency values. Makes the results card visible and scrolls down to it.

#### 4.2. PDF Generation (`generatePdfReport` function)

1.  **Check Data:** Verifies that tax has been calculated previously (checks if `lastCalculatedNetTaxPayable` is not null).
2.  **Create Document:** Initializes a `PdfDocument` and defines page info (A4 size assumed). Starts a new page and gets the `Canvas`.
3.  **Define Paints:** Creates `Paint` objects to control the appearance (text size, color, alignment, bold) of different elements (title, labels, values, footer).
4.  **Draw Content on Canvas:**
    *   Uses `canvas.drawText()` to draw the title, subtitle (with assessment year and category), labels, and formatted currency values at specific X, Y coordinates.
    *   Uses `canvas.drawLine()` to draw a divider.
    *   Calculates `yPos` incrementally to position elements vertically.
    *   Draws a footer with the generation date and app name.
5.  **Finish Page:** Calls `pdfDocument.finishPage(page)`.
6.  **Save File:**
    *   Generates a unique filename using a timestamp (`TaxReport_YYYYMMDD_HHMMSS.pdf`).
    *   **For Android Q (API 29) and above:** Uses `MediaStore` API to save the file directly to the public `Downloads` directory. It creates a `ContentValues` entry specifying the filename, MIME type (`application/pdf`), and relative path, then gets a `Uri` via `contentResolver.insert`. An `OutputStream` is opened from this `Uri`, and `pdfDocument.writeTo(outputStream)` writes the data.
    *   **For versions below Android Q:** Saves the file to the app's *external cache directory* (`applicationContext.externalCacheDir`) in a subfolder. This location doesn't typically require `WRITE_EXTERNAL_STORAGE` permission. It then gets a shareable `Uri` using `FileProvider.getUriForFile()`.
7.  **Trigger Share (`sharePdf`):** If the file is saved successfully and a `Uri` is obtained, calls the `sharePdf` function.
8.  **Error Handling:** Uses `try...catch` blocks to handle potential `IOException` during file saving or other exceptions. Shows error messages via `Toast`.
9.  **Close Document:** Uses a `finally` block to ensure `pdfDocument.close()` is always called, releasing resources.

#### 4.3. PDF Sharing (`sharePdf` function)

1.  **Create Intent:** Creates an `Intent` with `Intent.ACTION_SEND`.
2.  **Set Type:** Sets the MIME type to `application/pdf`.
3.  **Add File URI:** Puts the `Uri` of the generated PDF file into the intent's `EXTRA_STREAM`.
4.  **Grant Permission:** Adds the `Intent.FLAG_GRANT_READ_URI_PERMISSION` flag. This is crucial to allow the app chosen by the user (e.g., Gmail, WhatsApp) to read the file from the provided URI (especially important when using `FileProvider`).
5.  **Start Chooser:** Uses `Intent.createChooser` to show the standard Android share sheet, allowing the user to select an app to share the PDF with. Includes error handling for `ActivityNotFoundException`.

#### 4.4. UI Updates & Helpers

*   **`setupTaxpayerCategorySpinner`:** Populates the Spinner with categories from `strings.xml` and sets an `OnItemSelectedListener`.
*   **`updateSlabDisplayCard`:** Updates the text of the first slab range `TextView` (`@+id/textSlab1Range`) based on the selected Spinner position.
*   **`getTaxFreeLimit`:** Returns the correct tax-free threshold based on the selected Spinner position.
*   **`displayResults`:** Formats numbers as BDT currency and updates the result `TextViews`. Makes the result card visible and scrolls to it.
*   **`getInputAsDouble`:** Safely parses text input to `Double`, handling empty strings and format errors, showing errors on the `TextInputLayout`.
*   **`formatCurrency`:** Formats a `Double` value into a BDT currency string using appropriate locale settings.
*   **`hideKeyboard`:** Dismisses the soft keyboard.

---

### 5. Setup and Usage

1.  **Build:** Clone/download the project and open it in Android Studio. Ensure all dependencies are synced. Build the project (`Build -> Make Project` or Run).
2.  **Install:** Install the generated APK on an Android device or emulator.
3.  **Usage:**
    *   Launch the app.
    *   Select the appropriate Taxpayer Category from the dropdown. Notice the first tax slab range updates accordingly.
    *   Enter Annual Basic Salary (Required).
    *   Enter Annual Bonus and Other Taxable Income (Optional, enter 0 if none).
    *   Enter the Total Eligible Investment amount for rebate (Optional, enter 0 if none).
    *   Tap the "Calculate Tax" button.
    *   The "Tax Summary" card will appear, displaying the calculated Gross Taxable Income, Tax Payable Before Rebate, Investment Rebate, and Net Tax Payable.
    *   Tap the "Generate PDF Report" button. A PDF summary will be generated, saved to the Downloads folder, and a share sheet will appear allowing you to share the PDF.
    *   Tap the options menu (three dots) in the toolbar and select "Developer Info" to view the developer information page.

---

### 6. Known Limitations & Future Improvements

*   **Tax Rule Accuracy:** The implemented tax slabs, rates, exemption rules, and rebate calculations are **examples** based on general understanding or specific screenshots provided during development. They **must be verified and updated** according to the latest official NBR circulars for the relevant Assessment Year to be accurate.
*   **Exemptions:** The current exemption calculation is highly simplified (placeholder). A robust implementation should allow users to input details for specific allowances (House Rent, Medical, Conveyance, etc.) and apply NBR rules accurately.
*   **Minimum Tax:** The minimum tax calculation currently uses a default value. It needs to be updated based on the taxpayer's actual location (Dhaka/Ctg City Corp, Other City Corp, Other Area), which requires adding UI for location selection.
*   **Assessment Year Selection:** The "Year" button currently does nothing. Functionality should be added (e.g., using a DatePicker or NumberPicker) to select the Assessment Year, and the tax rules (constants) should potentially be adjusted based on the selected year.
*   **Error Handling:** More specific error messages and input validation can be added.
*   **UI/UX:** Further refinements to the UI, animations, and user feedback can be implemented.
*   **Localization:** While strings are externalized, translating them into Bengali would improve usability.
*   **Data Persistence:** User inputs are currently not saved. SharedPreferences or a database could be used to save inputs between sessions.
*   **Runtime Permissions (Pre-Android 10):** If targeting older Android versions, the code to request `WRITE_EXTERNAL_STORAGE` at runtime needs to be implemented for PDF saving to Downloads (though saving to cache currently bypasses this).

---

This documentation provides a comprehensive overview of the Bangladesh Tax Calculator application as developed. Remember that maintaining accuracy, especially regarding tax rules, is crucial for such an application.
