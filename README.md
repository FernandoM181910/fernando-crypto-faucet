
const recompensas = {
  BTC: 0.00000010,
  LTC: 0.00000100,
  DOGE: 0.00100000
};

const saldos = {
  BTC: 0,
  LTC: 0,
  DOGE: 0
};

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
    "¡Recompensa de prueba registrada! No se enviaron monedas reales.";
});
actualizar();
