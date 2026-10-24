# CyberShield: Security Awareness Training Platform with Authorized Phishing Simulation

A professional, full-stack cybersecurity awareness training platform designed to transform employees and students into an active human security perimeter. The platform combines interactive security training across 12 foundational categories, server-evaluated multiple-choice quizzes, persistent progress tracking, printable certificates of achievement, and an authorized, safe mock phishing simulation engine with instant micro-learning debriefs.

---

## 1. System Architecture & Tech Stack

```
security-awareness-platform/
├── backend/
│   ├── app/
│   │   ├── models/            # SQLAlchemy Database Models (User, Training, Quiz, Simulation, Audit)
│   │   ├── routes/            # REST API Endpoints (Auth, Training, Quizzes, Simulation, Admin)
│   │   ├── security/          # JWT handling, input validation, role-based decorators
│   │   ├── services/          # Real-time statistics, metrics & audit logging services
│   │   ├── config.py          # App & testing configurations (SQLite, CORS, JWT)
│   │   └── extensions.py      # SQLAlchemy & CORS extensions
│   ├── tests/                 # Automated Pytest test suite (21 passing tests)
│   ├── requirements.txt       # Python dependencies
│   ├── run.py                 # Flask server runner (Port 5000)
│   └── security_training.db   # Persistent SQLite Database
├── frontend/
│   ├── src/
│   │   ├── api/               # Centralized Fetch API client with automatic JWT handling
│   │   ├── components/        # Navbar, Sidebar, CertificateModal, ErrorAlert, Spinner
│   │   ├── context/           # AuthContext (login, register, session persistence)
│   │   ├── pages/             # 18 Full-featured application pages
│   │   ├── App.jsx            # Dynamic client router with server-verified RBAC
│   │   └── index.css          # Tailwind CSS styling & dark SOC theme
│   ├── package.json           # Frontend dependencies (React 18, Vite 6, Tailwind 3.4, Recharts)
│   └── vite.config.js         # Vite configuration with `/api` reverse proxy
├── scripts/
│   ├── seed_database.py       # Seeds 12 modules, quizzes, mock campaigns, and demo accounts
│   ├── create_admin.py        # Secure CLI administrator creator/promoter
│   └── package_project.py     # Script to package the clean distribution ZIP
├── .env.example               # Environment variables template
├── .gitignore                 # Excludes node_modules, .venv, caches, and build artifacts
└── README.md                  # Comprehensive setup and operating guide
```

### Technology Highlights
- **Frontend:** React.js 18 with Vite 6, Tailwind CSS (Dark SOC Theme), Lucide React icons, Recharts data visualization.
- **Backend:** Python 3.10+ with Flask REST API, Flask-CORS, PyJWT (HS256 with 32+ byte cryptographic keys).
- **Database:** SQLite with SQLAlchemy 2.0 ORM, strict unique constraints, relational cascading, and indexed lookups.
- **Authentication:** Werkzeug `generate_password_hash` (PBKDF2:SHA256) and signed JWT tokens stored client-side in `localStorage`.
- **Testing:** Automated Pytest suite covering authentication, RBAC, scoring, simulation event logging, and report generation.

---

## 2. Windows / VS Code Step-by-Step Setup Guide

### Prerequisites
1. **Python 3.10 or higher**: Verify with `python --version` in terminal.
2. **Node.js 18 or higher (with npm)**: Verify with `node --version` and `npm --version`.
3. **Visual Studio Code**: Recommended editor.

---

