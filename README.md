# Postiz Self-Hosted Setup

This is a self-hosted setup of Postiz configured for any Local Machine with local storage, Bluesky and X (Twitter) integration.

## Prerequisites

1. Docker Desktop for Mac
2. Node.js (recommended version: 18.x or later)
3. Gmail account (for nodemailer)
4. X (Twitter) Developer Account
5. Bluesky Account

## Setup Instructions

1. First, create the uploads directory wherever you want but here I used my Downloads folder:
```bash
mkdir -p ~/Downloads/postiz/uploads
chmod 777 ~/Downloads/postiz/uploads
```

2. Update the `.env` file with your credentials:
   - Replace `your-email@gmail.com` with your Gmail
   - Generate an [App Password](https://support.google.com/accounts/answer/185833?hl=en) for Gmail and update `EMAIL_PASS`
   - Update X API credentials from [X Developer Portal](https://developer.twitter.com/)
   - Update Bluesky credentials
   - Change the `JWT_SECRET` to a secure random string

3. Start the application:
```bash
docker-compose up -d
```

4. Check if all services are running:
```bash
docker-compose ps
```

5. Access Postiz at: http://localhost:5000

## Important Notes

- All uploads will be stored in `~/Downloads/postiz/uploads` directory
- PostgreSQL data is persisted in a Docker volume
- Redis data is persisted with AOF enabled
- The application is configured with healthchecks for all services
- Ports exposed:
  - Postiz: 5000
  - PostgreSQL: 5432 (for local development)
  - Redis: 6379 (for local development)

## Troubleshooting

If you face any issues:

1. Check logs:
```bash
docker-compose logs -f
```

2. Restart services:
```bash
docker-compose restart
```

3. Reset everything (this won't delete your uploads in Downloads folder):
```bash
docker-compose down -v
docker-compose up -d
```
