<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Proceeds and Bank Discount Calculator</title>
  <style>
    body { font-family: Arial, sans-serif; margin: 20px; background: #f9f9f9; }
    h1 { color: #333; }
    .calculator { background: #fff; padding: 20px; border-radius: 10px; box-shadow: 0 2px 10px rgba(0,0,0,0.1); max-width: 500px; margin: auto; }
    label { display: block; margin-top: 15px; }
    input, select, button { width: 100%; padding: 10px; margin-top: 5px; border-radius: 5px; border: 1px solid #ccc; }
    button { background-color: #4CAF50; color: white; font-weight: bold; }
    .result { margin-top: 20px; font-size: 18px; color: #2e7d32; }
  </style>
</head>
<body>
  <div class="calculator">
    <h1>Proceeds and Bank Discount Calculator</h1>
    <label for="calculate">Calculate:</label>
    <select id="calculate">
      <option value="proceeds">Proceeds (P)</option>
      <option value="S">Maturity Value (S)</option>
      <option value="d">Discount Rate (d)</option>
      <option value="t">Discount Term (t)</option>
      <option value="D">Bank Discount (D)</option>
    </select>

    <label for="S">Maturity Value (S):</label>
    <input type="number" id="S" placeholder="Enter S">

    <label for="d">Discount Rate (d):</label>
    <input type="number" step="any" id="d" placeholder="Enter d (e.g. 0.08)">

    <label for="t">Discount Term (t):</label>
    <input type="number" step="any" id="t" placeholder="Enter t">

    <label for="P">Proceeds (P):</label>
    <input type="number" id="P" placeholder="Enter P (if known)">

    <button id="solveBtn">Calculate</button>
    <div class="result" id="result"></div>
  </div>

  <script>
    const calcType = document.getElementById("calculate");
    const solveBtn = document.getElementById("solveBtn");

    solveBtn.addEventListener("click", calculate);

    function calculate() {
      const S = parseFloat(document.getElementById("S").value);
      const d = parseFloat(document.getElementById("d").value);
      const t = parseFloat(document.getElementById("t").value);
      const Pval = parseFloat(document.getElementById("P").value);
      const type = calcType.value;

      let result = "";

      if (type === "proceeds") {
        if (!isNaN(S) && !isNaN(d) && !isNaN(t)) {
          result = "Proceeds (P) = " + (S * (1 - d * t)).toFixed(2);
        } else {
          result = "Please fill in all values for S, d, and t.";
        }
      } else if (type === "S") {
        if (!isNaN(Pval) && !isNaN(d) && !isNaN(t)) {
          result = "Maturity Value (S) = " + (Pval / (1 - d * t)).toFixed(2);
        } else {
          result = "Please fill in all values for P, d, and t.";
        }
      } else if (type === "d") {
        if (!isNaN(Pval) && !isNaN(S) && !isNaN(t)) {
          result = "Discount Rate (d) = " + ((1 - Pval / S) / t).toFixed(4);
        } else {
          result = "Please fill in all values for P, S, and t.";
        }
      } else if (type === "t") {
        if (!isNaN(Pval) && !isNaN(S) && !isNaN(d)) {
          result = "Discount Term (t) = " + ((1 - Pval / S) / d).toFixed(4);
        } else {
          result = "Please fill in all values for P, S, and d.";
        }
      } else if (type === "D") {
        if (!isNaN(S) && !isNaN(d) && !isNaN(t)) {
          const D1 = S * d * t;
          result = "Bank Discount (D = Sdt) = " + D1.toFixed(2);
          if (!isNaN(Pval)) {
            const D2 = S - Pval;
            result += "\nBank Discount (D = S - P) = " + D2.toFixed(2);
          }
        } else if (!isNaN(S) && !isNaN(Pval)) {
          result = "Bank Discount (D = S - P) = " + (S - Pval).toFixed(2);
        } else {
          result = "Please fill in the required values to calculate D.";
        }
      }

      document.getElementById("result").innerText = result;
    }
  </script>
</body>
</html>
