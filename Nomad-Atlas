<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Nomad Atlas</title>

<link rel="manifest" href="data:application/json,{
  &quot;name&quot;:&quot;Nomad Atlas&quot;,
  &quot;short_name&quot;:&quot;Atlas&quot;,
  &quot;display&quot;:&quot;standalone&quot;,
  &quot;background_color&quot;:&quot;#0d0f12&quot;,
  &quot;theme_color&quot;:&quot;#0d0f12&quot;
}">

<link rel="stylesheet" href="https://unpkg.com/leaflet@1.9.4/dist/leaflet.css"/>

<style>
:root{
  --bg:#0d0f12;
  --card:#151922;
  --text:#e6e6eb;
  --muted:#9aa0aa;
  --accent:#4da3ff;
  --border:#23283a;
}

*{box-sizing:border-box;font-family:system-ui}

body{margin:0;background:var(--bg);color:var(--text)}

header{padding:1.2rem;text-align:center;border-bottom:1px solid var(--border)}

#map{height:45vh}

.panel{padding:1rem;border-top:1px solid var(--border);background:var(--card)}

input,textarea,select,button{
  width:100%;margin-top:.5rem;padding:.7rem;
  background:#0f1320;color:var(--text);
  border:1px solid var(--border);border-radius:8px
}

button{background:var(--accent);color:#000;font-weight:600;cursor:pointer}

.small{font-size:.85rem;color:var(--muted)}

.badge{font-size:.7rem;padding:.2rem .4rem;background:#1e253a;border-radius:6px}

.pro{color:#ffd166}
</style>
</head>

<body>

<header>
  <h2>Nomad Atlas</h2>
  <p class="small">Plan trips. Capture memories. Share the journey.</p>
</header>

<div id="map"></div>

<div class="panel">
  <h3>✨ Pro Plans</h3>
  <p class="small">
    Unlimited trips & pins • Public profile • AI trip optimizer<br>
    Free trial included • Cancel anytime
  </p>

  <button onclick="upgrade('weekly')">Pro Weekly – $1.99 (1-day trial)</button>
  <button onclick="upgrade('monthly')">Pro Monthly – $5.99 (2-day trial)</button>
  <button onclick="upgrade('yearly')">⭐ Pro Yearly – $49.99</button>
  <button onclick="upgrade('lifetime')">💎 Lifetime Pro – $79 (One-time)</button>

  <button onclick="manageSubscription()">Manage Subscription</button>

  <p class="small" id="proStatus"></p>
</div>

<footer class="panel small">
  Secure payments via Stripe • Cancel anytime • Data stored locally
</footer>

<script src="https://unpkg.com/leaflet@1.9.4/dist/leaflet.js"></script>

<script>
/* ---------------- CONFIG ---------------- */
const STRIPE_LINKS = {
  weekly:   "https://buy.stripe.com/WEEKLY_LINK",
  monthly:  "https://buy.stripe.com/MONTHLY_LINK",
  yearly:   "https://buy.stripe.com/YEARLY_LINK",
  lifetime: "https://buy.stripe.com/LIFETIME_LINK"
};

const STRIPE_PORTAL =
  "https://billing.stripe.com/p/login/PORTAL_LINK";

/* ---------------- STATE ---------------- */
const state = {
  pro: localStorage.getItem("pro")==="true",
  plan: localStorage.getItem("pro_plan")
};

/* ---------------- MAP ---------------- */
const map=L.map("map").setView([20,0],2);
L.tileLayer("https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png").addTo(map);

/* ---------------- PAYMENTS ---------------- */
function upgrade(plan){
  localStorage.setItem("pro_plan",plan);
  window.location.href = STRIPE_LINKS[plan];
}

function manageSubscription(){
  window.location.href = STRIPE_PORTAL;
}

/* ---------------- UNLOCK ---------------- */
const params=new URLSearchParams(location.search);

if(params.get("pro")==="success" || params.get("pro")==="lifetime"){
  localStorage.setItem("pro","true");
  localStorage.setItem("pro_since",new Date().toISOString());
  alert("🎉 Pro unlocked! Welcome to Nomad Atlas Pro.");
  history.replaceState({},document.title,location.pathname);
}

/* ---------------- UI ---------------- */
function updateUI(){
  const plan=localStorage.getItem("pro_plan");
  proStatus.textContent = state.pro
    ? `Pro active (${plan || "subscription"})`
    : "Free tier";
}
updateUI();
</script>

</body>
</html>
