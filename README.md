# 🚀 Google Chrome Enterprise Deployment & Management

This guide details the process for deploying and centrally managing Google Chrome Enterprise on Windows devices using **Microsoft Intune** for deployment and the **Google Admin Center** for policy configuration.

## 🎯 Prerequisites

Before starting, ensure you have:

* **Microsoft Intune/Endpoint Manager** access.
* **Google Admin Console** access.
* A target group (e.g., a Security Group for "Staff") for assignments in Intune and Google Admin.

## 📦 Step 1: Download and Initial Deployment

The recommended deployment method bypasses standard manual installation by using Intune to push the Chrome Enterprise MSI as a Line-of-Business (LOB) application.

1.  **Download the Installer:**
    * Get the appropriate MSI package for Chrome Enterprise: [Download Link](https://chromeenterprise.google/intl/en_uk/)

2.  **Deploy via Intune (LOB App):**
    * Upload the downloaded MSI file to Intune and deploy it as a **Line-of-Business (LOB) App** to your target device or user group. This is the streamlined method for deployment.
    * ➡️ *For deployment guidance, see this video:* [How to DEPLOY Google Chrome Using Intune!](https://www.youtube.com/watch?v=0-iUD2FaQbI)

## 🔑 Step 2: Enable Management & Get Enrollment Token

To link your devices to your Google Admin Center for policy enforcement, you must first enable the management service and retrieve a unique token.

1.  **Purchase Management (Free):**
    * In your Google Admin console, purchase the **Google Chrome management** service (this is a free service).

2.  **Generate Enrollment Token:**
    * Navigate to **Chrome Browser** > **Managed Browsers**.
    * Select the organizational unit (OU) you wish to enroll (e.g., `Staff`).
    * Click the **Enroll** button and **save the resulting Token**. You will need this for the Intune policy.

## ⚙️ Step 3: Configure Intune Policy for Enrollment

The saved token is used to create an Intune Configuration Profile that tells the deployed Chrome browsers to report to your Google Admin Center.

1.  **Create Configuration Policy:**
    * Create a **Device configuration** policy in Intune.
2.  **Configure Token:**
    * Follow the instructions in **Step 2, Option 1** on the Google Support page to correctly configure the Intune policy that distributes the enrollment token to devices.
    * 🔗 *Reference Guide:* [Enroll browsers on Windows (Google Support)](https://support.google.com/chrome/a/answer/9301891?hl=en&ref_topic=9301744#zippy=%2Cenroll-browsers-on-windows)
3.  **Assign:**
    * Assign this new policy to your target group (e.g., **Staff**).

## ⬆️ Step 4: Add ADMX for Automatic Updates

To manage Chrome updates directly through Intune, you need to import Google's Administrative Templates.

* **Import ADMX/ADML:**
    * Add the necessary Chrome Enterprise **ADMX** and **ADML** files to Intune's administrative templates import section. This enables you to create Configuration Profiles for update policies.
    * 🎥 *For detailed steps on importing the files and configuring the update policy override, see this video:* [How to Manage Google Chrome with Intune!](https://www.youtube.com/watch?v=0d_aKup5KlU)

## ✅ Step 5: Verification and Centralized Configuration

Once the Intune policy is deployed and devices sync, the installed Chrome browsers will be enrolled and appear in the Google Admin Center.

### Verification

* After a short delay, all enrolled Chrome Browsers will appear in the Google Admin Centre under the **Managed Browsers** tab.

### Centralized Settings Management

* Navigate to the **Settings** section and filter the platform to **Chrome for Desktop**.
* Here, you can apply powerful, centralized controls across all managed browsers:

| Configuration Area | Example Settings |
| :--- | :--- |
| **Security & Privacy** | Block incognito mode, enforce safe browsing. |
| **Extensions** | Block specific extensions, or block all non-approved extensions. |
| **Authentication** | Block personal Gmail sign-in, require managed accounts. |
| **Content Filtering** | Set YouTube age restrictions, block specific URLs. |
| **User Experience** | Set the default home page or startup pages. |

---

Would you like me to generate a simple shell script or PowerShell command that could automate the import of the ADMX files into Intune?
