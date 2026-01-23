# NYT Front Page Daily Email

Automatically delivers the New York Times front page PDF to your inbox every morning via GitHub Actions.

## Setup Instructions

### 1. Create a new GitHub repository

Create a new repository (can be private) and push this folder's contents to it.

### 2. Set up Gmail App Password

Since this uses Gmail to send emails, you'll need an App Password (regular passwords won't work with 2FA):

1. Go to [Google Account Security](https://myaccount.google.com/security)
2. Enable 2-Step Verification if not already enabled
3. Go to [App Passwords](https://myaccount.google.com/apppasswords)
4. Select "Mail" and "Other (Custom name)" → name it "GitHub Actions"
5. Copy the 16-character password generated

### 3. Add GitHub Secrets

In your repository, go to **Settings → Secrets and variables → Actions** and add:

| Secret Name | Value |
|-------------|-------|
| `GMAIL_USERNAME` | Your full Gmail address (e.g., `yourname@gmail.com`) |
| `GMAIL_APP_PASSWORD` | The 16-character App Password from step 2 |

### 4. Enable GitHub Actions

Actions should be enabled by default. If not, go to **Actions** tab and enable them.

### 5. Test It

1. Go to **Actions** tab
2. Click on "NYT Front Page Daily"
3. Click "Run workflow" → "Run workflow"
4. Check your email!

## Schedule

The workflow runs daily at **7:00 AM EST** (12:00 UTC). 

To change the time, edit the cron expression in `.github/workflows/nyt-frontpage.yml`:

```yaml
schedule:
  - cron: '0 12 * * *'  # Currently 12:00 UTC = 7:00 AM EST
```

[Cron schedule reference](https://crontab.guru/)

## Alternative: Use a Different Email Service

If you prefer not to use Gmail, you can swap out the SMTP settings:

**Outlook/Hotmail:**
```yaml
server_address: smtp-mail.outlook.com
server_port: 587
```

**SendGrid (free tier available):**
```yaml
server_address: smtp.sendgrid.net
server_port: 587
username: apikey
password: ${{ secrets.SENDGRID_API_KEY }}
```

## Troubleshooting

- **PDF not found**: The front page PDF may not be available until mid-morning. Try adjusting the schedule later.
- **Email not sending**: Double-check your Gmail App Password and ensure "Less secure app access" isn't blocking it.
- **Check Actions logs**: Go to Actions tab to see detailed logs of each run.

## Cost

This is completely free:
- GitHub Actions: Free for public repos, 2,000 minutes/month for private repos
- Gmail SMTP: Free

## License

MIT
