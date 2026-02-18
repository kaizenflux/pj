# Riyu's Birthday Scrapbook & Journey

A two-part interactive birthday experience: a password-protected love letter scrapbook and a 5-world AI-powered dream journey game.

## Project Structure

```
PJ/
├── src/
│   └── server.js           # Express server
├── public/
│   ├── index.html          # Love letter scrapbook (main entry)
│   ├── journey.html        # Interactive 5-world birthday journey
│   └── images/             # Photo storage
│       ├── photo1.jpg
│       ├── photo2.jpg
│       └── ...
├── .env                    # Environment variables (not in git)
├── .env.example            # Environment template
├── package.json
├── Dockerfile
├── docker-compose.yml
└── README.md
```

## Quick Start

### Local Development

1. **Install dependencies:**
   ```bash
   npm install
   ```

2. **Set up environment variables:**
   ```bash
   cp .env.example .env
   # Edit .env and add your GEMINI_API_KEY
   ```

3. **Add your photos:**
   - Place photos in `public/images/` as `photo1.jpg`, `photo2.jpg`, etc.
   - Edit `public/index.html` to update captions in the `CONFIG.photos` array

4. **Start the server:**
   ```bash
   npm start
   # Or for development with auto-reload:
   npm run dev
   ```

5. **Open in browser:**
   ```
   http://localhost:3000
   ```

### Default Passwords
- **Visitor password:** `iloveyou`
- **Admin password:** (removed - content is hardcoded)

## Customization

### Changing Content

All content is hardcoded in the HTML files. Edit these files directly:

**`public/index.html`** - Scrapbook content:
- `CONFIG.visitorPassword` - Password to enter
- `CONFIG.greeting` - Opening greeting
- `CONFIG.letterBody` - Letter text (paragraphs separated by `\n\n`)
- `CONFIG.signOff` - Sign-off text
- `CONFIG.birthdayDate` - Date display
- `CONFIG.photos` - Photo paths and captions

**`public/journey.html`** - Journey game:
- Recipient name "Riyu" appears ~15 times (search & replace)

### Adding Photos

1. Place images in `public/images/`
2. Name them `photo1.jpg`, `photo2.jpg`, etc.
3. Update captions in `public/index.html`:
   ```javascript
   photos: [
     {img:'/images/photo1.jpg', cap:'your caption here'},
     {img:'/images/photo2.jpg', cap:'another caption'},
     // ...
   ]
   ```

### Gemini API Key

The AI features require a Google Gemini API key:

1. Get a free key at: https://aistudio.google.com/apikey
2. Add to `.env`:
   ```
   GEMINI_API_KEY=AIza...your-key-here
   ```

Without an API key, the journey still works with pre-written fallback responses.

## Deployment

### Option A: DigitalOcean App Platform (Recommended)

1. Push code to GitHub
2. Go to DigitalOcean App Platform
3. Connect your GitHub repo
4. It will auto-detect Node.js
5. Add environment variable:
   - `GEMINI_API_KEY` = your API key
6. Deploy!

### Option B: DigitalOcean Droplet with Docker

1. **Create a Droplet** (Ubuntu 22.04 recommended)

2. **Install Docker:**
   ```bash
   curl -fsSL https://get.docker.com | sh
   ```

3. **Clone your repo:**
   ```bash
   git clone https://github.com/yourusername/your-repo.git
   cd your-repo
   ```

4. **Set up environment:**
   ```bash
   cp .env.example .env
   nano .env  # Add your GEMINI_API_KEY
   ```

5. **Build and run:**
   ```bash
   docker-compose up -d
   ```

6. **Set up nginx (optional, for domain/SSL):**
   ```bash
   apt install nginx certbot python3-certbot-nginx
   # Configure nginx as reverse proxy to port 3000
   ```

### Option C: Any Node.js Host

Works with Vercel, Railway, Render, Heroku, etc.

Required env var: `GEMINI_API_KEY`

## API Endpoints

| Endpoint | Method | Description |
|----------|--------|-------------|
| `/` | GET | Serves index.html (scrapbook) |
| `/journey.html` | GET | Serves journey game |
| `/api/config` | GET | Returns `{geminiKey: "..."}` |
| `/health` | GET | Health check for monitoring |

## Tech Stack

- **Backend:** Node.js + Express
- **Frontend:** Vanilla HTML/CSS/JS
- **AI:** Google Gemini API
- **Fonts:** Google Fonts (6 fonts)
- **Deployment:** Docker / DigitalOcean App Platform

## Features

### Scrapbook (`index.html`)
- Password-protected entry
- 3D animated envelope opening
- Origami paper unfold animation
- Polaroid-style photo gallery with lightbox
- Canvas-based particle effects
- Heart cursor trail
- Fireworks celebration

### Journey (`journey.html`)
- Birthday cake with candle blowing
- Wish input
- 5 unique themed worlds:
  - Barbie Core Potion Shop
  - Dream Garden
  - Star Map Observatory
  - Adventure Map
  - Mystic Apothecary
- AI-powered conversational prompts
- Vision board generator
- Personalized keepsake card

## License

MIT
