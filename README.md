# DiszkretPartner – közös backend (2 oldal + operátorok + Stripe + real-time)

Node.js (Express) + Socket.IO + Postgres backend, amit Renderre tudsz kirakni, miközben a frontend oldalak Netlify-n futnak.

## Mit tud
- 2 (vagy több) oldal kezelése **X-Site-Key** alapján (pl. `forrorandi`, `szerelmesszivek`).
- Regisztráció, bejelentkezés.
- Kredit rendszer (üzenet küldés = kredit levonás).
- Stripe checkout + webhook (kredit jóváírás).
- Operátor/supervisor login + inbox + válasz.
- **Real-time** Socket.IO események (új user, új üzenet, hozzárendelés).

## Gyors indulás (lokál)
1) `npm i`
2) Másold `.env.example` -> `.env` és töltsd ki a `DATABASE_URL`-t.
3) `npm run dev`

## Render deploy
- Hozz létre egy **Postgres** adatbázist.
- Web Service: build `npm i`, start `npm start`.
- Állítsd be az env változókat a `.env.example` alapján.

## Fontos request header
Minden API híváshoz add hozzá:
- `X-Site-Key: forrorandi` (vagy `szerelmesszivek`)

## Socket.IO kliens
Csatlakozás:
- URL: `https://YOUR-RENDER.onrender.com`
- auth: `{ token: "JWT", siteKey: "forrorandi" }`

Események:
- `user:new`
- `message:new`
- `conversation:assigned`

## API végpontok (röviden)
- `POST /v1/auth/register` (user)
- `POST /v1/auth/login` (user)
- `POST /v1/auth/staff-login` (operator/supervisor)
- `GET /v1/me`
- `GET /v1/credits/packages`
- `POST /v1/credits/checkout`
- `POST /v1/stripe/webhook`
- `POST /v1/chat/send`
- `GET /v1/operator/inbox`
- `POST /v1/operator/conversations/:id/assign`
- `POST /v1/operator/conversations/:id/reply`
