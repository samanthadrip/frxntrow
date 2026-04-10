[frxnt_row_playlist (2).html](https://github.com/user-attachments/files/26632010/frxnt_row_playlist.2.html)
# frxntrow<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>FRXNT ROW — Playlist Builder</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Archivo:ital,wght@0,300;0,400;0,500;1,300;1,400&family=Inter:wght@400;500;600;700&family=Work+Sans:wght@300;400;500&display=swap" rel="stylesheet">
<style>
  *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }
  :root {
    --warm-white: #FAFAF5;
    --ink: #110808;
    --ice: #DCF3F8;
    --ink-60: rgba(250,250,245,0.6);
    --ink-30: rgba(250,250,245,0.3);
    --ink-12: rgba(250,250,245,0.12);
    --ink-06: rgba(250,250,245,0.06);
    --gold: #C49A6C;
    --gold-light: rgba(196,154,108,0.15);
    --sand: #DDD8C4;
    --green: #1DB954;
    --display: "Archivo", sans-serif;
    --secondary: "Inter", sans-serif;
    --sans: "Work Sans", system-ui, sans-serif;
  }
  html { scroll-behavior: smooth; }
  body { font-family: var(--sans); background: var(--ink); color: var(--warm-white); font-size: 16px; line-height: 1.6; -webkit-font-smoothing: antialiased; min-height: 100vh; }

  /* NAV */
  .nav { max-width: 1200px; margin: 0 auto; padding: 1.5rem 2.5rem; display: flex; align-items: center; justify-content: space-between; border-bottom: 1px solid var(--ink-12); }
  .nav-logo { font-family: var(--display); font-size: 13px; font-weight: 500; letter-spacing: 0.16em; text-transform: uppercase; color: var(--warm-white); }
  .nav-sub { font-size: 11px; font-weight: 300; color: var(--ink-30); letter-spacing: 0.08em; font-family: var(--secondary); }
  .nav-right { display: flex; align-items: center; gap: 1.5rem; }
  .nav-link { font-size: 11px; font-weight: 500; letter-spacing: 0.1em; text-transform: uppercase; color: var(--ink-30); text-decoration: none; font-family: var(--secondary); }
  .nav-link:hover { color: var(--gold); }
  .spotify-btn { display: flex; align-items: center; gap: 8px; background: var(--green); color: #000; font-family: var(--secondary); font-size: 11px; font-weight: 700; letter-spacing: 0.08em; text-transform: uppercase; padding: 0.5rem 1.25rem; border-radius: 2px; border: none; cursor: pointer; text-decoration: none; transition: opacity 0.2s; }
  .spotify-btn:hover { opacity: 0.85; }
  .spotify-dot { width: 8px; height: 8px; border-radius: 50%; background: #000; }

  /* AUTH SCREEN */
  .auth-screen { max-width: 600px; margin: 6rem auto; padding: 0 2.5rem; text-align: center; }
  .auth-title { font-family: var(--display); font-size: clamp(32px, 5vw, 52px); font-weight: 300; line-height: 1.1; margin-bottom: 1rem; }
  .auth-title em { font-style: italic; }
  .auth-sub { font-size: 15px; font-weight: 300; color: var(--ink-60); line-height: 1.85; margin-bottom: 2.5rem; }
  .auth-connect { display: inline-flex; align-items: center; gap: 10px; background: var(--green); color: #000; font-family: var(--secondary); font-size: 13px; font-weight: 700; letter-spacing: 0.1em; text-transform: uppercase; padding: 1rem 2rem; border-radius: 2px; border: none; cursor: pointer; transition: opacity 0.2s; text-decoration: none; }
  .auth-connect:hover { opacity: 0.85; }
  .auth-note { font-size: 12px; font-weight: 300; color: var(--ink-30); margin-top: 1.25rem; font-family: var(--secondary); }

  /* MAIN APP */
  .app { max-width: 1200px; margin: 0 auto; padding: 2.5rem; display: none; }
  .app.visible { display: block; }
  .app-grid { display: grid; grid-template-columns: 1fr 380px; gap: 2.5rem; align-items: start; }

  /* SEARCH */
  .search-wrap { margin-bottom: 2rem; }
  .search-label { font-family: var(--secondary); font-size: 10px; font-weight: 600; letter-spacing: 0.14em; text-transform: uppercase; color: var(--gold); margin-bottom: 0.75rem; }
  .search-bar { display: flex; gap: 1px; background: var(--ink-12); border-radius: 3px; overflow: hidden; }
  .search-input { flex: 1; background: rgba(250,250,245,0.04); border: none; outline: none; color: var(--warm-white); font-family: var(--sans); font-size: 15px; font-weight: 300; padding: 0.9rem 1.25rem; }
  .search-input::placeholder { color: var(--ink-30); }
  .search-btn { background: var(--gold); border: none; color: var(--ink); font-family: var(--secondary); font-size: 11px; font-weight: 700; letter-spacing: 0.1em; text-transform: uppercase; padding: 0 1.5rem; cursor: pointer; transition: opacity 0.2s; white-space: nowrap; }
  .search-btn:hover { opacity: 0.85; }

  /* RESULTS */
  .results-label { font-family: var(--secondary); font-size: 10px; font-weight: 600; letter-spacing: 0.14em; text-transform: uppercase; color: var(--ink-30); margin-bottom: 0.75rem; }
  .results-list { display: flex; flex-direction: column; gap: 1px; background: var(--ink-12); border: 1px solid var(--ink-12); border-radius: 4px; overflow: hidden; margin-bottom: 2.5rem; min-height: 60px; }
  .result-item { background: var(--ink); padding: 1rem 1.25rem; display: grid; grid-template-columns: 48px 1fr auto auto; gap: 1rem; align-items: center; transition: background 0.15s; cursor: default; }
  .result-item:hover { background: rgba(250,250,245,0.03); }
  .result-art { width: 48px; height: 48px; border-radius: 2px; object-fit: cover; background: var(--ink-12); flex-shrink: 0; }
  .result-info { min-width: 0; }
  .result-name { font-family: var(--display); font-size: 15px; font-weight: 300; color: var(--warm-white); white-space: nowrap; overflow: hidden; text-overflow: ellipsis; }
  .result-artist { font-size: 12px; font-weight: 300; color: var(--ink-30); font-family: var(--secondary); }
  .result-bpm { font-family: var(--display); font-size: 13px; font-weight: 300; font-style: italic; color: var(--ice); white-space: nowrap; text-align: right; }
  .result-zone-pill { font-family: var(--secondary); font-size: 9px; font-weight: 600; letter-spacing: 0.1em; text-transform: uppercase; padding: 3px 8px; border-radius: 2px; white-space: nowrap; }
  .result-add { background: var(--gold-light); border: 1px solid rgba(196,154,108,0.3); color: var(--gold); font-family: var(--secondary); font-size: 10px; font-weight: 700; letter-spacing: 0.08em; text-transform: uppercase; padding: 0.4rem 0.9rem; border-radius: 2px; cursor: pointer; white-space: nowrap; transition: background 0.15s; }
  .result-add:hover { background: rgba(196,154,108,0.25); }
  .sc-btn { display: block; background: rgba(255,85,0,0.1); border: 1px solid rgba(255,85,0,0.25); color: #ff5500; font-family: var(--secondary); font-size: 9px; font-weight: 700; letter-spacing: 0.08em; text-transform: uppercase; padding: 0.4rem 0.6rem; border-radius: 2px; cursor: pointer; white-space: nowrap; text-decoration: none; text-align: center; transition: background 0.15s; }
  .sc-btn:hover { background: rgba(255,85,0,0.2); }
  .result-empty { padding: 2rem; text-align: center; font-family: var(--display); font-size: 14px; font-style: italic; color: var(--ink-30); }



  /* PLAYLIST PANEL */
  .playlist-panel { position: sticky; top: 2rem; }
  .panel-header { display: flex; justify-content: space-between; align-items: center; margin-bottom: 1rem; }
  .panel-title { font-family: var(--display); font-size: 20px; font-weight: 300; color: var(--warm-white); }
  .panel-title em { font-style: italic; }
  .panel-count { font-family: var(--secondary); font-size: 11px; font-weight: 600; letter-spacing: 0.1em; text-transform: uppercase; color: var(--ink-30); }
  .panel-name-wrap { margin-bottom: 1rem; }
  .panel-name-input { width: 100%; background: rgba(250,250,245,0.04); border: 1px solid var(--ink-12); border-radius: 3px; outline: none; color: var(--warm-white); font-family: var(--display); font-size: 14px; font-weight: 300; font-style: italic; padding: 0.65rem 1rem; }
  .panel-name-input::placeholder { color: var(--ink-30); }
  .playlist-items { display: flex; flex-direction: column; gap: 1px; background: var(--ink-12); border: 1px solid var(--ink-12); border-radius: 4px; overflow: hidden; margin-bottom: 1rem; min-height: 80px; max-height: 420px; overflow-y: auto; }
  .playlist-item { background: var(--ink); padding: 0.85rem 1rem; display: grid; grid-template-columns: 1fr auto; gap: 0.75rem; align-items: center; }
  .playlist-item-left { min-width: 0; }
  .playlist-item-name { font-size: 13px; font-weight: 300; color: var(--warm-white); white-space: nowrap; overflow: hidden; text-overflow: ellipsis; font-family: var(--display); }
  .playlist-item-meta { font-size: 11px; font-weight: 300; color: var(--ink-30); font-family: var(--secondary); }
  .playlist-item-remove { background: none; border: none; color: var(--ink-30); cursor: pointer; font-size: 16px; line-height: 1; padding: 2px 4px; transition: color 0.15s; font-family: var(--display); }
  .playlist-item-remove:hover { color: rgba(240,149,149,0.8); }
  .playlist-empty { padding: 2rem 1rem; text-align: center; font-family: var(--display); font-size: 13px; font-style: italic; color: var(--ink-30); }
  .panel-actions { display: flex; flex-direction: column; gap: 1px; }
  .panel-btn { width: 100%; padding: 0.9rem; font-family: var(--secondary); font-size: 11px; font-weight: 700; letter-spacing: 0.1em; text-transform: uppercase; border-radius: 2px; cursor: pointer; transition: opacity 0.2s; border: none; }
  .panel-btn-spotify { background: var(--green); color: #000; }
  .panel-btn-spotify:hover { opacity: 0.85; }
  .panel-btn-clear { background: rgba(250,250,245,0.04); color: var(--ink-30); border: 1px solid var(--ink-12); }
  .panel-btn-clear:hover { color: var(--warm-white); }

  /* ZONE LEGEND */
  .zone-legend { display: flex; flex-direction: column; gap: 1px; background: var(--ink-12); border: 1px solid var(--ink-12); border-radius: 4px; overflow: hidden; margin-bottom: 2.5rem; }
  .zone-legend-item { background: var(--ink); padding: 0.6rem 1rem; display: flex; align-items: center; gap: 0.75rem; }
  .zone-dot { width: 8px; height: 8px; border-radius: 50%; flex-shrink: 0; }
  .zone-legend-name { font-family: var(--display); font-size: 13px; font-weight: 300; color: var(--warm-white); flex: 1; }
  .zone-legend-bpm { font-family: var(--secondary); font-size: 10px; font-weight: 600; color: var(--ink-30); letter-spacing: 0.06em; }

  .loading { text-align: center; padding: 1.5rem; font-family: var(--display); font-size: 13px; font-style: italic; color: var(--ink-30); }
  .success-msg { background: rgba(29,158,117,0.1); border-left: 3px solid #1D9E75; padding: 0.75rem 1rem; border-radius: 0 3px 3px 0; font-size: 13px; color: #1D9E75; font-family: var(--secondary); margin-top: 0.5rem; display: none; }

  @media (max-width: 900px) { .app-grid { grid-template-columns: 1fr; } .playlist-panel { position: static; } }
  @media (max-width: 600px) { .nav { padding: 1.25rem; } .app { padding: 1.25rem; } .result-item { grid-template-columns: 40px 1fr auto; } .result-zone-pill { display: none; } }
</style>
</head>
<body>

<nav class="nav">
  <div>
    <div class="nav-logo">FRXNT ROW</div>
    <div class="nav-sub">Playlist Builder</div>
  </div>
  <div class="nav-right">
    <a href="frxnt_row_manual.html" class="nav-link">← Manual</a>
    <div id="nav-spotify-status"></div>
  </div>
</nav>

<!-- AUTH SCREEN -->
<div class="auth-screen" id="auth-screen">
  <h1 class="auth-title">Build your<br><em>class arc.</em></h1>
  <p class="auth-sub">Search any song, see its BPM instantly, and build a playlist that maps directly to the FRXNT ROW zones. Connect Spotify to get started.</p>
  <a href="#" class="auth-connect" id="connect-btn">
    <svg width="16" height="16" viewBox="0 0 24 24" fill="#000"><path d="M12 0C5.4 0 0 5.4 0 12s5.4 12 12 12 12-5.4 12-12S18.66 0 12 0zm5.521 17.34c-.24.359-.66.48-1.021.24-2.82-1.74-6.36-2.101-10.561-1.141-.418.122-.779-.179-.899-.539-.12-.421.18-.78.54-.9 4.56-1.021 8.52-.6 11.64 1.32.42.18.479.659.301 1.02zm1.44-3.3c-.301.42-.841.6-1.262.3-3.239-1.98-8.159-2.58-11.939-1.38-.479.12-1.02-.12-1.14-.6-.12-.48.12-1.021.6-1.141C9.6 9.9 15 10.561 18.72 12.84c.361.181.54.78.241 1.2zm.12-3.36C15.24 8.4 8.82 8.16 5.16 9.301c-.6.179-1.2-.181-1.38-.721-.18-.601.18-1.2.72-1.381 4.26-1.26 11.28-1.02 15.721 1.621.539.3.719 1.02.419 1.56-.299.421-1.02.599-1.559.3z"/></svg>
    Connect Spotify
  </a>
  <p class="auth-note">You'll be redirected to Spotify to authorize. No data is stored.</p>
</div>

<!-- MAIN APP -->
<div class="app" id="app">
  <div class="app-grid">
    <div class="app-left">

      <!-- SEARCH -->
      <div class="search-wrap">
        <div class="search-label">Search for a track</div>
        <div class="search-bar">
          <input type="text" class="search-input" id="search-input" placeholder="Song title or artist..." />
          <button class="search-btn" id="search-btn">Search</button>
        </div>
      </div>

      <!-- ZONE LEGEND -->
      <div class="results-label">Zone reference</div>
      <div class="zone-legend" id="zone-legend"></div>

      <!-- RESULTS -->
      <div class="results-label" id="results-label" style="display:none;">Results</div>
      <div class="results-list" id="results-list" style="display:none;">
        <div class="result-empty">Search for a track above to get started</div>
      </div>



    </div>

    <!-- PLAYLIST PANEL -->
    <div class="playlist-panel">
      <div class="panel-header">
        <div class="panel-title">Your <em>playlist</em></div>
        <div class="panel-count" id="panel-count">0 tracks</div>
      </div>
      <div class="panel-name-wrap">
        <input type="text" class="panel-name-input" id="playlist-name" placeholder="Name your playlist..." />
      </div>
      <div class="playlist-items" id="playlist-items">
        <div class="playlist-empty">Add tracks from the search results</div>
      </div>
      <div class="panel-actions">
        <button class="panel-btn panel-btn-spotify" id="save-spotify-btn">Save to Spotify</button>
        <button class="panel-btn panel-btn-clear" id="clear-btn">Clear playlist</button>
      </div>
      <div class="success-msg" id="success-msg">Playlist saved to Spotify!</div>
    </div>
  </div>
</div>

<script>
const CLIENT_ID = 'f6c2fd16dad14495860a1aa10aa66d42';
const REDIRECT_URI = 'https://eloquent-liger-bef3f3.netlify.app/frxnt_row_playlist.html';
const SCOPES = 'playlist-modify-public playlist-modify-private';

const zones = [
  { name:'Heavy hill', bpmMin:40, bpmMax:58, gearMin:8, gearMax:12, color:'#7F77DD' },
  { name:'Side to side', bpmMin:57, bpmMax:69, gearMin:6, gearMax:9, color:'#D4537E' },
  { name:'Opener / warm-up', bpmMin:70, bpmMax:80, gearMin:3, gearMax:5, color:'#1D9E75' },
  { name:'Fast hill', bpmMin:66, bpmMax:79, gearMin:5, gearMax:8, color:'#D85A30' },
  { name:'Moderate jog', bpmMin:77, bpmMax:89, gearMin:3, gearMax:5, color:'#378ADD' },
  { name:'Fast jog', bpmMin:87, bpmMax:100, gearMin:2, gearMax:4, color:'#639922' },
  { name:'Crack jog', bpmMin:100, bpmMax:115, gearMin:2, gearMax:3, color:'#BA7517' },
  { name:'Run', bpmMin:115, bpmMax:140, gearMin:2, gearMax:3, color:'#E24B4A' }
];

function getZone(bpm) {
  return zones.reduce((best, z) => {
    const mid = (z.bpmMin + z.bpmMax) / 2;
    const bestMid = (best.bpmMin + best.bpmMax) / 2;
    return Math.abs(bpm - mid) < Math.abs(bpm - bestMid) ? z : best;
  });
}

let accessToken = null;
let playlist = [];

function generateRandomString(length) {
  const chars = 'ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789';
  const values = crypto.getRandomValues(new Uint8Array(length));
  return Array.from(values).map(v => chars[v % chars.length]).join('');
}

async function generateCodeChallenge(verifier) {
  const data = new TextEncoder().encode(verifier);
  const digest = await crypto.subtle.digest('SHA-256', data);
  return btoa(String.fromCharCode(...new Uint8Array(digest)))
    .replace(/\+/g,'-').replace(/\//g,'_').replace(/=+$/,'');
}

async function login() {
  const verifier = generateRandomString(128);
  const challenge = await generateCodeChallenge(verifier);
  sessionStorage.setItem('pkce_verifier', verifier);
  const params = new URLSearchParams({
    client_id: CLIENT_ID,
    response_type: 'code',
    redirect_uri: REDIRECT_URI,
    scope: SCOPES,
    code_challenge_method: 'S256',
    code_challenge: challenge
  });
  window.location.href = 'https://accounts.spotify.com/authorize?' + params.toString();
}

async function exchangeCode(code) {
  const verifier = sessionStorage.getItem('pkce_verifier');
  const res = await fetch('https://accounts.spotify.com/api/token', {
    method: 'POST',
    headers: { 'Content-Type': 'application/x-www-form-urlencoded' },
    body: new URLSearchParams({
      client_id: CLIENT_ID,
      grant_type: 'authorization_code',
      code,
      redirect_uri: REDIRECT_URI,
      code_verifier: verifier
    })
  });
  const data = await res.json();
  return data.access_token;
}

function showApp() {
  document.getElementById('auth-screen').style.display = 'none';
  document.getElementById('app').classList.add('visible');
  document.getElementById('nav-spotify-status').innerHTML = `<span style="font-family:var(--secondary);font-size:11px;font-weight:600;letter-spacing:0.08em;text-transform:uppercase;color:var(--green);">Connected</span>`;
}

function buildZoneLegend() {
  const el = document.getElementById('zone-legend');
  zones.forEach(z => {
    const item = document.createElement('div');
    item.className = 'zone-legend-item';
    item.innerHTML = `<div class="zone-dot" style="background:${z.color}"></div><div class="zone-legend-name">${z.name}</div><div class="zone-legend-bpm">${z.bpmMin}–${z.bpmMax} BPM</div>`;
    el.appendChild(item);
  });
}

async function search(query) {
  const list = document.getElementById('results-list');
  const label = document.getElementById('results-label');
  list.style.display = 'flex';
  label.style.display = 'block';
  list.innerHTML = `<div class="loading">Searching...</div>`;

  try {
    const res = await fetch(`https://api.spotify.com/v1/search?q=${encodeURIComponent(query)}&type=track&limit=8`, {
      headers: { 'Authorization': `Bearer ${accessToken}` }
    });
    const data = await res.json();
    if (!data.tracks || !data.tracks.items.length) {
      list.innerHTML = `<div class="result-empty">No results found</div>`;
      return;
    }
    const tracks = data.tracks.items;
    const ids = tracks.map(t => t.id).join(',');
    const featRes = await fetch(`https://api.spotify.com/v1/audio-features?ids=${ids}`, {
      headers: { 'Authorization': `Bearer ${accessToken}` }
    });
    const featData = await featRes.json();
    list.innerHTML = '';
    tracks.forEach((track, i) => {
      const feat = featData.audio_features[i];
      const bpm = feat ? Math.round(feat.tempo) : null;
      const zone = bpm ? getZone(bpm) : null;
      const art = track.album.images[2] ? track.album.images[2].url : '';
        const scQuery = encodeURIComponent(track.name + ' ' + track.artists[0].name + ' remix');
      const item = document.createElement('div');
      item.className = 'result-item';
      item.innerHTML = `
        <img class="result-art" src="${art}" alt="">
        <div class="result-info">
          <div class="result-name">${track.name}</div>
          <div class="result-artist">${track.artists.map(a=>a.name).join(', ')}</div>
        </div>
        ${bpm ? `<div style="text-align:right"><div class="result-bpm">${bpm} BPM</div><div class="result-zone-pill" style="background:${zone.color}22;color:${zone.color};margin-top:3px;">${zone.name}</div></div>` : '<div class="result-bpm" style="color:var(--ink-30)">—</div>'}
        <div style="display:flex;flex-direction:column;gap:4px;">
          <button class="result-add" onclick="addTrack('${track.id}','${track.name.replace(/'/g,"\\'")}','${track.artists[0].name.replace(/'/g,"\\'")}',${bpm},'${track.uri}')">Add</button>
          <a href="https://soundcloud.com/search?q=${scQuery}" target="_blank" class="sc-btn">SoundCloud ↗</a>
        </div>
      `;
      list.appendChild(item);
    });
  } catch(e) {
    list.innerHTML = `<div class="result-empty">Something went wrong. Try again.</div>`;
  }
}

function addTrack(id, name, artist, bpm, uri) {
  if (playlist.find(t => t.id === id)) return;
  playlist.push({ id, name, artist, bpm, uri, zone: bpm ? getZone(bpm) : null });
  renderPlaylist();
}

function removeTrack(id) {
  playlist = playlist.filter(t => t.id !== id);
  renderPlaylist();
}

function renderPlaylist() {
  const el = document.getElementById('playlist-items');
  const count = document.getElementById('panel-count');
  count.textContent = `${playlist.length} track${playlist.length !== 1 ? 's' : ''}`;
  if (!playlist.length) {
    el.innerHTML = `<div class="playlist-empty">Add tracks from the search results</div>`;
    return;
  }
  el.innerHTML = '';
  playlist.forEach(t => {
    const item = document.createElement('div');
    item.className = 'playlist-item';
    item.innerHTML = `
      <div class="playlist-item-left">
        <div class="playlist-item-name">${t.name}</div>
        <div class="playlist-item-meta">${t.artist}${t.bpm ? ` · ${t.bpm} BPM` : ''}${t.zone ? ` · ${t.zone.name}` : ''}</div>
      </div>
      <button class="playlist-item-remove" onclick="removeTrack('${t.id}')">×</button>
    `;
    el.appendChild(item);
  });
}



async function saveToSpotify() {
  if (!playlist.length) return;
  const name = document.getElementById('playlist-name').value || 'FRXNT ROW Class';
  const btn = document.getElementById('save-spotify-btn');
  btn.textContent = 'Saving...';
  btn.style.opacity = '0.6';
  try {
    const meRes = await fetch('https://api.spotify.com/v1/me', { headers: { 'Authorization': `Bearer ${accessToken}` } });
    const me = await meRes.json();
    const plRes = await fetch(`https://api.spotify.com/v1/users/${me.id}/playlists`, {
      method: 'POST',
      headers: { 'Authorization': `Bearer ${accessToken}`, 'Content-Type': 'application/json' },
      body: JSON.stringify({ name, description: 'Built with FRXNT ROW Playlist Builder', public: false })
    });
    const pl = await plRes.json();
    await fetch(`https://api.spotify.com/v1/playlists/${pl.id}/tracks`, {
      method: 'POST',
      headers: { 'Authorization': `Bearer ${accessToken}`, 'Content-Type': 'application/json' },
      body: JSON.stringify({ uris: playlist.map(t => t.uri) })
    });
    btn.textContent = 'Save to Spotify';
    btn.style.opacity = '1';
    const msg = document.getElementById('success-msg');
    msg.textContent = `"${name}" saved to your Spotify.`;
    msg.style.display = 'block';
    setTimeout(() => msg.style.display = 'none', 4000);
  } catch(e) {
    btn.textContent = 'Save to Spotify';
    btn.style.opacity = '1';
    alert('Something went wrong saving to Spotify. Try again.');
  }
}

document.getElementById('connect-btn').onclick = login;
document.getElementById('search-btn').onclick = () => {
  const q = document.getElementById('search-input').value.trim();
  if (q) search(q);
};
document.getElementById('search-input').addEventListener('keydown', e => {
  if (e.key === 'Enter') { const q = e.target.value.trim(); if (q) search(q); }
});
document.getElementById('save-spotify-btn').onclick = saveToSpotify;
document.getElementById('clear-btn').onclick = () => { playlist = []; renderPlaylist(); };

buildZoneLegend();

(async () => {
  const params = new URLSearchParams(window.location.search);
  const code = params.get('code');
  if (code) {
    window.history.replaceState(null, null, window.location.pathname);
    try {
      accessToken = await exchangeCode(code);
      if (accessToken) showApp();
    } catch(e) {
      console.error('Auth error', e);
    }
  }
})();
</script>
</body>
</html>
