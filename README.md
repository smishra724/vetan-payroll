# Vetan Payroll

Payroll and HR for small Indian companies, in a single web page. No server, no build step, no sign-up: open `index.html` or host it on GitHub Pages.

## What it does

- **Dashboard**: this month's payroll (pending or processed), PF / ESI / TDS / PT totals, statutory due dates, workforce by department, records needing attention and a to-do list.
- **Sign-in**: separate **Employer** and **Employee** logins. The employer creates a username and password on first use (with a recovery code). Employees sign in with their employee code; their first password is their date of birth as DDMMYYYY and they set their own on first sign-in. Employers can reset passwords or turn sign-in off per employee.
- **Users & permissions**: the owner adds employer users (HR staff, managers, accountants) and gives each a role. For every section (employees, attendance, payroll, leave, loans, compliance, reports, settings) a role can be allowed to **view**, **edit**, and **approve or reject**. Ready-made roles: Admin, HR manager, Payroll officer, Team manager, View only; roles can be edited or created. Menus, buttons, dashboard blocks and salary figures follow the role.
- **Employee portal**: employees see their own profile, payslips, attendance and roster, apply for leave, request advances, upload their documents and change their password.
- **Employees**: quick add, CSV import, edit, deactivate, payslip preview, and **add from PDF or photo**: upload PAN, Aadhaar, a cheque, an offer letter or a scanned employee list; text is read with OCR (Tesseract.js, on the device) and pre-filled for review.
- **Candidate self-onboarding**: *Send joining link* (on the Dashboard, Employees and Onboarding pages) creates a link (share by WhatsApp, email or copy). The candidate fills in personal, contact, ID and bank details, uploads the requested documents and can take a passport photo with the phone or computer camera. The form produces one file they send back to HR; *Import submission* loads it. HR approves or rejects each document (with a reason), ticks details to correct, sends a correction link, and marks the candidate verified.
- **Appointment letter**: upload a Word (.docx) template once (Settings or the letter screen) with fields like `<<EmployeeName>>`, `<<Designation>>`, `<<JoiningDate>>`, `<<BasicMonthly>>`, `<<GrossAnnual>>`, `<<Director Name>>`. Vetan fills them and downloads the letter, with Share, Email and WhatsApp shortcuts. The template stays in your browser and is not part of this repository.
- **Camera capture**: take passport photos or photograph documents with the camera on the employee's documents panel and the candidate form.
- **Onboarding**: a four-step form for new joiners (personal details → job & salary → statutory & bank → documents) with uploads for photo, PAN, Aadhaar, bank proof, certificates and more. Drafts can be saved and continued later; joiners enter payroll only once onboarding is complete.
- **Bulk updates**: on Attendance and Roster, tick several employees (or quick-select a department or shift), choose a date range, and mark them all at once (present, absent, leave, holiday, week off, or clear) or set a shift, custom timing, week off or reset, skipping week offs if you want.
- **Attendance**: monthly grid (Present, Absent, Half day, Paid leave, Leave without pay, Holiday, Week off) with automatic loss-of-pay days.
- **Roster & shifts**: weekly shift roster with coverage counts and weekly hours. Type each day's timing as 24-hour clock numbers from 00:00 to 23:59, e.g. 09:00-18:00 (overnight shifts included), or OFF. Import the roster from Excel or CSV, download it as Excel, copy last week or reset. Rostered offs feed attendance.
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
- Because of this, employees can only sign in on the device that holds the data. Passwords are stored as salted SHA-256 hashes, but the sign-in is an in-browser lock, not server-side security. For employees to sign in from their own phones, connect a hosted database and authentication (for example Firebase).

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