### Step 1: Open the Project in VS Code
1. Launch **VS Code**.
2. Click **File > Open Folder...** and select the `security-awareness-platform` folder.
3. Open a new terminal inside VS Code: **Terminal > New Terminal** (or press `` Ctrl + ` ``).

---

### Step 2: Configure and Start the Flask Backend

In the VS Code terminal, navigate to the `backend` folder:
```powershell
cd backend
```

#### A. (Optional but recommended) Create and Activate a Python Virtual Environment
```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
```
*(If PowerShell displays an execution policy error, run `Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass` or activate using `.\.venv\Scripts\activate.bat` in CMD).*

#### B. Install Backend Dependencies
```powershell
python -m pip install -r requirements.txt
```

#### C. Initialize and Seed the Database
From the root directory or backend directory, run the automated database seeder:
```powershell
python ..\scripts\seed_database.py
```
This script automatically:
- Creates all SQLite database tables in `backend/security_training.db`.
- Seeds **12 rich security awareness modules** with real-world case studies, warning signs, and prevention tips.
- Seeds corresponding **quizzes with realistic multiple-choice questions**.
- Seeds **3 authorized mock phishing campaigns**.
- Seeds demo student accounts and an administrator account.

#### D. (Optional) Create a Custom Administrator
You can securely create or promote an admin account via the interactive CLI:
```powershell
python ..\scripts\create_admin.py
```

#### E. Run Automated Backend Tests
Run the automated Pytest test suite to verify all 21 test scenarios:
```powershell
python -m pytest tests -v
```
*Expected result: 21 passed in ~5 seconds.*

#### F. Start the Flask Backend Server
```powershell
python run.py
```
The Flask REST API will start on:
```
http://127.0.0.1:5000
```
Health Check endpoint: `http://127.0.0.1:5000/api/health`

---

### Step 3: Configure and Start the React Frontend

Open a **second terminal tab** in VS Code (click the `+` icon in the terminal panel) and navigate to `frontend`:
```powershell
cd frontend
```

#### A. Install Frontend Dependencies
```powershell
npm.cmd install
```
*(On Windows PowerShell, use `npm.cmd` or `cmd /c npm install` if script execution is disabled).*

#### B. Start the React Development Server
```powershell
npm.cmd run dev
```

The Vite dev server will start instantly and provide the local URL:
```
http://localhost:5173
```

Open **`http://localhost:5173`** in your web browser to access the CyberShield platform!

---

## 3. Pre-Seeded Demonstration Accounts

For quick local testing and evaluation, the database comes pre-seeded with two demonstration accounts:

| Role | Username | Email | Password | Access Privileges |
| :--- | :--- | :--- | :--- | :--- |
| **Student** | `student` | `student@cybertraining.local` | `StudentPassword123!` | Training modules, quizzes, progress tracking, phishing inbox, certificate generator |
| **Administrator** | `admin` | `admin@cybertraining.local` | `AdminPassword123!` | SOC telemetry dashboard, user management, module editor, quiz inspector, campaign manager, audit logs, CSV exports |

*Tip: The Login page includes one-click **"Demo Student"** and **"Demo Admin"** quick-fill buttons for immediate testing.*

---

## 4. Key Platform Features

### A. 12 Core Security Awareness Training Modules
Every module includes comprehensive learning objectives, full-text instructional guides, real-world breach case studies, warning signs/red flags, and preventive best practices:
1. **Phishing & Email Security**: Spear phishing, BEC, spoofed sender domains, URL inspection.
2. **Password Security & Password Managers**: Entropy calculation, credential stuffing, zero-knowledge vaults.
3. **Multi-Factor Authentication (MFA)**: SMS vulnerabilities, push bombing/fatigue defense, FIDO2 tokens.
4. **Social Engineering Awareness**: Pretexting, vishing, baiting, tailgating, psychological manipulation.
5. **Malware & Ransomware Defense**: Kill chain, double extortion, lateral movement, network isolation.
6. **Safe Web Browsing & Fraudulent Portals**: HTTPS padlock myths, URL hierarchy parsing, malvertising.
7. **Data Privacy & Protection**: PII, data classification tiers, shadow IT avoidance, AI prompt safety.
8. **Wi-Fi & Network Security**: Rogue access points, Evil Twins, public hotspot eavesdropping, VPNs.
9. **Removable Media & USB Security**: BadUSB keystroke injection, juice jacking, hardware hygiene.
10. **Incident Reporting & Response**: No-blame reporting culture, SOC escalation tiers, evidence preservation.
11. **Mobile Device Security**: App permissions, smishing defense, mobile device management (MDM).
12. **Cyber Hygiene & Secure Remote Work**: Clean desk policy, screen locks (`Win + L`), Wi-Fi router hardening.

Each module features a **"Mark as Completed"** action that persists completion timestamps in SQLite and updates the student's dashboard progress bar.

---

### B. Interactive MCQ Quiz Engine with Server-Side Scoring
- Multiple-choice questions with 4 distinct options.
- **Zero Client Trust**: Question answers and explanations are never sent to the browser prior to submission.
- The Flask backend calculates the score, percentage, and pass/fail status against configured thresholds.
- After submission, a comprehensive question-by-question review reveals correct answers and detailed educational explanations.
- Configurable maximum retakes policy.

---

### C. Authorized Phishing Simulation Engine & Instant Debrief
- **100% Internal & Safe**: Simulations run exclusively inside an internal training feed using synthetic data. No external emails are ever dispatched.
- **Dedicated "Report Phishing" Button**: Encourages and rewards proactive reporting with cyber defense points.
- **Lure Intercept & Instant Micro-Learning Debrief**: Clicking a simulated phishing link safely triggers a modal explaining:
  - That this was an authorized, harmless simulation.
  - The exact red flags present in the email (e.g. sender domain mismatch, high-pressure urgency).
  - How to recognize the pattern in the future.
  - Records simulation click and completion telemetry in SQLite for administrative reporting.

---

### D. Printable & Downloadable Resilience Certificate
- Students who complete modules and pass quizzes can generate an official **Certificate of Cybersecurity Resilience**.
- Displays user full name, department, unique verification ID, issue date, and CISO signature.
- Fully formatted for high-resolution printing or PDF export via browser print dialog.

---

### E. SOC Administrator Command Center & Analytics
- **Live Database Telemetry**: Real-time stats on enrolled students, completed modules, quiz passing rates, phishing click rates, and report rates.
- **Recharts Visualizations**:
  - Training module completion distribution bar chart.
  - Phishing simulation vigilance outcomes pie chart (Reported vs Clicked vs Viewed).
  - Quiz assessment accuracy by module.
- **User Management**: Promote/demote user roles between Student and Administrator, toggle account active/deactivation.
- **Curriculum & Quiz Management**: Create and edit modules, inspect question banks.
- **Campaign Controls**: Launch new simulated phishing lures or trigger an emergency halt on active campaigns.
- **Audit Logs & CSV Export**: Review detailed security event logs and download student compliance reports in CSV format.

---

## 5. Security & Deployment Best Practices

1. **Production Secret Keys**: In production, replace `SECRET_KEY` and `JWT_SECRET_KEY` in `.env` with cryptographically random 64-character strings (`python -c "import secrets; print(secrets.token_hex(32))"`).
2. **CORS Restrictions**: Update `CORS_ORIGINS` to allow only your production domain.
3. **Database Security**: SQLite is ideal for localized and departmental deployments. For large multi-campus deployments, set `DATABASE_URL=postgresql://user:password@host/dbname` in `.env`.
4. **HTTPS Enforcement**: Always deploy behind a reverse proxy (e.g., Nginx or Caddy) with TLS certificates enabled to ensure JWT tokens are encrypted in transit.

---

## 6. Troubleshooting Common Issues

- **PowerShell Script Execution Policy Error on Windows**:
  Run `Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass` in your PowerShell window, or use `npm.cmd` instead of `npm`.
- **Port 5000 Already in Use**:
  Run `$env:PORT=5001; python run.py` to start Flask on port 5001, and adjust `proxy` in `frontend/vite.config.js`.
- **Reset Database**:
  To reset demo data back to default, delete `backend/security_training.db` and run `python scripts/seed_database.py`.
