# Board Game Club Website — Setup Guide

## Repository structure

```
your-repo/
├── index.html        ← the website
├── images/
│   ├── logo.png      ← your club logo
│   ├── about.jpg     ← photo for the About section
│   ├── gallery1.jpg  ← game night photos
│   └── ...
└── README.md
```

---

## 1 · GitHub Pages deployment

1. Create a new GitHub repository (e.g. `boardgame-club`)
2. Push this folder to the `main` branch
3. Go to **Settings → Pages**
4. Source: **Deploy from a branch** → branch `main`, folder `/` (root)
5. Save — your site will be live at `https://YOUR_USERNAME.github.io/boardgame-club/`

---

## 2 · Add your assets

Open `index.html` and update the `CONFIG` object at the top of the `<script>`:

| Field | What to change |
|---|---|
| `clubName` | Your club's name |
| `tagline` | Hero tagline text |
| `contactEmail` | Email for the Join button |
| `members[]` | Array of member objects — name, initials, BGG username |
| `galleryImages[]` | Filenames of photos inside `/images/` |

Also replace placeholder text in the HTML:
- Hero `<h1>` — your club motto
- About section `<p>` paragraphs — your description
- Stats numbers (30+, 2×, 200+) — your real numbers
- Footer copyright name

---

## 3 · Google Calendar integration

### Step A — Make your calendar public
1. Open Google Calendar → find your club calendar → three-dot menu → **Settings and sharing**
2. Under **Access permissions** → tick **Make available to public**

### Step B — Get your Calendar ID
In the same settings page, scroll to **Integrate calendar** → copy the **Calendar ID**
(looks like `abc123@group.calendar.google.com` or your Gmail for the primary calendar)

### Step C — Create a Google API key (free)
1. Go to [console.cloud.google.com](https://console.cloud.google.com)
2. Create a new project (e.g. "BoardgameClub")
3. Go to **APIs & Services → Library** → search **Google Calendar API** → Enable
4. Go to **APIs & Services → Credentials** → **Create Credentials → API key**
5. Copy the key
6. (Recommended) Click **Restrict key** → under API restrictions, select **Google Calendar API** only

### Step D — Add to the website
In `index.html`, find the `CONFIG` object and replace:
```js
googleCalendarId: "YOUR_CALENDAR_ID@group.calendar.google.com",
googleApiKey:     "YOUR_GOOGLE_API_KEY",
```

> The API key is safe to expose in client-side JS as long as you restrict it to the Calendar API
> and optionally to your GitHub Pages domain (HTTP referrer restriction in Google Cloud Console).

---

## 4 · Customise colours & fonts

At the top of `index.html`, edit the CSS variables:

```css
:root {
  --accent:  #C0392B;  /* main colour (red by default) */
  --accent2: #2C3E50;  /* dark colour (navy by default) */
  --light:   #FDF8F0;  /* page background */
}
```

---

## 5 · Demo mode

If `googleCalendarId` or `googleApiKey` still contain `YOUR_`, the site runs in **demo mode**
and shows three placeholder events. This is fine for testing the layout before you get your API key.
