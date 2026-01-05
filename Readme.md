# Daily BGV Status Digest: Track Verifications with Google Sheets to Gmail Alerts

This n8n workflow sends a **daily late-night email summary** to each Background Verification (BGV) executive using your **“BGV Tracker”** Google Sheet.
Each executive receives a **personalized digest** listing candidates **completed today** and **pending cases**, with clearly flagged **stale items** requiring follow-up.

The workflow runs automatically every night at **23:00 IST**, groups records per executive, and sends formatted Gmail alerts — eliminating manual tracking.

---

## 🚀 Quick Start – Implementation Steps

1. Import the workflow JSON into your **n8n instance**
2. Prepare a Google Sheet named **`BGV Tracker`** with required columns
3. Configure **Google Sheets OAuth2** credentials in n8n
4. Configure **Gmail credentials** (OAuth or App Password)
5. Set the **Schedule Trigger** (default: 23:00 IST)
6. Activate the workflow and test with sample data

---

## 📌 What It Does

This automation:

* Reads your **BGV Tracker** sheet nightly
* Extracts key fields:

  * `candidate_name`
  * `previous_company`
  * `prevco_hr_name`
  * `prevco_hr_email`
  * `bgv_status`
  * `last_follow_up`
  * `bgv_completion_date`
  * `bgv_executive`
  * `bgv_exe_email`
* Normalizes and parses multiple date formats
* Identifies:

  * ✅ **Completed today**
  * ⚠️ **Pending & stale** (pending for ≥ 3 days)
* Groups rows **per executive**
* Builds **HTML email digests** with:

  * Completed Today table
  * Pending (stale highlighted)
* Sends emails via **Gmail**

---

## 👥 Who’s It For

Ideal for:

* BGV teams and vendors
* HR managers and HRBPs
* Operations teams managing BGV in Google Sheets
* Organizations with multiple BGV executives

---

## 🛠 Requirements

* Google Sheet named **`BGV Tracker`**
* Gmail account with send permission
* n8n instance (cloud or self-hosted)
* Google Sheets & Gmail credentials configured in n8n

---

## ⚙️ How It Works

1. **Schedule Trigger** – Runs daily at 23:00 IST
2. **Google Sheets Read** – Fetches all rows from `BGV Tracker`
3. **Normalize & Parse** – Cleans column names and parses dates
4. **Group & Filter** – Groups by executive and separates Completed vs Pending
5. **Format Digest** – Generates personalized HTML email content
6. **Gmail Node** – Sends emails to each executive

---

## 🎨 Customization Options

* **Run Time** – Change Schedule Trigger time
* **Skip Weekends** – Add IF condition for Sat/Sun
* **Stale Threshold** – Modify “≥ 3 days” logic
* **Email Template** – Update HTML layout or add summaries
* **Attachments** – Add CSV exports or CC managers

---

## ➕ Optional Enhancements

* Manager-level consolidated summary
* CSV attachments per executive
* Slack reminders for stale cases
* Auto write-back follow-up dates to Sheets

---

## 🧪 Common Troubleshooting

| Issue                     | Possible Cause                | Solution                                      |
| ------------------------- | ----------------------------- | --------------------------------------------- |
| No emails sent            | Gmail auth missing or expired | Reconnect Gmail credentials                   |
| Candidates missing        | Missing `bgv_exe_email`       | Ensure each row has a valid executive email   |
| Completed not shown       | Date format mismatch          | Standardize date format or update parse logic |
| Pending not marked stale  | Invalid last follow-up date   | Fix date format or adjust code logic          |
| Workflow runs on weekends | Schedule misconfigured        | Add weekend exclusion logic                   |

---

## 💬 Need Help?

Need help with setup, template customization, Slack integration, or scaling this workflow?
**WeblineIndia** provides professional n8n automation support tailored to HR and BGV operations.
