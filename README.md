
<!DOCTYPE html>
<html lang="id">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>NEON CALCULATOR</title>

<style>
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

body {
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 20px;
  font-family: Arial, sans-serif;
  color: white;
  background:
    radial-gradient(ellipse at top, #35205e, transparent 55%),
    #090910;
}

.calculator {
  width: 100%;
  max-width: 390px;
  padding: 26px;
  border: 1px solid #8b5cf655;
  border-radius: 28px;
  background: linear-gradient(145deg, #191725, #101019);
  box-shadow: 0 0 45px #7c3aed22;
}

.header {
  text-align: center;
  margin-bottom: 28px;
}

.logo {
  font-size: 12px;
  color: #b69aff;
  letter-spacing: 5px;
  margin-bottom: 10px;
}

h1 {
  font-size: 25px;
  letter-spacing: 1px;
}

.subtitle {
  color: #88869b;
  font-size: 12px;
  margin-top: 8px;
}

label {
  display: block;
  color: #aaa5c0;
  font-size: 12px;
  margin: 16px 0 8px;
}

input, select {
  width: 100%;
  border: 1px solid #ffffff12;
  border-radius: 13px;
  padding: 16px;
  font-size: 17px;
  color: white;
  background: #242132;
  outline: none;
}

input:focus, select:focus {
  border-color: #a78bfa;
  box-shadow: 0 0 12px #8b5cf633;
}

select {
  cursor: pointer;
}

select option {
  background: #242132;
}

button {
  width: 100%;
  border: none;
  border-radius: 13px;
  padding: 16px;
  margin-top: 18px;
  color: white;
  font-size: 14px;
  font-weight: bold;
  letter-spacing: 1px;
  cursor: pointer;
  background: linear-gradient(100deg, #7c3aed, #a855f7);
  box-shadow: 0 5px 22px #8b5cf633;
  transition: .2s;
}

button:active {
  transform: scale(.97);
}

.reset {
  margin-top: 10px;
  color: #bbb4d0;
  background: #292638;
  box-shadow: none;
}

.result {
  margin-top: 24px;
  padding: 20px;
  min-height: 115px;
  border: 1px solid #a78bfa33;
  border-radius: 17px;
  text-align: center;
  background: #0c0b14;
}

.result-label {
  color: #aaa5c0;
  font-size: 12px;
  letter-spacing: 2px;
}

#answer {
  margin-top: 13px;
  font-size: clamp(24px, 7vw, 34px);
  font-weight: bold;
  color: #c4b5fd;
  overflow-wrap: anywhere;
  text-shadow: 0 0 20px #a78bfa66;
}

#detail {
  color: #88869b;
  font-size: 12px;
  margin-top: 12px;
  overflow-wrap: anywhere;
}

.footer {
  text-align: center;
  color: #666276;
  font-size: 10px;
  letter-spacing: 2px;
  margin-top: 22px;
}
</style>
</head>

<body>
<div class="calculator">

  <div class="header">
    <div class="logo">✦ NEON SYSTEM ✦</div>
    <h1>CALCULATOR</h1>
    <p class="subtitle">Smart calculation interface</p>
  </div>

  <label for="num1">ANGKA PERTAMA</label>
  <input id="num1" type="number" step="any"
         placeholder="Masukkan angka...">

  <label for="operator">PILIH OPERASI</label>
  <select id="operator">
    <option value="*">✕ Perkalian</option>
    <option value="-">− Pengurangan</option>
    <option value="/">÷ Pembagian</option>
  </select>

  <label for="num2">ANGKA KEDUA</label>
  <input id="num2" type="number" step="any"
         placeholder="Masukkan angka...">

  <button onclick="calculate()">HITUNG SEKARANG ↗</button>
  <button class="reset" onclick="resetCalc()">RESET ULANG</button>

  <div class="result">
    <div class="result-label">HASIL PERHITUNGAN</div>
    <div id="answer">0</div>
    <div id="detail">Hasil akan muncul di sini</div>
  </div>

  <div class="footer">NEON CALCULATOR • 2026</div>
</div>

<script>
function calculate() {
  const a = document.getElementById("num1").value;
  const b = document.getElementById("num2").value;
  const op = document.getElementById("operator").value;
  const answer = document.getElementById("answer");
  const detail = document.getElementById("detail");

  if (a.trim() === "" || b.trim() === "") {
    answer.textContent = "INPUT KOSONG";
    detail.textContent = "Masukkan kedua angka terlebih dahulu.";
    return;
  }

  const x = Number(a);
  const y = Number(b);
  let result;
  let symbol;

  if (op === "*") {
    result = x * y;
    symbol = "×";
  } else if (op === "-") {
    result = x - y;
    symbol = "−";
  } else {
    if (y === 0) {
      answer.textContent = "ERROR";
      detail.textContent = "Angka tidak bisa dibagi dengan nol.";
      return;
    }
    result = x / y;
    symbol = "÷";
  }

  if (!Number.isFinite(result)) {
    answer.textContent = "DI LUAR BATAS";
    detail.textContent = "Hasil terlalu besar untuk ditampilkan.";
    return;
  }

  const formatted = Number(result.toPrecision(12)).toLocaleString(
    "en-US",
    { maximumFractionDigits: 12, useGrouping: true }
  );

  answer.textContent = formatted;
  detail.textContent = `${x} ${symbol} ${y} = ${formatted}`;
}

function resetCalc() {
  document.getElementById("num1").value = "";
  document.getElementById("num2").value = "";
  document.getElementById("operator").value = "*";
  document.getElementById("answer").textContent = "0";
  document.getElementById("detail").textContent =
    "Hasil akan muncul di sini";
}
</script>
</body>
</html>
