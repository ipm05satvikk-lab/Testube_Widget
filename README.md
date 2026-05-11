# Root Labs Test Tube Overlay

A gamified engagement widget that gives the audience a reason to tap the product link. The tube fills as clicks come in, and milestones unlock discount tiers along the way.

## What it looks like

**Overlay (bottom-right corner of stream):**
- Glass test tube with green liquid that rises as the audience engages
- Bubbles and beads float inside the tube for visual interest
- Four milestone markers next to the tube — light up gold when reached
- Stats below: current clicks / target, fill percentage, "Tap the product link to fill the tube" CTA

**Producer panel (second device):**
- TikTok username field — connects to the live and auto-fills the tube from likes (optional)
- Quick-add buttons (+1, +5, +10, +25, +50, +100) for manual click entry
- Set target buttons (200, 500, 1000, 2000)
- Host script line that updates based on current fill level
- Reset button (between mega loops)
- "Auto-fill demo (5 sec)" button — for rehearsal

## What's inside
```
server.js             - Backend (Node.js, Express, Socket.io)
public/overlay.html   - Stream overlay (goes in TikTok LIVE Studio)
public/producer.html  - Control panel (second device)
package.json          - Dependencies
```

## Setup

### 1. Install
```
npm install
```

### 2. Test locally
```
node server.js
```
Open http://localhost:3000/overlay.html and http://localhost:3000/producer.html in two tabs.

### 3. Deploy to Railway
```
npm install -g @railway/cli
railway login
railway init
railway up
```

### 4. Optional: auto-connect to a TikTok creator's live
In Railway dashboard, add environment variable:
```
TIKTOK_USERNAME=the_creator_going_live
```
This auto-fills the tube from real likes. The creator MUST be live before the server starts.

### 5. Add to TikTok LIVE Studio
1. Open LIVE Studio
2. Click "+" to add source → select "Link"
3. Paste: `https://your-railway-url.up.railway.app/overlay.html`
4. Position in the BOTTOM-RIGHT corner

### 6. Open producer on second device
`https://your-railway-url.up.railway.app/producer.html`

## How it works during the live

- Likes from the connected TikTok account automatically add to the tube (if username is configured)
- Producer manually clicks +clicks buttons when real orders come in on Seller Center
- At 25%: Flash sale unlocks (20% off)
- At 50%: Bundle deal drops (25% off 2-pack)
- At 75%: Free shipping unlocks
- At 100%: Max potency deal (30% off everything)
- Each milestone fires a burst animation
- Host reads the producer's "HOST READS THIS" line, which updates as the fill changes
- Reset between mega loops to restart the gamification

## Using with OBS instead
Add Browser Source → URL: your-railway-url/overlay.html → Width 340 Height 500
