# XOhub
XO-Dating XO-Dating is a modern, responsive Flask-based dating application designed for curated matchmaking. Admins create profiles for "potentials" (ladies), while users build their own profiles, set preferences, and get algorithmically matched. Features include coin-based payments for connections and date bookings, real-time user-to-user and user-to-potential messaging, video calls, and a pink-themed, mobile-responsive UI.Features & CapabilitiesCore FeaturesUser Registration & Authentication: Secure sign-up/login with Flask-Login. Users start with 100 coins.
User Profiles: Users create/edit profiles with name, age, location, and profile picture upload.
Preferences & Matching Algorithm: Set age range, location, keywords, and orientation preferences. Semantic matching uses TF-IDF cosine similarity on bios/keywords, filtered by demographics (age, location, orientation).
Admin-Curated Potentials: Admins add lady profiles with name, age, location, build, height, orientation (straight/les), bio, photos/videos. Auto-extracts keywords for matching.
Coin System: Virtual currency for payments. Deduct 10 coins to connect, 20 for date booking. (No real payments; extendable to Paystack/Stripe.)
Discovery Feed: Home page shows top 5 matched potentials in a responsive grid.
Connections & Bookings: Pay to connect; book dates with details. Track status (pending/confirmed/completed).
Real-Time Messaging: User-to-potential (gated behind connection).
User-to-user (direct from contacts).
Supports text and voice notes via SocketIO.

Video Calls: Twilio integration for video chats (gated behind connection).
Responsive UI: Bootstrap 5 with pink theme; mobile-first grids (stacks on small screens, cards equal-height).
Admin Dashboard: View/manage users/potentials, ban/unban/delete, mod logs.
Themes: Toggle light/pink theme.
Security: Banned users blocked; online status; secure uploads.

Technical CapabilitiesBackend: Flask app factory; SQLite (switch to PostgreSQL for prod via DATABASE_URL).
Real-Time: Flask-SocketIO with eventlet for chats/voice.
AI/ML: Scikit-learn for semantic matching (TF-IDF on bios vs. prefs).
Media: Upload/resize images/videos; serve via Flask.
Deployment: Heroku-ready (gunicorn, Procfile). Ephemeral FS; use S3 for prod media.
Extensibility: Add FCM notifications, real payments, more filters (e.g., build/height in prefs).

LimitationsSQLite for dev; scale to PostgreSQL for concurrency.
Matching is bio/keyword-focused; enhance with embeddings (e.g., Sentence Transformers).
Video: Twilio placeholder; requires API keys.
No email verification; add Flask-Mail.

Installation & SetupClone/Setup:

git clone <repo>  # Or create new dir
cd xo-dating

Environment:Create .env:

SECRET_KEY=your-secret-key
DATABASE_URL=sqlite:///xo.db  # Or postgresql:// for prod
TWILIO_ACCOUNT_SID=your-sid  # Optional for video
TWILIO_API_KEY_SID=your-key-sid
TWILIO_API_KEY_SECRET=your-secret

Install & Run:

pip install -r requirements.txt
python app.py

Access: http://127.0.0.1:5000
Admin: username a@#$^, password xo***

Database:Auto-creates tables on first run.
Migrate: Run app; add sample potentials via admin.

Deploy to Heroku:Create Procfile: web: gunicorn app:create_app[0] --worker-class eventlet -w 1
runtime.txt: python-3.12.3
git push heroku main
Set config vars: heroku config:set SECRET_KEY=...

UsageAs User:Register → Complete Profile (name/age/location/photo) → Set Preferences → Browse Matches.
Connect (10 coins) → Chat/Video → Book Date (20 coins).

As Admin:Login → Admin Dashboard → Add Potential (enhanced fields, media).

Messaging:Messages page: Tabs for potentials/users.
Real-time via WebSockets; voice notes supported.

Screenshots(Placeholder: Add images of home, chat, admin.)ContributingFork, PR with tests.
Issues: Report bugs/features.

© 2025 XO-Dating Team by JayyMadd Clicke Ltd



Integrate real payment gateway

