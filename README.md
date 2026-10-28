# Visa Autofill Generator

A Django web app built for a visa agency ([vdzservice.com](https://vdzservice.com/fr/)).
Agents enter each trip once (up to five travellers, their passports and family ties),
check a printable summary or PDF, and download one file: a userscript with its
configuration that the agency's browser automation uses to fill the appointment portal.

- Agency accounts by invitation link only
- Per-agency defaults (travel dates, number of travellers)
- Printable preview and PDF (ReportLab, with Arabic shaping)
- French interface (English and Arabic translations prepared)

## Run it locally

```bash
python -m venv .venv
.venv\Scripts\activate          # Windows; on Linux/macOS: source .venv/bin/activate
pip install -r requirements.txt
set DJANGO_DEBUG=1              # Linux/macOS: export DJANGO_DEBUG=1
python manage.py migrate
python manage.py createsuperuser
python manage.py runserver
```

## Production settings

Set these in the server's environment, never in the code:

| Variable | Value |
| --- | --- |
| `DJANGO_SECRET_KEY` | a long random string: `python -c "import secrets; print(secrets.token_urlsafe(50))"` |
| `DJANGO_ALLOWED_HOSTS` | `vdzservice.com,www.vdzservice.com` |
| `DJANGO_DEBUG` | leave unset (debug stays off) |

The database holds applicants' personal data (names, passports, addresses). It stays
on the server and out of this repository (`.gitignore`).

Made by Younes Ouali.
