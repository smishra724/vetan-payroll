# Vetan Payroll

Payroll and HR for small Indian companies, in a single web page. No server, no build step, no sign-up: open `index.html` or host it on GitHub Pages.

## What it does

- **Dashboard**: this month's payroll (pending or processed), PF / ESI / TDS / PT totals, statutory due dates, workforce by department, records needing attention and a to-do list.
- **Employees**: quick add, CSV import, edit, deactivate, payslip preview.
- **Onboarding**: a four-step form for new joiners (personal details → job & salary → statutory & bank → documents) with uploads for photo, PAN, Aadhaar, bank proof, certificates and more. Drafts can be saved and continued later; joiners enter payroll only once onboarding is complete.
- **Attendance**: monthly grid (Present, Absent, Half day, Paid leave, Leave without pay, Holiday, Week off) with automatic loss-of-pay days.
- **Roster & shifts**: weekly shift roster with coverage counts and weekly hours, copy-last-week, reset, CSV export; shift setup including overnight shifts. Rostered offs feed attendance.
- **Run payroll**: pro-rated earnings, PF (12% of basic up to the ₹15,000 ceiling), ESI (0.75% / 3.25% up to ₹21,000 gross), state professional tax, new-regime TDS estimate with the ₹12 L rebate and marginal relief, loan EMIs, bonus and other deductions. Processing locks the month; runs can be reopened.
- **Downloads**: payroll register, NEFT bank transfer sheet, EPFO ECR text file, payslips, and reports (employee master, attendance, roster, leave, loans, CTC, department summary).
- **Leave and loans**: requests, approvals, automatic attendance marking and EMI recovery.
- **Compliance**: deposit calendar with "mark paid", rate cards for PF, ESI, TDS and PT, Form 24Q due dates.
- **Settings**: company profile, statutory rates, TDS slabs, salary structures, backup and restore.

## Where data is stored

This version keeps everything **in the browser that uses it**:

- Records are kept in `localStorage`; uploaded documents in `IndexedDB`.
- Nothing is sent to any server, and GitHub never sees your data.
- Data does **not** sync between devices or people, and is lost if the browser's site data is cleared.

Use **Settings → Backup & restore** to download a backup file regularly and to move data to another browser. Uploaded documents are not included in the backup file.

For a shared, multi-user setup you would connect a hosted database (for example Supabase or Firebase) in place of the `localDB()` and `localAssets()` functions in `index.html`.

## Publish on GitHub Pages

1. Push this repository to GitHub.
2. Go to **Settings → Pages**.
3. Under **Build and deployment**, choose **Deploy from a branch**, branch `main`, folder `/ (root)`, and save.
4. After a minute the app is live at `https://<your-username>.github.io/<repository-name>/`.

A public repository makes the **code** public, not your data, which stays in each user's browser. GitHub Pages on a private repository needs a paid GitHub plan.

## Run locally

Open `index.html` in a browser, or serve the folder:

```sh
python3 -m http.server 8000
# then visit http://localhost:8000
```

## Important

Statutory rates and slabs (PF, ESI, professional tax by state, TDS) are defaults that can be edited in Settings. Confirm them with your CA before paying salaries. Labour Welfare Fund is not calculated.
