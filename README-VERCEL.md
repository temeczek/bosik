# Zlecenka na Vercel

Struktura repozytorium (dokładnie tak, bez dodatkowego folderu na górze):

    api/index.js
    public/index.html
    public/admin.html
    public/legal.html
    vercel.json
    package.json

## 1. Baza (Turso, SQLite w chmurze)
1. Załóż konto na turso.tech i utwórz bazę (np. `zlecenka`).
2. Skopiuj **URL bazy** (zaczyna się od `libsql://`) i wygeneruj **token dostępu**.

## 2. Zmienne środowiskowe w Vercel (Settings > Environment Variables)
- `TURSO_DATABASE_URL`, `TURSO_AUTH_TOKEN`
- `BASE_URL` = adres strony, np. `https://twoj-projekt.vercel.app`
- `ADMIN_TOKEN` = długi losowy ciąg (hasło do /admin)
- opcjonalnie: `STRIPE_SECRET_KEY`, `STRIPE_WEBHOOK_SECRET`, `RESEND_API_KEY`, `MAIL_FROM`, `GOOGLE_CLIENT_ID`, `GOOGLE_CLIENT_SECRET`

## 3. Deploy
Import repozytorium w Vercel (Framework: Other, bez komendy build). Po zmianie zmiennych zrób *Redeploy*.
Tabele tworzą się same przy pierwszym żądaniu.

## Różnice względem wersji na serwerze
- Brak automatycznych kopii zapasowych w aplikacji (kopie robi Turso).
- Limity zapytań działają osobno w każdej instancji funkcji, więc są słabsze.
- Powiadomienia o zleceniach: do 30 maili na zlecenie, wysyłane przed zakończeniem żądania.
