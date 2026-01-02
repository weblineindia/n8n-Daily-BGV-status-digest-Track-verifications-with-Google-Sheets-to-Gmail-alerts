# Daily BGV Status Digest: Track Verifications with Google Sheets to Gmail Alerts

This n8n workflow sends a **daily late‑night email summary** to each Background Verification (BGV) executive using your “BGV Tracker” Google Sheet. Each executive receives a personalized digest listing **candidates whose background checks were completed today**, along with **pending cases** — including clearly flagged “stale” items that need follow‑up. The workflow runs every night at **23:00 IST**, auto‑groups entries per executive, and sends formatted Gmail alerts. :contentReference[oaicite:1]{index=1}

---

## 🚀 Quick Start – Implementation Steps

1. Import the workflow JSON into your **n8n instance**. :contentReference[oaicite:2]{index=2}
2. Prepare your **Google Sheet** tab labeled `BGV Tracker` with required columns. :contentReference[oaicite:3]{index=3}
3. Add **Google Sheets OAuth2** credentials in n8n for reading your tracking sheet. :contentReference[oaicite:4]{index=4}
4. Add **Gmail credentials** (OAuth or App Password) to send alert emails. :contentReference[oaicite:5]{index=5}
5. Configure the **Schedule Trigger** node to run daily at your desired time (default: 23:00 IST). :contentReference[oaicite:6]{index=6}
6. Activate the workflow and verify the first run with sample data. :contentReference[oaicite:7]{index=7}

---

## 📌 What It Does

This automation:

- **Reads your “BGV Tracker” sheet** every night, pulling key fields such as:
  - `candidate_name`
  - `previous_company`
  - `prevco_hr_name`
  - `prevco_hr_email`
  - `bgv_status`
  - `last_follow_up`
  - `bgv_completion_date`
  - `bgv_executive`
  - `bgv_exe_email` :contentReference[oaicite:8]{index=8}
- **Normalizes and parses** dates across multiple formats.
- Flags items **completed today** and **stale pending cases** (pending with last follow‑up ≥ 3 days). :contentReference[oaicite:9]{index=9}
- **Groups rows by executive email**, creating personalized digests.
- Builds a **daily HTML email** per executive with two tables:
  - Completed Today
  - Pending (with ⚠️ stale alerts) :contentReference[oaicite:10]{index=10}
- Sends the email via **Gmail** automatically, with customizable subject and layout. :contentReference[oaicite:11]{index=11}

---

## 👥 Who’s It For

This workflow is ideal for:

- **BGV team leads & vendors** who want automatic daily updates on their verification queues. :contentReference[oaicite:12]{index=12}
- **HR managers** wanting to automate compliance and candidate tracking. :contentReference[oaicite:13]{index=13}
- **Ops teams** using Google Sheets to manage background check statuses. :contentReference[oaicite:14]{index=14}
- Organizations managing candidate checks across multiple owners/executives. :contentReference[oaicite:15]{index=15}

---

## 🛠 Requirements

- Google Sheets **“BGV Tracker”** sheet with supported columns. :contentReference[oaicite:16]{index=16}
- Gmail credentials (OAuth or App Password) with permission to send emails. :contentReference[oaicite:17]{index=17}
- An n8n instance (cloud or self‑hosted) with Google and Gmail credentials configured. :contentReference[oaicite:18]{index=18}

---

## ⚙️ How It Works & Setup Details

1. **Schedule Trigger** — Runs every day at 23:00 IST (can be modified). :contentReference[oaicite:19]{index=19}
2. **Google Sheets Read** — Reads all rows from the `BGV Tracker` sheet. :contentReference[oaicite:20]{index=20}
3. **Normalize & Parse** — Code nodes clean column names and parse dates. :contentReference[oaicite:21]{index=21}
4. **Group & Filter** — Groups by executive email; separates Completed and Pending lists. :contentReference[oaicite:22]{index=22}
5. **Format Digest** — Code node builds personalized HTML email content. :contentReference[oaicite:23]{index=23}
6. **Gmail Alert** — Sends formatted emails to each executive with their digest. :contentReference[oaicite:24]{index=24}

---

## 🎨 How to Customize

- **Run Time** — Modify the Schedule Trigger to fit your operational hours. :contentReference[oaicite:25]{index=25}
- **Skip Weekends** — Add conditional logic to exclude Sat/Sun runs. :contentReference[oaicite:26]{index=26}
- **Stale Threshold** — Edit the “>= 3 days” logic in the parse code to change stale criteria. :contentReference[oaicite:27]{index=27}
- **Email Template** — Customize the HTML layout or add additional summary sections. :contentReference[oaicite:28]{index=28}
- **Attachments** — Optionally attach CSVs, add CC, or include manager summaries. :contentReference[oaicite:29]{index=29}

---

## ➕ Add‑Ons (Optional Enhancements)

- **Manager Summary** — Aggregate all digests and send a consolidated email to HR heads. :contentReference[oaicite:30]{index=30}
- **CSV Exports** — Attach filtered candidate lists per executive. :contentReference[oaicite:31]{index=31}
- **Slack Reminders** — DM executives with their stale pending items. :contentReference[oaicite:32]{index=32}
- **Auto Write‑Back** — Update next follow‑up dates in the sheet for stale cases. :contentReference[oaicite:33]{index=33}

---

## 📈 Use Case Examples

1. **BGV Vendor Automation** — Nightly queue email helps each checker focus on daily work. :contentReference[oaicite:34]{index=34}
2. **HR Compliance Reporting** — HRBP receives daily statuses with overdue alerts. :contentReference[oaicite:35]{index=35}
3. **Large Hiring Projects** — Send only relevant candidates per executive for clarity and efficiency. :contentReference[oaicite:36]{index=36}

---

## 🧪 Common Troubleshooting

| **Issue**                   | **Possible Cause**                   | **Solution**                                        |
| --------------------------- | ------------------------------------ | --------------------------------------------------- | --------------------------------------- |
| No emails sent              | Gmail credentials missing or expired | Re‑authenticate Gmail node and check sending limits | :contentReference[oaicite:37]{index=37} |
| Candidates missing in email | Missing or invalid `bgv_exe_email`   | Ensure every row has a valid executive email        | :contentReference[oaicite:38]{index=38} |
| Completed items not listed  | Date format mismatch in sheet        | Use supported date format; adjust parse logic       | :contentReference[oaicite:39]{index=39} |
| Pending not marked stale    | Last follow‑up format issues         | Standardize date formats or update code node logic  | :contentReference[oaicite:40]{index=40} |
| Workflow runs on weekends   | Schedule misconfigured               | Add weekend checks or adjust trigger                | :contentReference[oaicite:41]{index=41} |

---

## 💬 Need Help?

If you need assistance with setup, customizing templates, connecting Slack/CSV attachments, or scaling this digest across systems — our n8n experts at **WeblineIndia** can help you tailor and optimize the workflow to match your HR operations and reporting needs. :contentReference[oaicite:42]{index=42}

---

📥 _If you want this as a downloadable `README.md` file, just tell me “generate file”!_
::contentReference[oaicite:43]{index=43}
