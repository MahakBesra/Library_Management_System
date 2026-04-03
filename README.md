# Library Management System

A Flask-based library management web app with multi-role authentication (admin, employee, member), book and reservation management, fines, and vendor handling.

## 🚀 Features

- User roles: Admin, Employee, Member
- Login/logout/register (member registration)
- Role-based dashboards and access control
- CRUD for books, authors, publishers, vendors
- Issue, return, reservation, and fine tracking
- MySQL backend using `mysql-connector-python`
- Session-based login state

## 🧩 Tech stack

- Python 3.11+ (work with 3.13)
- Flask 3.0
- MySQL (Railway free tier sample)
- Jinja2 templates (in `templates/`)
- CSS in `static/css/`

## 📦 Setup

1. Clone repository:

```bash
git clone https://github.com/<your-org>/Library_management_system.git
cd Library_management_system
```

2. Create venv and install:

```bash
python -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

3. Create a MySQL database and user (or use Railway):

- Database name: `librarys_management_system` (as in config default)
- Tables and sample data are in `mysql.sql`

4. Apply schema:

```bash
mysql -u <user> -p < library.sql
# or use your GUI with mysql.sql content.
```

5. Configure environment

Create `.env` or environment variables:

```bash
export SECRET_KEY='super-secret'
export MYSQL_HOST='nozomi.proxy.rlwy.net'
export MYSQL_PORT='29951'
export MYSQL_USER='root'
export MYSQL_PASSWORD='wUiUFYWLRpyFsdLuLhsbQqCzFHPmlIMw'
export MYSQL_DATABASE='librarys_management_system'
```

6. Optional: edit `config.py` defaults if not using env variables.

## ▶️ Run locally

```bash
source .venv/bin/activate
python main.py
```

Open http://127.0.0.1:5000/login

## 🧪 Useful default credentials (from `mysql.sql`)

- Admin: `admin` / `admin123`
- Member: `user1` / `user123`
- Employee: `employee1` / `employee123`

## 🔐 Security notes

- Password hashing is supported via Werkzeug (`generate_password_hash`, `check_password_hash`).
- Some sample seeded rows have plaintext passwords in SQL; migrate them to hashed values.
- Add CSRF protection (Flask-WTF) for production.
- Add rate-limiting/lockout to prevent brute-force login.

## � Troubleshooting

- **DB Connection Issues**: The app includes retry logic for Railway DB drops. If 500 errors on login, check Railway logs and DB status.
- **Passwords**: Use hashed passwords in production; sample data has some plaintext for testing.
- **Sessions**: Configure `SECRET_KEY` securely.

## 🚢 Deploying on Railway (Free)

1. Create/sign in to [Railway.app](https://railway.app).

2. Create a new project and add a MySQL database (free tier included).

3. Connect your GitHub repo to the project.

4. Railway will auto-detect Python and use `requirements.txt`.

5. Optional: Set custom start command in Railway settings: `gunicorn app:app --bind 0.0.0.0:$PORT`

6. Set environment variables in Railway dashboard (Variables tab):
   - `SECRET_KEY`: your-secret-key
   - `MYSQL_HOST`: (auto-provided by Railway DB)
   - `MYSQL_PORT`: (auto)
   - `MYSQL_USER`: (auto)
   - `MYSQL_PASSWORD`: (auto)
   - `MYSQL_DATABASE`: (auto)

6. Deploy: Railway builds and runs automatically.

7. Apply `mysql.sql` to the DB (use Railway's DB console or connect via MySQL client).

Note: Free tier sleeps after inactivity; first load may be slow. DB is persistent.

## 🧰 Optional improvements

- Use `flask_mysqldb` or `SQLAlchemy` for cleaner ORM queries.
- Fix role table selection to avoid injection risks (already safe via map).
- Add logging to user login attempts, and health-check route.

## 📚 License

MIT (customize as needed).