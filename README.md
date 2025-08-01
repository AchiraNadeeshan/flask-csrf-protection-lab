# Flask CSRF Protection Lab

This lab demonstrates how Cross-Site Request Forgery (CSRF) attacks work in web applications and how to defend against them using `Flask-WTF`.

## Directory Structure

```
.
├── app.py                  # Main Flask application
├── requirements.txt        # Python dependencies
├── users.db                # SQLite database for user data
├── venv/                   # Python virtual environment
├── templates/              # HTML templates (home, login, profile, etc.)
│   ├── change_password.html
│   ├── home.html
│   ├── login.html
│   └── profile.html
├── csrf_exploit/          # Malicious HTML files to simulate CSRF attacks
│   ├── exploit.html
│   └── exploit_password.html
├── .gitignore
└── .git/
```

## Setup

1. **Clone the repository** and navigate into it.

2. **Create a virtual environment** (if not already set up):

   ```bash
   python3 -m venv venv
   source venv/bin/activate   # On Windows: venv\Scripts\activate
   ```

3. **Install dependencies**:

   ```bash
   pip install -r requirements.txt
   ```

4. **Start the Flask server**:

   ```bash
   python3 app.py
   ```

   If port `3000` is already in use, change it to another port (e.g., `3001`) inside `app.py`.

5. **Visit the app**:
   Open your browser at: [http://127.0.0.1:3000](http://127.0.0.1:3000)

## Testing CSRF Vulnerability

To simulate CSRF attacks:

1. Checkout the vulnerable version:

   ```bash
   git checkout 5680c23
   ```

2. Start the app again and log in using valid credentials (e.g., `admin` / `secret`).

3. In another terminal, navigate to the `csrf_exploit/` folder:

   ```bash
   cd csrf_exploit
   python3 -m http.server 8001
   ```

4. In the same browser (same session), visit:

   * [http://127.0.0.1:8001/exploit.html](http://127.0.0.1:8001/exploit.html)
   * [http://127.0.0.1:8001/exploit\_password.html](http://127.0.0.1:8001/exploit_password.html)

5. Check if the profile email or password was changed without user consent.

## Testing CSRF Protection

To test the secured version:

1. Checkout the protected version:

   ```bash
   git checkout bb158c9
   ```

2. Install any dependencies (if needed) and restart the server:

   ```bash
   pip install -r requirements.txt
   python3 app.py
   ```

3. Repeat the same exploit steps. The CSRF attacks should now fail with a CSRF token error or no change to data.

## License

This project is done for Application Security Module Course work and only for educational purposes only.