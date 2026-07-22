# Deployment Guide — Where is My Faculty

Free deployment: **Backend on Render** + **Frontend on Netlify**

---

## Step 1 — Push changes to GitHub

```bash
git add .
git commit -m "deploy: add render.yaml, netlify.toml, config.js, update API URLs"
git push
```

---

## Step 2 — Deploy Backend on Render (free)

1. Go to [https://render.com](https://render.com) and sign in (use GitHub login)
2. Click **New → Web Service**
3. Connect your repo: `shreyagoyal9/Where-is-My-Faculty`
4. Render will auto-detect `render.yaml` — confirm the settings:
   - **Root Directory**: `backend`
   - **Build Command**: `npm install`
   - **Start Command**: `node index.js`
5. Under **Environment Variables**, add:
   - `MONGO_URI` → `mongodb+srv://shansit007:Shansit13555@universitycluster.n9xx7pn.mongodb.net/?retryWrites=true&w=majority&appName=UniversityCluster`
   - `JWT_SECRET` → `yourSuperSecretKey123`
6. Click **Create Web Service**
7. Wait ~2 minutes for the first deploy. Your backend URL will be something like:
   `https://where-is-my-faculty.onrender.com`

> **Copy this URL** — you'll need it in Step 3.

---

## Step 3 — Update frontend config with your Render URL

Open `frontend/public/js/config.js` and replace the URL:

```js
const API_URL = "https://where-is-my-faculty.onrender.com"; // ← paste your actual Render URL here
```

Then push again:
```bash
git add frontend/public/js/config.js
git commit -m "config: set production backend URL"
git push
```

---

## Step 4 — Deploy Frontend on Netlify (free)

1. Go to [https://netlify.com](https://netlify.com) and sign in (use GitHub login)
2. Click **Add new site → Import an existing project**
3. Choose GitHub → select `shreyagoyal9/Where-is-My-Faculty`
4. Netlify auto-reads `netlify.toml`, so settings are pre-filled:
   - **Publish directory**: `frontend/public`
   - No build command needed (static HTML)
5. Click **Deploy site**
6. Your site will be live at something like:
   `https://where-is-my-faculty.netlify.app`

---

## Notes

- Render free tier **spins down after 15 min of inactivity** — first request after idle takes ~30 seconds.
- Both services redeploy automatically on every `git push`.
- To use a custom domain, configure it in Render/Netlify dashboard settings.
