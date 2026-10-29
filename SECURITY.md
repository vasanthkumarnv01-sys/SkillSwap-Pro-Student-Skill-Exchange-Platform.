# Security notes

- Keep `DJANGO_SECRET_KEY` private and use a different random key per deployment.
- Disable debug mode outside local development and set `DJANGO_ALLOWED_HOSTS` explicitly.
- Do not commit `.env`, local SQLite databases, uploaded media, credentials, or real student data.
- Keep Django and installed dependencies patched.
- Use HTTPS and secure cookie settings when deployed.
- This portfolio project is not a security-audited production service.
