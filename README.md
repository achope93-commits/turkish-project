[README.md](https://github.com/user-attachments/files/31083235/README.md)
# Türkçe Konuş — deploy pe Netlify

## Structura proiectului

├── index.html                     ← frontend-ul (platforma)
├── netlify.toml                   ← configurare Netlify
└── netlify/
    └── functions/
        └── chat.js                ← backend-ul: ține cheia API în siguranță

## De ce ai nevoie de acest backend
`index.html` nu mai apelează direct `api.anthropic.com`. În schimb, trimite
request-urile către `/.netlify/functions/chat`, care rulează pe server,
adaugă cheia ta API (păstrată secretă, ca variabilă de mediu) și abia apoi
vorbește cu Claude. Așa cheia nu ajunge niciodată în browser-ul utilizatorului.

## Pași de deploy

### 1. Obține o cheie API Anthropic
Mergi pe console.anthropic.com, creează un cont (sau folosește unul existent)
și generează o cheie API din secțiunea API Keys. Reține că folosirea API-ului
e plătită separat de un abonament Claude.ai — vei avea nevoie de credit
adăugat în cont.

### 2. Urcă proiectul pe Netlify
Cel mai simplu mod:
- Creează un repo nou pe GitHub și pune fișierele din acest folder în el
- Pe app.netlify.com → Add new site → Import an existing project
- Conectează repo-ul; Netlify va detecta automat netlify.toml

### 3. Adaugă cheia API ca variabilă de mediu
În Netlify: Site settings → Environment variables → Add a variable
- Key: ANTHROPIC_API_KEY
- Value: cheia ta de la pasul 1

Apoi fă un redeploy al site-ului (Environment variables noi necesită
un deploy nou ca să fie preluate).

### 4. Gata
Site-ul tău va fi live la un URL de tipul nume-random.netlify.app.
Poți seta ulterior un domeniu propriu din Domain settings.

## Cost
Netlify: gratuit pentru trafic mic. Anthropic API: se plătește per token
folosit — pentru conversații scurte de exersare, costul e de obicei sub
un cent per schimb de mesaje.
