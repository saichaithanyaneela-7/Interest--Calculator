
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Interest Calculator</title>

  <style>
/* ===== GLOBAL STYLES ===== */
* {
  box-sizing: border-box;
}

html {
  scroll-behavior: smooth;
}

body {
  margin: 0;
  font-family: "Segoe UI", Arial, sans-serif;
  background: linear-gradient(135deg, #eff6ff, #f5f3ff, #eef2ff);
  background-attachment: fixed;
  color: #1e293b;
  line-height: 1.6;
}

/* ===== HEADER ===== */
header {
  background: linear-gradient(120deg, #1d4ed8, #6d28d9, #2563eb);
  background-size: 200% 200%;
  animation: gradientMove 8s ease infinite;
  color: white;
  text-align: center;
  padding: 40px 15px;
  box-shadow: 0 8px 25px #2563eb35;
}

header h1 {
  margin: 0 0 10px;
  font-size: clamp(28px, 5vw, 42px);
  letter-spacing: 1px;
  animation: fadeDown 0.8s ease;
}

header p {
  margin-bottom: 0;
  opacity: 0.9;
}

/* ===== NAVIGATION ===== */
nav {
  background: #172554;
  padding: 12px;
  text-align: center;
  box-shadow: 0 4px 12px #00000015;
}

nav button {
  width: auto;
  margin: 4px;
  padding: 11px 20px;
  background: transparent;
  color: white;
  border: 1px solid #64748b;
  border-radius: 25px;
  transition: all 0.3s ease;
}

nav button:hover {
  background: white;
  color: #1d4ed8;
  border-color: white;
  transform: translateY(-3px);
  box-shadow: 0 5px 15px #ffffff25;
}

/* ===== MAIN CONTAINER ===== */
.container {
  width: min(1000px, 94%);
  margin: 35px auto;
  padding: 10px;
}

/* ===== CALCULATOR AND HISTORY BOXES ===== */
.calculator,
.history-box {
  background: #ffffffed;
  padding: 30px;
  border: 1px solid #dbeafe;
  border-radius: 20px;
  box-shadow: 0 10px 30px #1e40af12;
  margin-bottom: 30px;
  transition: box-shadow 0.3s ease;
  animation: fadeUp 0.7s ease;
}

.calculator:hover,
.history-box:hover {
  box-shadow: 0 15px 35px #1e40af20;
}

h2 {
  color: #1d4ed8;
  font-size: 26px;
  margin-top: 0;
}

h2::after {
  content: "";
  display: block;
  width: 65px;
  height: 4px;
  margin-top: 8px;
  border-radius: 5px;
  background: linear-gradient(90deg, #2563eb, #9333ea);
}

/* ===== LABELS AND INPUTS ===== */
label {
  display: block;
  margin-top: 18px;
  font-weight: 600;
  color: #334155;
}

input,
select {
  width: 100%;
  padding: 13px;
  margin-top: 7px;
  border: 1px solid #cbd5e1;
  border-radius: 10px;
  background: #f8fafc;
  color: #1e293b;
  font: inherit;
  outline: none;
  transition: all 0.3s ease;
}

input:hover,
select:hover {
  border-color: #818cf8;
  background: white;
}

input:focus,
select:focus {
  border-color: #6366f1;
  background: white;
  box-shadow: 0 0 0 4px #6366f125;
  transform: translateY(-1px);
}

/* ===== BUTTONS ===== */
button {
  padding: 12px 19px;
  margin-top: 15px;
  border: none;
  border-radius: 9px;
  background: linear-gradient(135deg, #2563eb, #6d28d9);
  color: white;
  cursor: pointer;
  font-size: 14px;
  font-weight: 600;
  box-shadow: 0 4px 10px #2563eb25;
  transition: transform 0.25s ease,
              box-shadow 0.25s ease,
              filter 0.25s ease;
}

button:hover {
  transform: translateY(-3px);
  box-shadow: 0 8px 18px #2563eb35;
  filter: brightness(1.08);
}

button:active {
  transform: scale(0.97);
}

button:focus-visible {
  outline: 3px solid #a5b4fc;
  outline-offset: 3px;
}

/* ===== DELETE BUTTON ===== */
button.danger {
  background: linear-gradient(135deg, #ef4444, #b91c1c);
  box-shadow: 0 4px 10px #dc262625;
}

button.danger:hover {
  box-shadow: 0 8px 18px #dc262640;
}

/* ===== CALCULATION RESULT ===== */
#result {
  display: none;
  margin-top: 25px;
  padding: 22px;
  background: linear-gradient(135deg, #dcfce7, #ecfdf5);
  color: #14532d;
  border: 1px solid #86efac;
  border-left: 5px solid #16a34a;
  border-radius: 12px;
  line-height: 2;
  overflow-wrap: anywhere;
  box-shadow: 0 6px 20px #16a34a12;
  animation: resultReveal 0.5s ease;
}

#result b {
  color: #166534;
}

/* ===== INTEREST TYPE CARDS ===== */
.types {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(210px, 1fr));
  gap: 20px;
}

.card {
  position: relative;
  overflow: hidden;
  background: white;
  padding: 22px;
  border: 1px solid #e2e8f0;
  border-left: 5px solid #6366f1;
  border-radius: 14px;
  box-shadow: 0 5px 15px #00000008;
  transition: transform 0.3s ease,
              box-shadow 0.3s ease,
              border-color 0.3s ease;
}

.card::before {
  content: "";
  position: absolute;
  top: 0;
  left: -100%;
  width: 100%;
  height: 4px;
  background: linear-gradient(90deg, #2563eb, #a855f7);
  transition: left 0.4s ease;
}

.card:hover {
  transform: translateY(-7px);
  border-left-color: #9333ea;
  box-shadow: 0 14px 28px #4f46e525;
}

.card:hover::before {
  left: 0;
}

.card h3 {
  margin-top: 0;
  color: #4f46e5;
  transition: color 0.3s ease;
}

.card:hover h3 {
  color: #9333ea;
}

.card p {
  font-size: 14px;
  line-height: 1.8;
  color: #475569;
}

/* ===== HISTORY TABLE ===== */
.table-wrap {
  overflow-x: auto;
  border-radius: 10px;
}

table {
  width: 100%;
  border-collapse: collapse;
  margin-top: 18px;
  font-size: 14px;
}

th,
td {
  padding: 13px;
  border: 1px solid #e2e8f0;
  text-align: left;
  white-space: nowrap;
}

th {
  background: linear-gradient(135deg, #dbeafe, #ede9fe);
  color: #312e81;
}

tr:nth-child(even) {
  background: #f8fafc;
}

tbody tr {
  transition: background 0.2s ease;
}

tbody tr:hover {
  background: #e0e7ff;
}

/* ===== NOTES AND VISIBILITY ===== */
.note {
  color: #64748b;
  font-size: 13px;
  line-height: 1.7;
}

.hidden {
  display: none !important;
}

/* ===== FOOTER ===== */
footer {
  text-align: center;
  background: linear-gradient(120deg, #0f172a, #312e81);
  color: white;
  padding: 22px;
  margin-top: 40px;
}

footer p {
  margin: 0;
}

/* ===== ANIMATIONS ===== */
@keyframes gradientMove {
  0%, 100% {
    background-position: 0% 50%;
  }

  50% {
    background-position: 100% 50%;
  }
}

@keyframes fadeDown {
  from {
    opacity: 0;
    transform: translateY(-15px);
  }

  to {
    opacity: 1;
    transform: translateY(0);
  }
}

@keyframes fadeUp {
  from {
    opacity: 0;
    transform: translateY(15px);
  }

  to {
    opacity: 1;
    transform: translateY(0);
  }
}

@keyframes resultReveal {
  from {
    opacity: 0;
    transform: translateY(10px);
  }

  to {
    opacity: 1;
    transform: translateY(0);
  }
}

/* ===== RESPONSIVE DESIGN ===== */
@media (max-width: 600px) {
  header {
    padding: 30px 12px;
  }

  header h1 {
    font-size: 27px;
  }

  nav {
    padding: 10px 5px;
  }

  nav button {
    padding: 9px 12px;
    font-size: 12px;
  }

  .container {
    width: 96%;
    margin: 20px auto;
    padding: 5px;
  }

  .calculator,
  .history-box {
    padding: 18px;
    border-radius: 14px;
  }

  h2 {
    font-size: 22px;
  }

  .types {
    grid-template-columns: 1fr;
    gap: 15px;
  }

  input,
  select {
    padding: 12px;
    font-size: 16px;
  }

  #result {
    padding: 15px;
  }

  footer {
    padding: 18px 10px;
  }
}

/* ===== ACCESSIBILITY ===== */
@media (prefers-reduced-motion: reduce) {
  *,
  *::before,
  *::after {
    animation-duration: 0.01ms !important;
    animation-iteration-count: 1 !important;
    scroll-behavior: auto !important;
    transition-duration: 0.01ms !important;
  }
}
```
 

  </style>
</head>

<body>

  <header>
    <h1>💰 Interest Calculator</h1>
    <p>Calculate interest, manage calculations, and explore money concepts.</p>
  </header>

  <nav>
    <button onclick="showSection('calculatorSection')">
      Calculator
    </button>

    <button onclick="openHistory()">
      📋 History
    </button>

    <button onclick="showSection('typesSection')">
      Interest Types
    </button>
  </nav>

  <main class="container">

    <!-- CALCULATOR -->

    <section id="calculatorSection" class="calculator">
      <h2>Calculate Your Interest</h2>

      <label for="type">Select Interest Type</label>
      <select id="type">
        <option value="simple">Simple Interest</option>
        <option value="compound">Compound Interest</option>
        <option value="savings">Savings Account Estimate</option>
        <option value="fd">Fixed Deposit (FD)</option>
        <option value="loan">Loan EMI Calculator</option>
        <option value="credit">Credit Card Interest</option>
      </select>

      <label for="principal">Principal / Amount (₹)</label>
      <input type="number" id="principal" min="0.01"
             step="any" placeholder="Enter amount">

      <label for="rate">Annual Interest Rate (%)</label>
      <input type="number" id="rate" min="0"
             step="any" placeholder="Enter interest rate">

      <label for="time">Time (Years)</label>
      <input type="number" id="time" min="0.01"
             step="any" placeholder="Enter time in years">

      <div id="frequencyBox">
        <label for="frequency">Compounding Frequency</label>
        <select id="frequency">
          <option value="1">Yearly</option>
          <option value="2">Half-yearly</option>
          <option value="4">Quarterly</option>
          <option value="12">Monthly</option>
        </select>
      </div>

      <button onclick="calculate()">Calculate Now</button>

      <div id="result" aria-live="polite"></div>
      <p class="note">
        Successful calculations are saved automatically in your history.
      </p>
    </section>

    <!-- CALCULATION HISTORY -->

    <section id="historySection" class="history-box hidden">
      <h2>📋 Calculation History</h2>

      <p class="note">
        Your calculations are stored in this browser.
        Each record is automatically deleted after 30 days.
      </p>

      <button onclick="openHistory()">🔄 Refresh History</button>
      <button class="danger" onclick="clearHistory()">
        Delete All History
      </button>

      <p id="historyStatus" aria-live="polite">
        Loading history...
      </p>

      <div class="table-wrap">
        <table>
          <thead>
            <tr>
              <th>Date & Time</th>
              <th>Interest Type</th>
              <th>Principal</th>
              <th>Rate</th>
              <th>Duration</th>
              <th>Interest</th>
              <th>Total / Repayment</th>
              <th>Action</th>
            </tr>
          </thead>

          <tbody id="historyTable"></tbody>
        </table>
      </div>
    </section>

    <!-- INTEREST TYPES -->

    <section id="typesSection">
      <h2>Types of Interest</h2>

      <div class="types">

        <article class="card">
          <h3>Simple Interest</h3>
          <p>Interest is calculated only on the original principal.</p>
          <p><b>Formula:</b> SI = (P × R × T) / 100</p>
        </article>

        <article class="card">
          <h3>Compound Interest</h3>
          <p>Interest is earned on the principal and accumulated interest.</p>
          <p><b>Formula:</b> A = P(1 + R/100)<sup>T</sup></p>
        </article>

        <article class="card">
          <h3>Savings Interest</h3>
          <p>Interest earned on eligible bank savings balances.</p>
        </article>

        <article class="card">
          <h3>Fixed Deposit</h3>
          <p>Interest earned by depositing money for a fixed period.</p>
        </article>

        <article class="card">
          <h3>Loan Interest</h3>
          <p>The cost of borrowing money, often repaid through EMIs.</p>
        </article>

        <article class="card">
          <h3>Credit Card Interest</h3>
          <p>Interest that may apply to unpaid credit card balances.</p>
        </article>

        <article class="card">
          <h3>Fixed Rate</h3>
          <p>A rate that remains unchanged for the agreed period.</p>
        </article>

        <article class="card">
          <h3>Floating Rate</h3>
          <p>A rate that can change with a benchmark or market conditions.</p>
        </article>

        <article class="card">
          <h3>Nominal Interest</h3>
          <p>The stated interest rate before adjusting for inflation.</p>
        </article>

        <article class="card">
          <h3>Real Interest</h3>
          <p>The rate adjusted for inflation. Approximately, nominal rate minus inflation rate.</p>
        </article>

        <article class="card">
          <h3>Overdue Interest</h3>
          <p>Interest that may apply when a payment is late, subject to the agreement.</p>
        </article>

        <article class="card">
          <h3>Precomputed Interest</h3>
          <p>Interest calculated in advance using a specified loan method.</p>
        </article>

        <article class="card">
          <h3>Negative Interest</h3>
          <p>A rate below zero, which can result in a charge on certain balances.</p>
        </article>

      </div>
    </section>

  </main>

  <footer>
    <p>Interest Calculator | Learn and Manage Money Wisely</p>
  </footer>

  <script>
    // DATABASE CONFIGURATION

    const DB_NAME = "InterestCalculatorDB";
    const STORE_NAME = "calculations";
    const DB_VERSION = 1;
    const DAYS_30 = 30 * 24 * 60 * 60 * 1000;

    let db;

    // Open the IndexedDB database.

    function openDatabase() {
      return new Promise((resolve, reject) => {
        const request = indexedDB.open(DB_NAME, DB_VERSION);

        request.onupgradeneeded = function(event) {
          const database = event.target.result;

          if (!database.objectStoreNames.contains(STORE_NAME)) {
            const store = database.createObjectStore(
              STORE_NAME,
              { keyPath: "id", autoIncrement: true }
            );

            store.createIndex("createdAt", "createdAt");
          }
        };

        request.onsuccess = function(event) {
          db = event.target.result;
          resolve(db);
        };

        request.onerror = function() {
          reject(request.error);
        };
      });
    }

    // Save one calculation to the database.

    function saveCalculation(record) {
      return new Promise((resolve, reject) => {
        const transaction = db.transaction(STORE_NAME, "readwrite");
        const store = transaction.objectStore(STORE_NAME);

        store.add(record);

        transaction.oncomplete = () => resolve();
        transaction.onerror = () => reject(transaction.error);
        transaction.onabort = () => reject(transaction.error);
      });
    }

    // Get all saved calculations.

    function getAllCalculations() {
      return new Promise((resolve, reject) => {
        const transaction = db.transaction(STORE_NAME, "readonly");
        const request = transaction.objectStore(STORE_NAME).getAll();

        request.onsuccess = () => resolve(request.result);
        request.onerror = () => reject(request.error);
      });
    }

    // Delete an individual record.

    function deleteCalculation(id) {
      return new Promise((resolve, reject) => {
        const transaction = db.transaction(STORE_NAME, "readwrite");

        transaction.objectStore(STORE_NAME).delete(id);

        transaction.oncomplete = () => resolve();
        transaction.onerror = () => reject(transaction.error);
      });
    }

    // Delete all records.

    function deleteAllCalculations() {
      return new Promise((resolve, reject) => {
        const transaction = db.transaction(STORE_NAME, "readwrite");

        transaction.objectStore(STORE_NAME).clear();

        transaction.oncomplete = () => resolve();
        transaction.onerror = () => reject(transaction.error);
      });
    }

    // Automatically remove records older than 30 days.

    async function cleanOldHistory() {
      const records = await getAllCalculations();
      const cutoff = Date.now() - DAYS_30;

      const expiredRecords = records.filter(
        record => record.createdAt < cutoff
      );

      if (expiredRecords.length === 0) {
        return;
      }

      await new Promise((resolve, reject) => {
        const transaction = db.transaction(STORE_NAME, "readwrite");
        const store = transaction.objectStore(STORE_NAME);

        expiredRecords.forEach(record => store.delete(record.id));

        transaction.oncomplete = () => resolve();
        transaction.onerror = () => reject(transaction.error);
      });
    }

    // Format Indian currency.

    function money(value) {
      return value.toLocaleString("en-IN", {
        style: "currency",
        currency: "INR",
        maximumFractionDigits: 2
      });
    }

    // Format a saved date.

    function formatDate(timestamp) {
      return new Date(timestamp).toLocaleString("en-IN");
    }

    const typeNames = {
      simple: "Simple Interest",
      compound: "Compound Interest",
      savings: "Savings Account",
      fd: "Fixed Deposit",
      loan: "Loan EMI",
      credit: "Credit Card"
    };

    // CALCULATE INTEREST

    async function calculate() {
      const type = document.getElementById("type").value;

      const pInput = document.getElementById("principal").value;
      const rInput = document.getElementById("rate").value;
      const tInput = document.getElementById("time").value;

      const P = Number(pInput);
      const R = Number(rInput);
      const T = Number(tInput);
      const n = Number(document.getElementById("frequency").value);

      const result = document.getElementById("result");

      result.style.display = "block";

      if (
        pInput.trim() === "" ||
        rInput.trim() === "" ||
        tInput.trim() === "" ||
        !Number.isFinite(P) ||
        !Number.isFinite(R) ||
        !Number.isFinite(T) ||
        P <= 0 || R < 0 || T <= 0
      ) {
        result.textContent =
          "Enter a positive amount and duration, and a non-negative rate.";
        return;
      }

      let interest;
      let amount;
      let emi = null;
      let duration = T;
      let extra = "";

      if (type === "simple") {
        interest = P * R * T / 100;
        amount = P + interest;
      }

      else if (
        type === "compound" ||
        type === "savings" ||
        type === "fd"
      ) {
        amount = P * Math.pow(1 + R / (100 * n), n * T);
        interest = amount - P;

        extra = "Compounding: " + n + " time(s) per year";
      }

      else if (type === "loan") {
        const months = Math.round(T * 12);
        const monthlyRate = R / 1200;

        emi = monthlyRate === 0
          ? P / months
          : P * monthlyRate * Math.pow(1 + monthlyRate, months) /
            (Math.pow(1 + monthlyRate, months) - 1);

        amount = emi * months;
        interest = amount - P;

        duration = months / 12;
        extra = "Monthly EMI: " + money(emi);
      }

      else if (type === "credit") {
        const months = Math.round(T * 12);
        const monthlyRate = R / 1200;

        amount = P * Math.pow(1 + monthlyRate, months);
        interest = amount - P;

        duration = months / 12;
        extra = "Illustrative estimate assuming no payments, fees, or new purchases.";
      }

      if (
        !Number.isFinite(interest) ||
        !Number.isFinite(amount) ||
        (emi !== null && !Number.isFinite(emi))
      ) {
        result.textContent = "The result is too large to calculate.";
        return;
      }

      result.innerHTML =
        "<b>Interest Type:</b> " + typeNames[type] +
        "<br><b>Principal:</b> " + money(P) +
        "<br><b>Interest:</b> " + money(interest) +
        "<br><b>Total Amount / Repayment:</b> " + money(amount) +
        (emi !== null ? "<br><b>Monthly EMI:</b> " + money(emi) : "") +
        (extra ? "<br><small>" + extra + "</small>" : "");

      // Save the result in IndexedDB.

      try {
        await saveCalculation({
          type: type,
          typeName: typeNames[type],
          principal: P,
          rate: R,
          duration: duration,
          interest: interest,
          amount: amount,
          emi: emi,
          createdAt: Date.now()
        });

        result.innerHTML +=
          "<br><b>✓ Saved to calculation history.</b>";

        // Refresh the history if it is currently open.
        if (!document.getElementById("historySection").classList.contains("hidden")) {
          await openHistory();
        }

      } catch (error) {
        console.error(error);
        result.innerHTML +=
          "<br><b>Warning:</b> Calculation completed, but history could not be saved.";
      }
    }

    // SHOW A SECTION.

    function showSection(sectionId) {
      document.getElementById("calculatorSection").classList.add("hidden");
      document.getElementById("historySection").classList.add("hidden");
      document.getElementById("typesSection").classList.add("hidden");

      document.getElementById(sectionId).classList.remove("hidden");

      window.scrollTo({ top: 0, behavior: "smooth" });
    }

    // VIEW HISTORY AND CLEAN EXPIRED RECORDS.

    async function openHistory() {
      showSection("historySection");

      const status = document.getElementById("historyStatus");
      const table = document.getElementById("historyTable");

      status.textContent = "Loading history...";
      table.replaceChildren();

      try {
        await cleanOldHistory();

        const records = await getAllCalculations();

        records.sort((a, b) => b.createdAt - a.createdAt);

        status.textContent = records.length
          ? records.length + " saved calculation(s). Records expire after 30 days."
          : "No calculation history found.";

        records.forEach(record => {
          const row = document.createElement("tr");

          const values = [
            formatDate(record.createdAt),
            record.typeName,
            money(record.principal),
            record.rate + "%",
            record.duration + " year(s)",
            money(record.interest),
            money(record.amount)
          ];

          values.forEach(value => {
            const cell = document.createElement("td");
            cell.textContent = value;
            row.appendChild(cell);
          });

          const actionCell = document.createElement("td");
          const deleteButton = document.createElement("button");

          deleteButton.textContent = "Delete";
          deleteButton.className = "danger";
          deleteButton.style.marginTop = "0";

          deleteButton.onclick = async function() {
            try {
              await deleteCalculation(record.id);
              await openHistory();
            } catch (error) {
              status.textContent = "Could not delete this record.";
            }
          };

          actionCell.appendChild(deleteButton);
          row.appendChild(actionCell);
          table.appendChild(row);
        });

      } catch (error) {
        console.error(error);
        status.textContent =
          "Unable to access history. Please use a browser that supports IndexedDB.";
      }
    }

    // CLEAR ALL HISTORY.

    async function clearHistory() {
      if (!confirm("Are you sure you want to delete ALL calculation history?")) {
        return;
      }

      try {
        await deleteAllCalculations();
        await openHistory();
        document.getElementById("historyStatus").textContent =
          "All calculation history has been deleted.";
      } catch (error) {
        document.getElementById("historyStatus").textContent =
          "Could not delete history.";
      }
    }

    // INITIALIZE DATABASE AND CLEAN EXPIRED RECORDS.

    async function initializeApp() {
      try {
        await openDatabase();
        await cleanOldHistory();
      } catch (error) {
        console.error("Database initialization failed:", error);

        document.getElementById("result").style.display = "block";
        document.getElementById("result").textContent =
          "Database unavailable. Please open this page in a modern browser.";
      }
    }

    initializeApp();
  </script>

</body>
</html>
