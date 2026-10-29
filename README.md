# SkillSwap — Student Skill Exchange Platform

SkillSwap is a full-stack Django application where students and lifelong learners can offer skills, discover people to learn from, and organize peer-to-peer skill exchanges. The project is designed as a practical portfolio app with user authentication, profile pages, searchable skill listings, request workflows, and a personal dashboard.

## Features

- **Accounts and profiles:** register, log in/out, and maintain public profiles with biography, college, location, interests, and optional avatar.
- **Skill marketplace:** create, edit, activate/pause listings; categorize skills; select teach/learn intent and experience level; add tags and availability.
- **Discovery and filters:** keyword search across listing titles, descriptions, tags, and usernames; filter by category, intent, and level.
- **Exchange requests:** send a personal request with an optional proposed time; recipients can accept or decline; requesters can cancel; participants can mark accepted exchanges complete.
- **Personal dashboard:** summary metrics, listing management, incoming requests, and active exchange links.
- **Admin tools:** Django admin registrations for profiles, skills, and exchange requests.
- **Interface:** responsive custom CSS, mobile navigation, feedback messages, and accessible focus states.
- **Data integrity:** server-side validation, ownership checks, CSRF protection, indexed query fields, transaction-wrapped request actions, and a constraint preventing duplicate open requests for the same skill.

## Technology stack

- Python 3.11+
- Django 5.2
- SQLite for local development
- HTML templates, custom CSS, and vanilla JavaScript
- Django authentication, forms, ORM, admin, and messages framework

## Run locally

### 1. Clone and enter the project

```bash
git clone https://github.com/YOUR_GITHUB_USERNAME/skillswap-pro.git
cd skillswap-pro
```

### 2. Create a virtual environment

Windows PowerShell:

```powershell
py -m venv .venv
.venv\Scripts\Activate.ps1
```

macOS/Linux:

```bash
python3 -m venv .venv
source .venv/bin/activate
```

### 3. Install dependencies

```bash
python -m pip install --upgrade pip
pip install -r requirements.txt
```

### 4. Configure environment (recommended)

Copy `.env.example` to `.env` and set a unique `DJANGO_SECRET_KEY`. The project loads this file through `django-environ`. The app works locally with development defaults, but never deploy with the development secret or debug enabled.

### 5. Run migrations and create an admin account

```bash
python manage.py makemigrations accounts skills swaps
python manage.py migrate
python manage.py createsuperuser
python manage.py seed_demo  # optional: add fictional showcase profiles/listings
python manage.py runserver
```

Open http://127.0.0.1:8000/ and the admin at http://127.0.0.1:8000/admin/.

## Main routes

| Route | Purpose |
|---|---|
| `/` | Landing page and latest active skills |
| `/accounts/register/` | Account registration |
| `/accounts/login/` | Login |
| `/accounts/profile/edit/` | Edit your profile (login required) |
| `/accounts/profile/<username>/` | Public member profile |
| `/skills/` | Search and filter listings |
| `/skills/new/` | Create a skill listing (login required) |
| `/skills/<id>/` | Skill details |
| `/swaps/mine/` | Sent and received exchange requests |
| `/dashboard/` | Personal dashboard (login required) |
| `/admin/` | Django administration |

## Project structure

```text
skillswap-pro/
├── accounts/       # Profile model, registration and profile views
├── config/         # Django settings and root URL configuration
├── dashboard/      # Public landing page and member dashboard
├── skills/         # Skill listings, search, filters, and ownership controls
├── swaps/          # Exchange-request model and status workflow
├── static/css/     # Responsive design system
├── static/js/      # Mobile navigation and small UI interactions
├── templates/      # Shared layout and feature templates
├── manage.py
└── requirements.txt
```

## Optional demo data

Run `python manage.py seed_demo` to create fictional user profiles and sample skill listings for a local showcase. These demo users have unusable passwords, use reserved `.test` email addresses, and do not represent real people. The command is idempotent for its sample entries.

## Production checklist

Before public deployment, set a strong secret from environment variables, set `DJANGO_DEBUG=0`, configure `DJANGO_ALLOWED_HOSTS`, run `python manage.py check --deploy`, configure HTTPS and secure cookies, configure persistent media storage and a production database, and serve collected static files. Add email verification/password reset delivery and automated tests before treating this as production-ready. Do not commit `.env`, database files, uploaded user media, or real personal information.

## Portfolio note

This repository demonstrates a learning project, not a deployed or independently audited production service. Run through registration, profile editing, creating/filtering a listing, sending a request, accepting/declining it, and marking it complete before presenting a live demo. Add screenshots and a deployment URL after you have tested and deployed your own instance.

## License

MIT — see [LICENSE](LICENSE).
