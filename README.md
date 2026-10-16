
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>ProductPilot | Product Management Dashboard</title>
<style>
:root {
  --bg: #f5f7fb;
  --card: #ffffff;
  --text: #172033;
  --muted: #687386;
  --primary: #5146e5;
  --border: #e5e9f2;
}
* { box-sizing: border-box; }
body {
  margin: 0;
  font-family: Inter, Arial, sans-serif;
  background: var(--bg);
  color: var(--text);
}
header {
  background: #171b31;
  color: white;
  padding: 22px 6%;
  display: flex;
  justify-content: space-between;
  align-items: center;
  gap: 16px;
}
header h1 { margin: 0; font-size: 23px; }
header p { margin: 6px 0 0; color: #c5c9dc; font-size: 13px; }
main { max-width: 1150px; margin: 30px auto; padding: 0 20px; }
h2 { font-size: 19px; margin: 0 0 16px; }
.section { margin-bottom: 30px; }
.grid {
  display: grid;
  grid-template-columns: repeat(4, minmax(0, 1fr));
  gap: 15px;
}
.card {
  background: var(--card);
  border: 1px solid var(--border);
  border-radius: 13px;
  padding: 20px;
  min-width: 0;
}
.metric-label { color: var(--muted); font-size: 13px; }
.metric { font-size: 28px; font-weight: 750; margin: 12px 0 5px; }
.note { font-size: 12px; color: var(--muted); }
.layout {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 18px;
}
label { display: block; font-size: 13px; margin: 12px 0 6px; }
input, select, button {
  font: inherit;
  border-radius: 7px;
  padding: 10px;
}
input, select {
  width: 100%;
  border: 1px solid #dce1eb;
  background: white;
}
button {
  background: var(--primary);
  color: white;
  border: 0;
  cursor: pointer;
  font-weight: 600;
}
button:hover { opacity: .88; }
form button { margin-top: 15px; width: 100%; }
.table-wrap { overflow-x: auto; }
table { width: 100%; border-collapse: collapse; font-size: 13px; }
th, td {
  text-align: left;
  padding: 12px 8px;
  border-bottom: 1px solid var(--border);
}
th { color: var(--muted); font-weight: 600; }
.pill {
  display: inline-block;
  padding: 5px 8px;
  border-radius: 20px;
  background: #eeedff;
  color: #5146e5;
  font-size: 11px;
}
.delete {
  background: #fff0f0;
  color: #b42318;
  padding: 6px 8px;
}
.roadmap-item {
  padding: 12px;
  margin-top: 10px;
  border: 1px solid var(--border);
  border-radius: 9px;
}
.roadmap-item strong { display: block; margin-bottom: 7px; }
.feedback { color: var(--muted); font-size: 13px; line-height: 1.5; }
footer {
  text-align: center;
  padding: 25px;
  color: var(--muted);
  font-size: 12px;
}
@media(max-width:750px) {
  .grid { grid-template-columns: repeat(2, minmax(0,1fr)); }
  .layout { grid-template-columns: 1fr; }
  header { align-items: flex-start; flex-direction: column; }
}
@media(max-width:400px) {
  .grid { grid-template-columns: 1fr; }
}
</style>
</head>
<body>
<header>
  <div>
    <h1>ProductPilot</h1>
    <p>Product decisions backed by data and customer needs</p>
  </div>
  <span class="pill">PRODUCT WORKSPACE</span>
</header>

<main>
  <section class="section">
    <h2>Product Overview</h2>
    <div class="grid">
      <div class="card">
        <div class="metric-label">Feature Requests</div>
        <div class="metric" id="total">0</div>
        <div class="note">Ideas in the backlog</div>
      </div>
      <div class="card">
        <div class="metric-label">High Priority</div>
        <div class="metric" id="high">0</div>
        <div class="note">RICE score of 50 or more</div>
      </div>
      <div class="card">
        <div class="metric-label">Planned Features</div>
        <div class="metric" id="planned">0</div>
        <div class="note">Features on the roadmap</div>
      </div>
      <div class="card">
        <div class="metric-label">Delivered</div>
        <div class="metric" id="shipped">0</div>
        <div class="note">Marked as shipped</div>
      </div>
    </div>
  </section>

  <section class="section layout">
    <div class="card">
      <h2>Prioritize a Feature</h2>
      <p class="feedback">RICE = Reach × Impact × Confidence ÷ Effort.
      Enter estimates to compare opportunities.</p>
      <form id="featureForm">
        <label for="name">Feature name</label>
        <input id="name" required maxlength="100"
          placeholder="e.g. Simplify onboarding">
        <label for="reach">Users reached per quarter</label>
        <input id="reach" type="number" min="0" required value="500">
        <label for="impact">Impact (0.25, 0.5, 1, 2 or 3)</label>
        <select id="impact">
          <option value="0.25">0.25 — Minimal</option>
          <option value="0.5">0.5 — Low</option>
          <option value="1" selected>1 — Medium</option>
          <option value="2">2 — High</option>
          <option value="3">3 — Massive</option>
        </select>
        <label for="confidence">Confidence (%)</label>
        <input id="confidence" type="number" min="0"
          max="100" required value="80">
        <label for="effort">Effort (person-months)</label>
        <input id="effort" type="number" min="0.1"
          step="0.1" required value="2">
        <label for="status">Roadmap status</label>
        <select id="status">
          <option>Backlog</option>
          <option>Planned</option>
          <option>In Progress</option>
          <option>Shipped</option>
        </select>
        <button type="submit">Add Feature</button>
      </form>
    </div>

    <div class="card">
      <h2>Product Roadmap</h2>
      <p class="feedback">Use this sample roadmap to demonstrate
      how product priorities move toward delivery.</p>
      <div id="roadmap"></div>
    </div>
  </section>

  <section class="section card">
    <h2>Feature Backlog & Prioritization</h2>
    <div class="table-wrap">
      <table>
        <thead>
          <tr>
            <th>Feature</th>
            <th>RICE</th>
            <th>Priority</th>
            <th>Status</th>
            <th>Action</th>
          </tr>
        </thead>
        <tbody id="features"></tbody>
      </table>
    </div>
    <p class="feedback" id="empty" hidden>
      No features yet. Add one using the form above.
    </p>
  </section>

  <section class="section card">
    <h2>Product Success Metrics</h2>
    <p class="feedback">
      Example targets only — replace these with validated product data.
    </p>
    <div class="grid">
      <div>
        <div class="metric-label">Activation target</div>
        <div class="metric">40%</div>
      </div>
      <div>
        <div class="metric-label">Retention target</div>
        <div class="metric">30%</div>
      </div>
      <div>
        <div class="metric-label">Time to value</div>
        <div class="metric">5 days</div>
      </div>
      <div>
        <div class="metric-label">NPS target</div>
        <div class="metric">40</div>
      </div>
    </div>
  </section>
</main>

<footer>
  ProductPilot · Independent product management portfolio project
</footer>

<script>
const starterFeatures = [
  { name: "Simplify onboarding", reach: 500, impact: 2,
    confidence: 80, effort: 2, status: "Planned" },
  { name: "Improve search", reach: 300, impact: 1,
    confidence: 70, effort: 2, status: "In Progress" },
  { name: "Export reports", reach: 150, impact: 1,
    confidence: 90, effort: 3, status: "Backlog" }
];

let features = starterFeatures.map((feature, index) => ({
  ...feature, id: index + 1
}));
let nextId = features.length + 1;

function rice(feature) {
  if (feature.effort <= 0) return 0;
  return feature.reach * feature.impact *
    (feature.confidence / 100) / feature.effort;
}

function priority(score) {
  if (score >= 50) return "High";
  if (score >= 20) return "Medium";
  return "Low";
}

function render() {
  document.getElementById("total").textContent = features.length;
  document.getElementById("high").textContent =
    features.filter(f => rice(f) >= 50).length;
  document.getElementById("planned").textContent =
    features.filter(f => f.status === "Planned" ||
      f.status === "In Progress").length;
  document.getElementById("shipped").textContent =
    features.filter(f => f.status === "Shipped").length;

  const tbody = document.getElementById("features");
  tbody.replaceChildren();

  const sorted = [...features].sort((a, b) => rice(b) - rice(a));
  document.getElementById("empty").hidden = sorted.length !== 0;

  sorted.forEach(feature => {
    const tr = document.createElement("tr");
    const values = [
      feature.name,
      rice(feature).toFixed(1),
      priority(rice(feature)),
      feature.status
    ];

    values.forEach(value => {
      const td = document.createElement("td");
      td.textContent = value;
      tr.appendChild(td);
    });

    const action = document.createElement("td");
    const btn = document.createElement("button");
    btn.className = "delete";
    btn.textContent = "Remove";
    btn.addEventListener("click", () => {
      features = features.filter(f => f.id !== feature.id);
      render();
    });
    action.appendChild(btn);
    tr.appendChild(action);
    tbody.appendChild(tr);
  });

  const roadmap = document.getElementById("roadmap");
  roadmap.replaceChildren();

  ["Planned", "In Progress", "Shipped"].forEach(status => {
    const items = features.filter(f => f.status === status);
    const group = document.createElement("div");
    group.className = "roadmap-item";

    const title = document.createElement("strong");
    title.textContent = status + " (" + items.length + ")";
    group.appendChild(title);

    const detail = document.createElement("div");
    detail.className = "feedback";
    detail.textContent = items.length
      ? items.map(f => f.name).join(", ")
      : "No features yet";
    group.appendChild(detail);
    roadmap.appendChild(group);
  });
}

document.getElementById("featureForm").addEventListener("submit", event => {
  event.preventDefault();

  const feature = {
    id: nextId++,
    name: document.getElementById("name").value.trim(),
    reach: Number(document.getElementById("reach").value),
    impact: Number(document.getElementById("impact").value),
    confidence: Number(document.getElementById("confidence").value),
    effort: Number(document.getElementById("effort").value),
    status: document.getElementById("status").value
  };

  if (!feature.name || feature.reach < 0 ||
      feature.confidence < 0 || feature.confidence > 100 ||
      feature.effort <= 0) return;

  features.push(feature);
  event.target.reset();
  render();
});

render();
</script>
</body>
</html>
