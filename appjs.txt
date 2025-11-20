// Utility per nascondere sezioni
function hideAll() {
  document.getElementById("summary").classList.add("hidden");
  document.getElementById("shop").classList.add("hidden");
  document.getElementById("events").classList.add("hidden");
  document.getElementById("analytics").classList.add("hidden");
}

// Carica il summary dal backend
async function loadSummary() {
  hideAll();
  document.getElementById("summary").classList.remove("hidden");
  const res = await fetch("http://127.0.0.1:8081/2/summary");
  const data = await res.json();
  document.getElementById("summary-data").innerHTML = `
    <p>Status: ${data.status}</p>
    <p>Moduli attivi: ${data.modules.join(", ")}</p>
    <p>Uptime: ${Math.floor(data.uptime)}s</p>
    <p>Timestamp: ${data.timestamp}</p>
  `;
  renderChart(data.modules.length);
}

// Shop
function loadShop() {
  hideAll();
  document.getElementById("shop").classList.remove("hidden");
  document.getElementById("shop-items").innerHTML = `
    <ul>
      <li>Booster x2 – 100 FNXM</li>
      <li>Auto-clicker – 250 FNXM</li>
      <li>Pass Stagionale – 500 FNXM</li>
    </ul>
  `;
}

// Eventi
function loadEvents() {
  hideAll();
  document.getElementById("events").classList.remove("hidden");
  document.getElementById("event-list").innerHTML = `
    <ul>
      <li>Happy Hour – x2 clicker</li>
      <li>Tap Frenzy – x5 mobile</li>
      <li>Weekend Boost – x1.5 watcher</li>
    </ul>
  `;
}

// Analitiche
function loadAnalytics() {
  hideAll();
  document.getElementById("analytics").classList.remove("hidden");
  document.getElementById("analytics-data").innerHTML = `
    <p>Engagement: 85%</p>
    <p>Economia: 1200 FNXM spesi nello shop</p>
    <p>Stabilità: 98% shares valide</p>
    <p>Conversioni: 35% utenti hanno acquistato booster</p>
  `;
}

// Grafico con Chart.js
function renderChart(modCount) {
  const ctx = document.getElementById('hashChart').getContext('2d');
  new Chart(ctx, {
    type: 'bar',
    data: {
      labels: ['Clicker', 'Typer', 'Watcher', 'GPU', 'CPU'],
      datasets: [{
        label: 'Hashrate simulato',
        data: [modCount*10, modCount*8, modCount*6, modCount*12, modCount*15],
        backgroundColor: '#00ffcc'
      }]
    }
  });
}

// Carica subito il summary
window.onload = loadSummary;
