<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>Violetta Cosméticos</title>
<script src="https://cdnjs.cloudflare.com/ajax/libs/html2pdf.js/0.10.1/html2pdf.bundle.min.js"></script>
<style>
:root{--v:#762d76;--pink:#f7e5f4;--bg:#f7f2f8;--green:#16834a;--red:#c92c49}
*{box-sizing:border-box}
body{margin:0;background:var(--bg);font-family:Arial,sans-serif;color:#332536}
header{background:linear-gradient(135deg,#512056,#a54b98);color:white;text-align:center;padding:24px 12px}
header h1{margin:0;font-size:27px}
main{max-width:950px;margin:18px auto;padding:0 12px}
.panel{background:white;border-radius:14px;padding:17px;margin-bottom:16px;box-shadow:0 3px 14px #32133a12}
h2{color:var(--v);font-size:21px;margin-top:0}
label{display:block;font-size:13px;font-weight:bold;margin:0 0 6px}
input,select,textarea{width:100%;padding:11px;border:1px solid #ddcddd;border-radius:8px;font:inherit;background:white}
input[type=file]{font-size:12px;padding:7px}
.grid{display:grid;grid-template-columns:repeat(2,minmax(0,1fr));gap:12px}
.field{min-width:0}
.full{grid-column:1/-1}
button{border:0;border-radius:9px;padding:12px 15px;font-size:14px;font-weight:bold;cursor:pointer}
.primary{background:var(--v);color:white}
.secondary{background:#f0e0ef;color:var(--v)}
.success{background:var(--green);color:white}
.danger{background:var(--red);color:white}
.actions{display:flex;gap:8px;flex-wrap:wrap;margin-top:13px}
.product{border:1px solid #ead9e9;border-radius:12px;padding:12px;margin:12px 0;background:#fffbff}
.product-head{display:flex;justify-content:space-between;align-items:center;gap:8px;margin-bottom:10px}
.product-head strong{color:var(--v)}
.product-grid{display:grid;grid-template-columns:85px repeat(2,minmax(0,1fr));gap:10px;align-items:end}
.preview{width:85px;height:85px;object-fit:contain;border:1px solid #ead9e9;border-radius:8px;background:white}
.product-total{margin-top:12px;background:var(--pink);padding:10px;border-radius:8px;font-weight:bold;display:flex;justify-content:space-between;gap:8px}
.totalbox{background:#fcf2fb;padding:13px;border-radius:10px;margin-top:14px}
.line{display:flex;justify-content:space-between;gap:12px;margin:9px 0}
.grand{border-top:1px solid #dfc9df;padding-top:10px;color:var(--v);font-size:21px;font-weight:bold}
.small{font-size:12px;color:#766878;line-height:1.5}
.status{padding:5px 9px;border-radius:20px;font-weight:bold;font-size:12px;display:inline-block}
.paid{color:#08743b;background:#dff7e8}
.pending{color:#b3213d;background:#ffe4e9}
.history-item{border:1px solid #ead9e9;border-radius:10px;padding:12px;margin:10px 0}
.history-item h3{font-size:16px;color:var(--v);margin:0 0 8px}
.history-buttons{display:flex;gap:7px;flex-wrap:wrap;margin-top:9px}
.history-buttons button{font-size:12px;padding:9px}
@media(max-width:560px){
header h1{font-size:23px}
.grid{grid-template-columns:1fr}
.full{grid-column:auto}
.product-grid{grid-template-columns:72px 1fr}
.preview{width:72px;height:72px}
.product-grid .field{grid-column:2}
.actions button{flex:1 1 100%}
}
</style>
</head>
<body>
<header>
<h1>VIOLETTA COSMÉTICOS</h1>
<p>Comprobantes de venta y control de pagos</p>
</header>

<main>
<section class="panel">
<h2>1. Datos del comprobante</h2>
<div class="grid">
<div class="field">
<label>Número automático</label>
<input id="invoiceNo" readonly>
</div>
<div class="field">
<label>Fecha y hora de creación</label>
<input id="createdAt" readonly>
</div>
<div class="field">
<label for="invoiceDate">Fecha de emisión</label>
<input id="invoiceDate" type="date">
</div>
<div class="field">
<label for="clientName">Nombre de la clienta *</label>
<input id="clientName" placeholder="Nombre y apellido">
</div>
<div class="field">
<label for="clientPhone">Teléfono / WhatsApp</label>
<input id="clientPhone" type="tel" placeholder="Número de contacto">
</div>
<div class="field">
<label for="paymentStatus">Estado del pago</label>
<select id="paymentStatus">
<option value="pending">Pendiente de pago</option>
<option value="partial">Abonó una parte</option>
<option value="paid">Pagado completamente</option>
</select>
</div>
<div class="field">
<label for="dueDays">Días para pagar</label>
<input id="dueDays" type="number" min="0" value="7">
</div>
<div class="field">
<label for="dueDate">Fecha límite de pago</label>
<input id="dueDate" type="date">
</div>
<div class="field">
<label for="amountPaid">Importe abonado ($)</label>
<input id="amountPaid" type="number" min="0" step="0.01" value="0">
</div>
<div class="field">
<label for="paymentAlias">Alias de pago</label>
<input id="paymentAlias" placeholder="Ej. violetta.pagos">
</div>
<div class="field">
<label for="bankName">Banco o billetera</label>
<input id="bankName" placeholder="Ej. Mercado Pago">
</div>
<div class="field full">
<label for="notes">Observaciones</label>
<textarea id="notes" rows="2" placeholder="Detalles de entrega u otras aclaraciones"></textarea>
</div>
</div>
</section>

<section class="panel">
<h2>2. Productos</h2>
<p class="small">Agregá productos, fotos, precio, cantidad y descuento.</p>
<div id="products"></div>
<button id="addProductBtn" type="button" class="primary">＋ AGREGAR PRODUCTO</button>
<div class="totalbox">
<div class="line"><span>Subtotal</span><strong id="subtotal">$0,00</strong></div>
<div class="line"><span>Descuentos</span><strong id="discountTotal">$0,00</strong></div>
<div class="line grand"><span>TOTAL</span><span id="grandTotal">$0,00</span></div>
<div class="line"><span>Total abonado</span><strong id="paidTotal">$0,00</strong></div>
<div class="line"><span>Saldo pendiente</span><strong id="balanceTotal">$0,00</strong></div>
</div>
</section>

<section class="panel">
<h2>3. Comprobante PDF</h2>
<p class="small">El PDF se descarga directamente. En Chrome, revisá la carpeta Descargas.</p>
<div class="actions">
<button id="pdfBtn" class="primary" type="button">⬇ DESCARGAR COMPROBANTE PDF</button>
<button id="saveBtn" class="success" type="button">GUARDAR EN HISTORIAL</button>
<button id="newBtn" class="secondary" type="button">NUEVO COMPROBANTE</button>
</div>
<p id="message" class="small" aria-live="polite"></p>
</section>

<section class="panel">
<h2>4. Historial de ventas</h2>
<label for="searchHistory">Buscar por clienta o número</label>
<input id="searchHistory" placeholder="Escribí para buscar">
<div class="actions">
<button id="summaryBtn" class="secondary" type="button">DESCARGAR RESUMEN PDF</button>
<button id="backupBtn" class="secondary" type="button">EXPORTAR COPIA</button>
<button id="importBtn" class="secondary" type="button">IMPORTAR COPIA</button>
<input id="importFile" type="file" accept=".json,application/json" hidden>
</div>
<div id="history"></div>
</section>
</main>

<script>
'use strict';

const $ = id => document.getElementById(id);
let products = [];
let historyData = [];

try {
  const x = JSON.parse(localStorage.getItem('violetta_history') || '[]');
  if (Array.isArray(x)) historyData = x;
} catch(e) {
  historyData = [];
}

function money(n) {
  return new Intl.NumberFormat('es-AR', {
    style: 'currency',
    currency: 'ARS'
  }).format(Number(n) || 0);
}

function esc(v) {
  return String(v ?? '').replace(/[&<>"']/g, c => ({
    '&': '&amp;',
    '<': '&lt;',
    '>': '&gt;',
    '"': '&quot;',
    "'": '&#039;'
  }[c]));
}

function today() {
  const d = new Date();
  return d.getFullYear() + '-' +
    String(d.getMonth()+1).padStart(2,'0') + '-' +
    String(d.getDate()).padStart(2,'0');
}

function dateText(v) {
  if (!v) return '—';
  const p = v.split('-');
  return p.length === 3 ? p[2]+'/'+p[1]+'/'+p[0] : v;
}

function dateTimeText(d) {
  return d.toLocaleDateString('es-AR') + ' ' +
    d.toLocaleTimeString('es-AR', {
      hour: '2-digit',
      minute: '2-digit',
      second: '2-digit'
    });
}

function addDays(date, days) {
  const d = new Date((date || today()) + 'T12:00:00');
  d.setDate(d.getDate() + Math.max(0, Number(days) || 0));
  return d.getFullYear() + '-' +
    String(d.getMonth()+1).padStart(2,'0') + '-' +
    String(d.getDate()).padStart(2,'0');
}

function makeNumber() {
  const d = new Date();
  const stamp = '' + d.getFullYear() +
    String(d.getMonth()+1).padStart(2,'0') +
    String(d.getDate()).padStart(2,'0') +
    String(d.getHours()).padStart(2,'0') +
    String(d.getMinutes()).padStart(2,'0') +
    String(d.getSeconds()).padStart(2,'0') +
    String(d.getMilliseconds()).padStart(3,'0');

  return 'VC-' + stamp + '-' + Math.floor(1000 + Math.random()*9000);
}

function newNumber() {
  const d = new Date();
  $('invoiceNo').value = makeNumber();
  $('createdAt').value = dateTimeText(d);
}

function makeId() {
  return 'p' + Date.now() + Math.random().toString(36).slice(2,8);
}

function addProduct(data = {}) {
  products.push({
    id: makeId(),
    name: data.name || '',
    price: Math.max(0, Number(data.price) || 0),
    quantity: Math.max(1, Number(data.quantity) || 1),
    discount: Math.min(100, Math.max(0, Number(data.discount) || 0)),
    image: data.image || ''
  });
  renderProducts();
  updateTotals();
}

function renderProducts() {
  const root = $('products');
  root.innerHTML = '';

  products.forEach((p, index) => {
    const card = document.createElement('div');
    card.className = 'product';

    const head = document.createElement('div');
    head.className = 'product-head';

    const title = document.createElement('strong');
    title.textContent = 'Producto ' + (index+1);

    const remove = document.createElement('button');
    remove.type = 'button';
    remove.className = 'danger';
    remove.textContent = 'Eliminar';
    remove.addEventListener('click', () => {
      products.splice(index, 1);
      renderProducts();
      updateTotals();
    });

    head.append(title, remove);
    card.appendChild(head);

    const grid = document.createElement('div');
    grid.className = 'product-grid';

    const img = document.createElement('img');
    img.className = 'preview';
    img.alt = 'Foto del producto';
    img.src = p.image || 'data:image/svg+xml,' +
      encodeURIComponent(
        '<svg xmlns="http://www.w3.org/2000/svg" width="100" height="100">' +
        '<rect width="100%" height="100%" fill="#fff7fc"/>' +
        '<text x="50%" y="50%" font-size="12" text-anchor="middle" fill="#762d76">Sin foto</text></svg>'
      );
    grid.appendChild(img);

    function field(label, type, value, placeholder, handler) {
      const wrap = document.createElement('div');
      wrap.className = 'field';

      const l = document.createElement('label');
      l.textContent = label;

      const input = document.createElement('input');
      input.type = type;

      if (type !== 'file') input.value = value;
      if (placeholder) input.placeholder = placeholder;

      if (type === 'number') {
        input.min = '0';
        input.step = 'any';
      }

      input.addEventListener('input', () => handler(input));

      wrap.append(l, input);
      grid.appendChild(wrap);
    }

    field('Nombre del producto', 'text', p.name, 'Ej. Perfume',
      i => p.name = i.value);

    field('Foto del producto', 'file', '', '',
      i => {
        const f = i.files && i.files[0];
        if (!f) return;

        if (!f.type.startsWith('image/')) {
          alert('Elegí una imagen válida.');
          i.value = '';
          return;
        }

        const r = new FileReader();
        r.onload = () => {
          p.image = r.result;
          img.src = p.image;
        };
        r.readAsDataURL(f);
      });

    field('Precio unitario ($)', 'number', p.price, '',
      i => {
        p.price = Math.max(0, Number(i.value) || 0);
        updateTotals();
      });

    field('Cantidad', 'number', p.quantity, '',
      i => {
        p.quantity = Math.max(1, Math.floor(Number(i.value) || 1));
        updateTotals();
      });

    field('Descuento (%)', 'number', p.discount, '',
      i => {
        p.discount = Math.min(100, Math.max(0, Number(i.value) || 0));
        updateTotals();
      });

    card.appendChild(grid);

    const line = document.createElement('div');
    line.className = 'product-total';

    const a = document.createElement('span');
    a.textContent = 'Importe del producto';

    const b = document.createElement('span');
    b.id = 'line_' + p.id;

    line.append(a, b);
    card.appendChild(line);
    root.appendChild(card);
  });
}

function calculate() {
  let subtotal = 0;
  let total = 0;

  products.forEach(p => {
    const base = p.price * p.quantity;
    subtotal += base;
    total += base * (1 - p.discount/100);
  });

  const discount = subtotal - total;
  const paid = Math.min(
    Math.max(0, Number($('amountPaid').value) || 0),
    total
  );

  return {
    subtotal,
    discount,
    total,
    paid,
    balance: Math.max(0, total-paid)
  };
}

function updateTotals() {
  const t = calculate();

  $('subtotal').textContent = money(t.subtotal);
  $('discountTotal').textContent = money(t.discount);
  $('grandTotal').textContent = money(t.total);
  $('paidTotal').textContent = money(t.paid);
  $('balanceTotal').textContent = money(t.balance);

  products.forEach(p => {
    const e = $('line_' + p.id);
    if (e) {
      e.textContent = money(
        p.price * p.quantity * (1-p.discount/100)
      );
    }
  });
}

function syncStatus() {
  const t = calculate();
  $('paymentStatus').value =
    t.total > 0 && t.balance <= 0 ? 'paid' :
    t.paid > 0 ? 'partial' : 'pending';
  updateTotals();
}

function syncPaid() {
  const t = calculate();

  if ($('paymentStatus').value === 'paid') {
    $('amountPaid').value = t.total.toFixed(2);
  } else if ($('paymentStatus').value === 'pending') {
    $('amountPaid').value = '0';
  }

  updateTotals();
}

function getSale() {
  const t = calculate();

  return {
    id: $('invoiceNo').value.trim(),
    createdAt: $('createdAt').value,
    date: $('invoiceDate').value || today(),
    client: $('clientName').value.trim(),
    phone: $('clientPhone').value.trim(),
    dueDays: Number($('dueDays').value) || 0,
    dueDate: $('dueDate').value || '',
    status: t.balance <= 0 && t.total > 0 ? 'paid' :
      t.paid > 0 ? 'partial' : 'pending',
    amountPaid: t.paid,
    alias: $('paymentAlias').value.trim(),
    bank: $('bankName').value.trim(),
    notes: $('notes').value.trim(),
    products: products.map(p => ({...p})),
    subtotal: t.subtotal,
    discount: t.discount,
    total: t.total,
    balance: t.balance
  };
}

function invoiceHTML(s) {
  const status = s.status === 'paid' ? 'PAGADO' :
    s.status === 'partial' ? 'PAGO PARCIAL' : 'PENDIENTE DE PAGO';

  const rows = s.products.map(p => `
    <tr>
      <td style="padding:8px;border-bottom:1px solid #ead9e9">
        ${p.image ? `<img src="${p.image}" style="width:45px;height:45px;object-fit:contain;display:block">` : ''}
        ${esc(p.name || 'Producto')}
      </td>
      <td style="padding:8px;text-align:center;border-bottom:1px solid #ead9e9">${p.quantity}</td>
      <td style="padding:8px;text-align:right;border-bottom:1px solid #ead9e9">${money(p.price)}</td>
      <td style="padding:8px;text-align:center;border-bottom:1px solid #ead9e9">${p.discount}%</td>
      <td style="padding:8px;text-align:right;border-bottom:1px solid #ead9e9">${money(p.price*p.quantity*(1-p.discount/100))}</td>
    </tr>
  `).join('');

  return `
  <div style="font-family:Arial,sans-serif;color:#332536;background:white;padding:24px;width:100%">
    <div style="background:#762d76;color:white;padding:20px;text-align:center;border-radius:8px">
      <h1 style="margin:0;font-size:26px">VIOLETTA COSMÉTICOS</h1>
      <p>Comprobante de venta y pago</p>
    </div>
    <p><strong>Número de comprobante:</strong> ${esc(s.id)}</p>
    <p><strong>Fecha y hora de creación:</strong> ${esc(s.createdAt || '—')}</p>
    <p><strong>Fecha de emisión:</strong> ${dateText(s.date)}</p>
    <p><strong>Clienta:</strong> ${esc(s.client)}</p>
    <p><strong>Teléfono:</strong> ${esc(s.phone || 'No especificado')}</p>
    <p><strong>Estado:</strong> ${status}</p>
    <p><strong>Fecha límite de pago:</strong> ${dateText(s.dueDate)}</p>

    <h3 style="color:#762d76">Detalle de productos</h3>
    <table style="width:100%;border-collapse:collapse;font-size:12px">
      <thead>
        <tr style="background:#f7e5f4">
          <th style="padding:8px;text-align:left">Producto</th>
          <th style="padding:8px">Cant.</th>
          <th style="padding:8px;text-align:right">Precio</th>
          <th style="padding:8px">Desc.</th>
          <th style="padding:8px;text-align:right">Importe</th>
        </tr>
      </thead>
      <tbody>${rows}</tbody>
    </table>

    <div style="margin:20px 0 0 auto;max-width:320px">
      <p>Subtotal: <strong>${money(s.subtotal)}</strong></p>
      <p>Descuentos: <strong>${money(s.discount)}</strong></p>
      <p style="font-size:20px;color:#762d76"><strong>TOTAL: ${money(s.total)}</strong></p>
      <p>Abonado: <strong>${money(s.amountPaid)}</strong></p>
      <p style="color:${s.balance>0?'#b3213d':'#08743b'}"><strong>Saldo pendiente: ${money(s.balance)}</strong></p>
    </div>

    ${s.alias || s.bank ? `
      <div style="background:#fcf2fb;padding:12px;border-radius:8px">
        <h3 style="color:#762d76">Datos para pagar</h3>
        ${s.alias ? `<p><strong>Alias:</strong> ${esc(s.alias)}</p>` : ''}
        ${s.bank ? `<p><strong>Banco o billetera:</strong> ${esc(s.bank)}</p>` : ''}
      </div>
    ` : ''}

    ${s.notes ? `<p><strong>Observaciones:</strong> ${esc(s.notes)}</p>` : ''}

    ${s.balance > 0 ? `
      <div style="background:#fff0f2;padding:12px;margin-top:18px;border-left:4px solid #c92c49">
        <strong>Recordatorio de pago</strong>
        <p>Por favor, aboná el saldo pendiente antes de la fecha acordada.</p>
      </div>
    ` : `
      <div style="background:#e4f8eb;padding:12px;margin-top:18px;border-left:4px solid #16834a">
        <strong>¡Muchas gracias por tu compra!</strong>
        <p>Tu pago está completo. Gracias por elegir Violetta Cosméticos.</p>
      </div>
    `}

    <p style="text-align:center;color:#766878;font-size:10px;margin-top:25px">
      Comprobante de registro de venta no fiscal.
    </p>
  </div>`;
}

async function makePDF(html, filename, width='750px') {
  if (typeof html2pdf === 'undefined') {
    alert('No se pudo cargar el generador PDF. Conectate a internet y volvé a intentar.');
    return;
  }

  const holder = document.createElement('div');
  holder.style.position = 'fixed';
  holder.style.left = '-20000px';
  holder.style.top = '0';
  holder.style.width = width;
  holder.innerHTML = html;
  document.body.appendChild(holder);

  try {
    await html2pdf().set({
      margin: 8,
      filename,
      image: {type:'jpeg',quality:.95},
      html2canvas: {scale:1.5,useCORS:true,backgroundColor:'#fff'},
      jsPDF: {unit:'mm',format:'a4',orientation:'portrait'},
      pagebreak: {mode:['css','legacy']}
    }).from(holder).save();

    $('message').textContent = 'PDF generado. Revisá Descargas de Chrome.';
  } catch(e) {
    console.error(e);
    alert('No se pudo generar el PDF. Comprobá tu conexión.');
  } finally {
    holder.remove();
  }
}

async function downloadCurrentPDF() {
  const s = getSale();

  if (!s.client) {
    alert('Ingresá el nombre de la clienta.');
    $('clientName').focus();
    return;
  }

  if (!s.products.length) {
    alert('Agregá al menos un producto.');
    return;
  }

  await makePDF(invoiceHTML(s), 'Violetta_Comprobante_' + s.id + '.pdf');
}

function persist() {
  try {
    localStorage.setItem('violetta_history', JSON.stringify(historyData));
    return true;
  } catch(e) {
    alert('No se pudo guardar. Probá con fotos más pequeñas.');
    return false;
  }
}

function saveSale() {
  const s = getSale();

  if (!s.client) {
    alert('Ingresá el nombre de la clienta.');
    return;
  }

  if (!s.products.length) {
    alert('Agregá al menos un producto.');
    return;
  }

  const i = historyData.findIndex(x => String(x.id) === s.id);

  if (i >= 0) {
    if (!confirm('Este comprobante ya está guardado. ¿Querés actualizarlo?')) return;
    historyData[i] = s;
  } else {
    historyData.unshift(s);
  }

  if (persist()) {
    renderHistory();
    $('message').textContent = 'Comprobante guardado en este dispositivo.';
  }
}

function renderHistory() {
  const q = $('searchHistory').value.trim().toLowerCase();

  const arr = historyData.filter(s =>
    String(s.client || '').toLowerCase().includes(q) ||
    String(s.id || '').toLowerCase().includes(q)
  );

  $('history').innerHTML = '';

  if (!arr.length) {
    $('history').innerHTML = '<p class="small">No hay comprobantes guardados para mostrar.</p>';
    return;
  }

  arr.forEach(s => {
    const card = document.createElement('div');
    card.className = 'history-item';

    const h = document.createElement('h3');
    h.textContent = s.client || 'Sin nombre';

    const st = document.createElement('span');
    st.className = 'status ' + (s.status === 'paid' ? 'paid' : 'pending');
    st.textContent = s.status === 'paid' ? 'PAGADO' :
      s.status === 'partial' ? 'PAGO PARCIAL' : 'PENDIENTE';

    const p = document.createElement('p');
    p.className = 'small';
    p.textContent = 'N.º ' + s.id + ' · Creado: ' + (s.createdAt || '—');

    const t = document.createElement('p');
    t.textContent = 'Total: ' + money(s.total) +
      ' · Abonado: ' + money(s.amountPaid) +
      ' · Debe: ' + money(s.balance);

    const actions = document.createElement('div');
    actions.className = 'history-buttons';

    const pdf = document.createElement('button');
    pdf.className = 'primary';
    pdf.textContent = 'Descargar PDF';
    pdf.addEventListener('click', () =>
      makePDF(invoiceHTML(s), 'Violetta_Comprobante_' + s.id + '.pdf')
    );

    const load = document.createElement('button');
    load.className = 'secondary';
    load.textContent = 'Cargar / editar';
    load.addEventListener('click', () => loadSale(s.id));

    const del = document.createElement('button');
    del.className = 'danger';
    del.textContent = 'Eliminar';
    del.addEventListener('click', () => {
      if (confirm('¿Eliminar este comprobante del historial?')) {
        historyData = historyData.filter(x => String(x.id) !== String(s.id));
        if (persist()) renderHistory();
      }
    });

    actions.append(pdf, load, del);
    card.append(h, st, p, t, actions);
    $('history').appendChild(card);
  });
}

function loadSale(id) {
  const s = historyData.find(x => String(x.id) === String(id));
  if (!s) return;

  $('invoiceNo').value = s.id || '';
  $('createdAt').value = s.createdAt || '';
  $('invoiceDate').value = s.date || today();
  $('clientName').value = s.client || '';
  $('clientPhone').value = s.phone || '';
  $('dueDays').value = s.dueDays ?? 7;
  $('dueDate').value = s.dueDate || '';
  $('amountPaid').value = s.amountPaid || 0;
  $('paymentStatus').value = s.status || 'pending';
  $('paymentAlias').value = s.alias || '';
  $('bankName').value = s.bank || '';
  $('notes').value = s.notes || '';

  products = (s.products || []).map(p => ({...p,id:makeId()}));
  renderProducts();
  updateTotals();

  window.scrollTo({top:0,behavior:'smooth'});
  $('message').textContent = 'Comprobante cargado. Guardá para actualizar el historial.';
}

async function downloadSummary() {
  if (!historyData.length) {
    alert('Todavía no hay ventas guardadas.');
    return;
  }

  const total = historyData.reduce((a,s) => a + (Number(s.total)||0), 0);
  const paid = historyData.reduce((a,s) => a + (Number(s.amountPaid)||0), 0);
  const debt = historyData.reduce((a,s) => a + (Number(s.balance)||0), 0);

  const rows = historyData.map(s => `
    <tr>
      <td style="padding:7px;border-bottom:1px solid #ead9e9">${esc(s.client)}</td>
      <td style="padding:7px;border-bottom:1px solid #ead9e9">${esc(s.id)}</td>
      <td style="padding:7px;border-bottom:1px solid #ead9e9">${dateText(s.date)}</td>
      <td style="padding:7px;text-align:right;border-bottom:1px solid #ead9e9">${money(s.total)}</td>
      <td style="padding:7px;text-align:right;border-bottom:1px solid #ead9e9">${money(s.amountPaid)}</td>
      <td style="padding:7px;text-align:right;border-bottom:1px solid #ead9e9">${money(s.balance)}</td>
    </tr>
  `).join('');

  const html = `
  <div style="font-family:Arial;padding:22px;color:#332536;background:white">
    <div style="background:#762d76;color:white;padding:18px;text-align:center">
      <h1>VIOLETTA COSMÉTICOS</h1>
      <p>Resumen de ventas y pagos</p>
    </div>
    <p>Fecha: ${dateText(today())}</p>
    <p><strong>Total vendido:</strong> ${money(total)}</p>
    <p><strong>Total abonado:</strong> ${money(paid)}</p>
    <p><strong>Saldo pendiente:</strong> ${money(debt)}</p>
    <p><strong>Comprobantes:</strong> ${historyData.length}</p>
    <table style="width:100%;border-collapse:collapse;font-size:11px">
      <thead>
        <tr style="background:#f7e5f4">
          <th style="padding:7px">Clienta</th>
          <th style="padding:7px">N.º</th>
          <th style="padding:7px">Fecha</th>
          <th style="padding:7px">Total</th>
          <th style="padding:7px">Abonado</th>
          <th style="padding:7px">Debe</th>
        </tr>
      </thead>
      <tbody>${rows}</tbody>
    </table>
  </div>`;

  await makePDF(html, 'Violetta_Resumen_Ventas.pdf', '900px');
}

function newSale() {
  if (!confirm('¿Comenzar un comprobante nuevo?')) return;

  $('invoiceDate').value = today();
  $('clientName').value = '';
  $('clientPhone').value = '';
  $('dueDays').value = '7';
  $('dueDate').value = addDays(today(),7);
  $('paymentStatus').value = 'pending';
  $('amountPaid').value = '0';
  $('paymentAlias').value = '';
  $('bankName').value = '';
  $('notes').value = '';

  products = [];
  newNumber();
  addProduct();

  $('message').textContent = '';
  window.scrollTo({top:0,behavior:'smooth'});
}

function exportBackup() {
  const blob = new Blob(
    [JSON.stringify(historyData,null,2)],
    {type:'application/json'}
  );

  const url = URL.createObjectURL(blob);
  const a = document.createElement('a');
  a.href = url;
  a.download = 'Violetta_Copia_Seguridad.json';
  document.body.appendChild(a);
  a.click();
  a.remove();
  setTimeout(() => URL.revokeObjectURL(url),1000);
}

function importBackup(event) {
  const file = event.target.files && event.target.files[0];
  if (!file) return;

  const r = new FileReader();

  r.onload = () => {
    try {
      const data = JSON.parse(r.result);
      if (!Array.isArray(data)) throw Error();

      if (!confirm('La copia reemplazará el historial actual. ¿Continuar?')) return;

      historyData = data;

      if (persist()) {
        renderHistory();
        alert('Copia importada correctamente.');
      }
    } catch(e) {
      alert('El archivo no es una copia válida.');
    } finally {
      $('importFile').value = '';
    }
  };

  r.readAsText(file);
}

$('addProductBtn').addEventListener('click', () => addProduct());
$('pdfBtn').addEventListener('click', downloadCurrentPDF);
$('saveBtn').addEventListener('click', saveSale);
$('newBtn').addEventListener('click', newSale);
$('summaryBtn').addEventListener('click', downloadSummary);
$('backupBtn').addEventListener('click', exportBackup);
$('importBtn').addEventListener('click', () => $('importFile').click());
$('importFile').addEventListener('change', importBackup);
$('searchHistory').addEventListener('input', renderHistory);
$('amountPaid').addEventListener('input', syncStatus);
$('paymentStatus').addEventListener('change', syncPaid);

$('invoiceDate').addEventListener('change', () => {
  $('dueDate').value = addDays($('invoiceDate').value,$('dueDays').value);
});

$('dueDays').addEventListener('change', () => {
  $('dueDate').value = addDays($('invoiceDate').value,$('dueDays').value);
});

$('invoiceDate').value = today();
$('dueDate').value = addDays(today(),7);
newNumber();
addProduct();
renderHistory();
updateTotals();
</script>
</body>
</html>
