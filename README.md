
<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>Fernando Crypto Faucet</title>
  <style>
    body {
      background: #0b1020;
      color: white;
      font-family: Arial, sans-serif;
      text-align: center;
      padding: 25px 12px;
    }
    main {
      max-width: 500px;
      margin: auto;
    }
    section {
      background: #182440;
      padding: 20px;
      margin: 18px 0;
      border-radius: 16px;
    }
    h1 { color: #ffc857; }
    button, select {
      width: 100%;
      padding: 14px;
      border: 0;
      border-radius: 10px;
      margin: 8px 0;
      font-size: 16px;
    }
    button {
      background: #ffc857;
      font-weight: bold;
    }
    .saldo { color: #43d9a3; }
  </style>
</head>
<body>
<main>
  <h1>₿ Fernando Crypto Faucet</h1>
  <p>Tu faucet de demostración de criptomonedas</p>

  <section>
    <h2>🎁 Reclamar recompensa</h2>
    <select id="moneda">
      <option value="BTC">Bitcoin (BTC)</option>
      <option value="LTC">Litecoin (LTC)</option>
      <option value="DOGE">Dogecoin (DOGE)</option>
    </select>
    <p id="recompensa">0.00000010 BTC</p>
    <button id="reclamar">Reclamar ahora</button>
    <p id="mensaje" aria-live="polite"></p>
  </section>

  <section>
    <h2>💰 Saldos de prueba</h2>
    <p>BTC: <span id="BTC" class="saldo">0.00000000</span></p>
    <p>LTC: <span id="LTC" class="saldo">0.00000000</span></p>
    <p>DOGE: <span id="DOGE" class="saldo">0.00000000</span></p>
  </section>

  <p>Demostración educativa. No se envían criptomonedas reales.</p>
</main>

<script>
const recompensas = {
  BTC: 0.00000010,
  LTC: 0.00000100,
  DOGE: 0.00100000
};

const saldos = { BTC: 0, LTC: 0, DOGE: 0 };
let ultimoReclamo = 0;

const moneda = document.getElementById("moneda");

function actualizar() {
  const m = moneda.value;
  document.getElementById("recompensa").textContent =
    recompensas[m].toFixed(8) + " " + m;

  for (const c of ["BTC", "LTC", "DOGE"]) {
    document.getElementById(c).textContent =
      saldos[c].toFixed(8);
  }
}

moneda.addEventListener("change", actualizar);

document.getElementById("reclamar").addEventListener("click", () => {
  const ahora = Date.now();
  const espera = 60000 - (ahora - ultimoReclamo);

  if (espera > 0) {
    document.getElementById("mensaje").textContent =
      "Espera " + Math.ceil(espera / 1000) + " segundos.";
    return;
  }

  const m = moneda.value;
  saldos[m] += recompensas[m];
  ultimoReclamo = ahora;
  actualizar();

  document.getElementById("mensaje").textContent =
    "¡Recompensa de prueba registrada! No es un pago real.";
});

actualizar();
</script>
</body>
</html>
