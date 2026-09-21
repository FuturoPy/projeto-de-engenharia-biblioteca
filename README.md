<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Acervo — Biblioteca de Projetos</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Spectral:ital,wght@0,400;0,500;0,600;0,700;1,400&family=Work+Sans:wght@400;500;600;700&display=swap" rel="stylesheet">
<style>
  :root{
    --ink:#221f1a;
    --paper:#efe4cc;
    --paper-dark:#e3d5b3;
    --wood:#2c221a;
    --wood-light:#3b2f24;
    --brass:#a9782f;
    --brass-light:#c99a4b;
    --teal:#3f6c63;
    --rust:#a6462f;
    --slate:#5c6e78;
    --line:rgba(34,31,26,0.18);
  }
  *{box-sizing:border-box;}
  html,body{margin:0;padding:0;}
  body{
    background:var(--wood);
    background-image:linear-gradient(180deg, var(--wood) 0%, var(--wood-light) 100%);
    color:var(--ink);
    font-family:'Work Sans', sans-serif;
    min-height:100vh;
    padding:32px 20px 80px;
  }
  .wrap{max-width:1080px;margin:0 auto;}

  header{
    display:flex;align-items:flex-end;justify-content:space-between;
    gap:24px;margin-bottom:28px;flex-wrap:wrap;
  }
  .brand h1{
    font-family:'Spectral', serif;font-weight:600;font-size:2.4rem;
    color:var(--paper);margin:0 0 4px;letter-spacing:0.2px;
  }
  .brand p{color:#c9bfa8;margin:0;font-size:0.98rem;max-width:480px;line-height:1.5;}
  .head-right{display:flex;align-items:center;gap:22px;flex-wrap:wrap;}
  .stats{display:flex;gap:18px;}
  .stat{text-align:center;color:var(--paper);min-width:64px;}
  .stat .n{font-family:'Spectral',serif;font-size:1.6rem;font-weight:600;display:block;color:var(--brass-light);}
  .stat .l{font-size:0.72rem;color:#c9bfa8;}

  .mode-toggle{
    display:flex;background:rgba(0,0,0,0.25);border-radius:20px;padding:3px;
  }
  .mode-toggle button{
    border:none;background:none;color:#c9bfa8;font-family:'Work Sans',sans-serif;
    font-size:0.82rem;font-weight:600;padding:7px 14px;border-radius:16px;cursor:pointer;
    transition:background .15s ease, color .15s ease;
  }
  .mode-toggle button.active{background:var(--brass);color:#fff;}

  .drawer{display:flex;gap:6px;overflow-x:auto;padding-bottom:2px;}
  .tab{
    background:var(--paper-dark);border:none;border-radius:8px 8px 0 0;
    padding:12px 20px 14px;font-family:'Spectral', serif;font-size:0.98rem;font-weight:600;
    color:#786a4d;cursor:pointer;position:relative;top:2px;
    transition:background .15s ease, color .15s ease;white-space:nowrap;
  }
  .tab:hover{color:var(--ink);}
  .tab.active{background:var(--paper);color:var(--ink);box-shadow:0 -2px 0 var(--brass) inset;}
  .tab .count{font-family:'Work Sans',sans-serif;font-weight:500;font-size:0.75rem;color:#9a8c6a;margin-left:6px;}
  .tab.active .count{color:var(--brass);}

  .panel{background:var(--paper);border-radius:0 10px 10px 10px;padding:22px;box-shadow:0 20px 40px rgba(0,0,0,0.35);}

  .toolbar{display:flex;gap:12px;flex-wrap:wrap;align-items:center;margin-bottom:20px;padding-bottom:18px;border-bottom:1px dashed var(--line);}
  .search{flex:1 1 220px;display:flex;align-items:center;background:#fff;border:1px solid var(--line);border-radius:6px;padding:9px 12px;gap:8px;}
  .search svg{flex:none;opacity:0.5;}
  .search input{border:none;outline:none;background:transparent;font-family:'Work Sans',sans-serif;font-size:0.95rem;color:var(--ink);width:100%;}
  select#sortSelect{font-family:'Work Sans',sans-serif;font-size:0.9rem;padding:9px 12px;border-radius:6px;border:1px solid var(--line);background:#fff;color:var(--ink);cursor:pointer;}
  .btn-new{background:var(--brass);color:#fff;border:none;border-radius:6px;padding:10px 18px;font-family:'Work Sans',sans-serif;font-weight:600;font-size:0.92rem;cursor:pointer;transition:background .15s ease;}
  .btn-new:hover{background:#8f631f;}

  .empty{text-align:center;padding:60px 20px;color:#8a7c5c;}
  .empty h3{font-family:'Spectral',serif;color:var(--ink);margin-bottom:6px;font-size:1.3rem;}
  .empty p{margin:0 0 18px;font-size:0.92rem;}

  .grid{display:grid;grid-template-columns:repeat(auto-fill, minmax(250px, 1fr));gap:16px;}
  .card{background:#fff;border:1px solid var(--line);border-radius:8px;overflow:hidden;position:relative;display:flex;flex-direction:column;transition:box-shadow .15s ease, transform .15s ease;}
  .card:hover{box-shadow:0 10px 22px rgba(34,31,26,0.12);transform:translateY(-2px);}

  .cover{
    width:100%;aspect-ratio:4/3;background:var(--paper-dark);
    display:flex;align-items:center;justify-content:center;overflow:hidden;cursor:pointer;position:relative;
  }
  .cover img{width:100%;height:100%;object-fit:cover;}
  .cover .no-img{color:#a99a76;font-size:0.78rem;font-family:'Spectral',serif;}
  .cover .more{
    position:absolute;bottom:6px;right:6px;background:rgba(34,31,26,0.7);color:#fff;
    font-size:0.7rem;padding:2px 7px;border-radius:10px;font-weight:600;
  }

  .card-body{padding:14px 16px 14px;display:flex;flex-direction:column;gap:8px;flex:1;}
  .card-top{display:flex;justify-content:space-between;align-items:flex-start;gap:8px;}
  .card h3{font-family:'Spectral', serif;font-size:1.1rem;font-weight:600;margin:0;line-height:1.3;color:var(--ink);}
  .badge{font-size:0.66rem;font-weight:600;padding:4px 9px;border-radius:20px;white-space:nowrap;flex:none;}
  .badge.interessado{background:#fbe9d9;color:var(--brass);}
  .badge.atual{background:#dcece7;color:var(--teal);}
  .badge.antigo{background:#efe0dc;color:var(--rust);}

  .card .cliente{font-size:0.9rem;color:var(--slate);}
  .card .cliente b{color:var(--ink);font-weight:600;}
  .card .meta{font-size:0.78rem;color:#9a8c6a;display:flex;gap:10px;flex-wrap:wrap;}
  .card .desc{font-size:0.85rem;color:#5a5344;line-height:1.5;margin:2px 0 4px;display:-webkit-box;-webkit-line-clamp:3;-webkit-box-orient:vertical;overflow:hidden;}
  .card a.link{font-size:0.82rem;color:var(--brass);text-decoration:none;font-weight:600;}
  .card a.link:hover{text-decoration:underline;}
  .card-actions{display:flex;gap:8px;margin-top:auto;padding-top:10px;border-top:1px solid var(--line);}
  .card-actions button{flex:1;background:none;border:1px solid var(--line);border-radius:6px;padding:6px 0;font-size:0.78rem;font-family:'Work Sans',sans-serif;font-weight:600;color:var(--slate);cursor:pointer;transition:background .15s ease, color .15s ease;}
  .card-actions button:hover{background:#f5efe0;color:var(--ink);}
  .card-actions button.del:hover{background:#f6e4de;color:var(--rust);border-color:#e5c3b6;}

  .overlay{position:fixed;inset:0;background:rgba(20,17,12,0.55);display:none;align-items:center;justify-content:center;padding:20px;z-index:50;}
  .overlay.open{display:flex;}
  .modal{background:var(--paper);border-radius:10px;max-width:500px;width:100%;padding:26px 26px 22px;box-shadow:0 30px 60px rgba(0,0,0,0.45);max-height:88vh;overflow-y:auto;}
  .modal h2{font-family:'Spectral',serif;font-size:1.4rem;margin:0 0 18px;color:var(--ink);}
  .field{margin-bottom:14px;}
  .field label{display:block;font-size:0.78rem;font-weight:600;color:var(--slate);margin-bottom:5px;}
  .field input, .field textarea, .field select{width:100%;font-family:'Work Sans',sans-serif;font-size:0.92rem;padding:9px 11px;border:1px solid var(--line);border-radius:6px;background:#fff;color:var(--ink);resize:vertical;}
  .row2{display:grid;grid-template-columns:1fr 1fr;gap:12px;}
  .field textarea{min-height:70px;}
  .modal-actions{display:flex;justify-content:flex-end;gap:10px;margin-top:18px;}
  .modal-actions button{padding:10px 18px;border-radius:6px;border:none;font-family:'Work Sans',sans-serif;font-weight:600;font-size:0.9rem;cursor:pointer;}
  .btn-cancel{background:transparent;color:var(--slate);border:1px solid var(--line) !important;}
  .btn-save{background:var(--brass);color:#fff;}
  .btn-save:hover{background:#8f631f;}
  .btn-save:disabled{opacity:0.6;cursor:not-allowed;}

  .img-drop{
    border:2px dashed var(--line);border-radius:8px;padding:16px;text-align:center;
    cursor:pointer;font-size:0.85rem;color:var(--slate);background:#fbf7ec;
  }
  .img-drop:hover{border-color:var(--brass);color:var(--brass);}
  .img-drop input{display:none;}
  .thumbs{display:flex;gap:8px;flex-wrap:wrap;margin-top:10px;}
  .thumb{position:relative;width:64px;height:64px;border-radius:6px;overflow:hidden;border:1px solid var(--line);}
  .thumb img{width:100%;height:100%;object-fit:cover;}
  .thumb .rm{
    position:absolute;top:2px;right:2px;background:rgba(20,17,12,0.7);color:#fff;
    border:none;border-radius:50%;width:18px;height:18px;font-size:11px;line-height:1;cursor:pointer;
  }
  .hint{font-size:0.72rem;color:#9a8c6a;margin-top:6px;}
  .budget-bar{height:6px;border-radius:4px;background:#e6dcc2;margin-top:10px;overflow:hidden;}
  .budget-bar-fill{height:100%;background:var(--brass);width:0%;transition:width .2s ease, background .2s ease;}
  .budget-bar-fill.warn{background:var(--rust);}

  .status-msg{position:fixed;bottom:22px;left:50%;transform:translateX(-50%);background:var(--ink);color:var(--paper);padding:10px 20px;border-radius:6px;font-size:0.85rem;opacity:0;pointer-events:none;transition:opacity .25s ease;z-index:60;max-width:90vw;text-align:center;}
  .status-msg.show{opacity:1;}

  .lightbox{position:fixed;inset:0;background:rgba(10,8,5,0.9);display:none;align-items:center;justify-content:center;z-index:70;padding:30px;}
  .lightbox.open{display:flex;}
  .lightbox img{max-width:90vw;max-height:80vh;border-radius:6px;box-shadow:0 20px 50px rgba(0,0,0,0.5);}
  .lightbox-nav{position:absolute;top:0;bottom:0;width:15%;display:flex;align-items:center;justify-content:center;cursor:pointer;color:#fff;font-size:2rem;opacity:0.6;}
  .lightbox-nav:hover{opacity:1;}
  .lightbox-nav.prev{left:0;}
  .lightbox-nav.next{right:0;}
  .lightbox-close{position:absolute;top:18px;right:24px;color:#fff;font-size:1.6rem;cursor:pointer;background:none;border:none;}
  .lightbox-count{position:absolute;bottom:18px;left:50%;transform:translateX(-50%);color:#dcd0b6;font-size:0.8rem;}

  .banner-cliente{
    background:var(--teal);color:#fff;text-align:center;padding:8px 14px;border-radius:6px;
    font-size:0.82rem;margin-bottom:16px;
  }

  @media (max-width:600px){
    .row2{grid-template-columns:1fr;}
    header{flex-direction:column;align-items:flex-start;}
  }
</style>
</head>
<body>
<div class="wrap">

  <header>
    <div class="brand">
      <h1>Acervo</h1>
      <p>Sua biblioteca de projetos — organize, acompanhe interessados e mostre seu trabalho aos clientes.</p>
    </div>
    <div class="head-right">
      <div class="stats" id="stats"></div>
      <div class="mode-toggle" id="modeToggle">
        <button id="modeEdicao" class="active">Você</button>
        <button id="modeCliente">Cliente</button>
      </div>
    </div>
  </header>

  <div id="clienteBanner" class="banner-cliente" style="display:none;">Modo de visualização — apenas para mostrar seus projetos, sem opções de edição.</div>

  <div class="drawer" id="drawer">
    <button class="tab active" data-filter="todos">Todos <span class="count" id="c-todos"></span></button>
    <button class="tab" data-filter="interessado">Interessados <span class="count" id="c-interessado"></span></button>
    <button class="tab" data-filter="atual">Clientes atuais <span class="count" id="c-atual"></span></button>
    <button class="tab" data-filter="antigo">Clientes antigos <span class="count" id="c-antigo"></span></button>
  </div>

  <div class="panel">
    <div class="toolbar">
      <div class="search">
        <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><circle cx="11" cy="11" r="7"/><line x1="21" y1="21" x2="16.65" y2="16.65"/></svg>
        <input type="text" id="searchInput" placeholder="Buscar por projeto ou cliente...">
      </div>
      <select id="sortSelect">
        <option value="data_desc">Mais recente primeiro</option>
        <option value="data_asc">Mais antigo primeiro</option>
        <option value="alfabetica">Ordem alfabética</option>
        <option value="cliente">Nome do cliente</option>
        <option value="status">Status</option>
      </select>
      <button class="btn-new" id="btnNew">+ Nova ficha</button>
    </div>

    <div id="gridArea"></div>
  </div>

</div>

<div class="overlay" id="overlay">
  <div class="modal">
    <h2 id="modalTitle">Nova ficha</h2>
    <input type="hidden" id="editId">
    <div class="field">
      <label for="fTitulo">Nome do projeto</label>
      <input type="text" id="fTitulo" placeholder="Ex: Identidade visual — Padaria Trigo">
    </div>
    <div class="field">
      <label for="fCliente">Nome do cliente</label>
      <input type="text" id="fCliente" placeholder="Ex: Maria Souza">
    </div>
    <div class="row2">
      <div class="field">
        <label for="fData">Data</label>
        <input type="date" id="fData">
      </div>
      <div class="field">
        <label for="fHora">Hora</label>
        <input type="time" id="fHora">
      </div>
    </div>
    <div class="field">
      <label for="fStatus">Status do cliente</label>
      <select id="fStatus">
        <option value="interessado">Interessado</option>
        <option value="atual">Cliente atual</option>
        <option value="antigo">Cliente antigo</option>
      </select>
    </div>
    <div class="field">
      <label for="fLink">Link do projeto (opcional)</label>
      <input type="text" id="fLink" placeholder="https://...">
    </div>
    <div class="field">
      <label>Imagens do projeto</label>
      <label class="img-drop" id="imgDrop">
        Clique para adicionar imagens (até 8)
        <input type="file" id="fImagens" accept="image/*" multiple>
      </label>
      <div class="thumbs" id="thumbsArea"></div>
      <div class="budget-bar"><div class="budget-bar-fill" id="budgetBarFill"></div></div>
      <div class="hint" id="budgetHint">As imagens são redimensionadas e comprimidas automaticamente.</div>
    </div>
    <div class="field">
      <label for="fDesc">Notas / descrição</label>
      <textarea id="fDesc" placeholder="Detalhes do projeto, observações sobre o cliente, próximos passos..."></textarea>
    </div>
    <div class="modal-actions">
      <button class="btn-cancel" id="btnCancel">Cancelar</button>
      <button class="btn-save" id="btnSave">Salvar ficha</button>
    </div>
  </div>
</div>

<div class="lightbox" id="lightbox">
  <button class="lightbox-close" id="lbClose">&times;</button>
  <div class="lightbox-nav prev" id="lbPrev">&#8249;</div>
  <img id="lbImg" src="" alt="">
  <div class="lightbox-nav next" id="lbNext">&#8250;</div>
  <div class="lightbox-count" id="lbCount"></div>
</div>

<div class="status-msg" id="statusMsg"></div>

<script>
const INDEX_KEY = 'projetos-index';
let projetos = [];
let currentFilter = 'todos';
let currentSort = 'data_desc';
let currentSearch = '';
let viewMode = 'edicao'; // 'edicao' | 'cliente'
let pendingImages = [];
let lightboxImages = [];
let lightboxIndex = 0;
let isClienteLink = false; // true quando aberto via link ?cliente=1 — trava no modo cliente

const gridArea = document.getElementById('gridArea');
const overlay = document.getElementById('overlay');
const statusMsg = document.getElementById('statusMsg');
const lightbox = document.getElementById('lightbox');

function showMsg(text){
  statusMsg.textContent = text;
  statusMsg.classList.add('show');
  setTimeout(()=>statusMsg.classList.remove('show'), 3400);
}

function uid(){
  return 'p_' + Date.now().toString(36) + Math.random().toString(36).slice(2,7);
}

// ---------- Storage ----------
// Usa window.storage quando existir (ambiente do Claude). Fora dele (ex.: GitHub Pages)
// usa IndexedDB, que guarda os dados no navegador com muito mais espaço.
const HAS_PLATFORM_STORAGE = typeof window.storage !== 'undefined'
  && window.storage && typeof window.storage.get === 'function';

let dbPromise = null;
function openDB(){
  if(!dbPromise){
    dbPromise = new Promise((resolve, reject)=>{
      const req = indexedDB.open('acervo-db', 1);
      req.onupgradeneeded = ()=> req.result.createObjectStore('kv');
      req.onsuccess = ()=> resolve(req.result);
      req.onerror = ()=> reject(req.error);
    });
  }
  return dbPromise;
}
function idbRun(mode, fn){
  return openDB().then(db => new Promise((resolve, reject)=>{
    const tx = db.transaction('kv', mode);
    const req = fn(tx.objectStore('kv'));
    tx.oncomplete = ()=> resolve(req.result);
    tx.onerror = ()=> reject(tx.error);
    tx.onabort = ()=> reject(tx.error);
  }));
}

const store = HAS_PLATFORM_STORAGE ? {
  get: (k)=> window.storage.get(k, true),
  set: (k, v)=> window.storage.set(k, v, true),
  del: (k)=> window.storage.delete(k, true)
} : {
  get: async (k)=>{
    const v = await idbRun('readonly', s => s.get(k));
    return v === undefined ? null : { key:k, value:v };
  },
  set: async (k, v)=>{ await idbRun('readwrite', s => s.put(v, k)); return { key:k, value:v }; },
  del: async (k)=>{ await idbRun('readwrite', s => s.delete(k)); return { key:k, deleted:true }; }
};

async function loadData(){
  try{
    const idxRes = await store.get(INDEX_KEY);
    const ids = idxRes && idxRes.value ? JSON.parse(idxRes.value) : [];
    const results = await Promise.all(ids.map(async id=>{
      try{
        const r = await store.get('projeto:'+id);
        return r && r.value ? JSON.parse(r.value) : null;
      }catch(e){ return null; }
    }));
    projetos = results.filter(Boolean);
  }catch(e){
    projetos = [];
  }
  render();
}

async function saveIndex(){
  const ids = projetos.map(p=>p.id);
  try{
    await store.set(INDEX_KEY, JSON.stringify(ids));
  }catch(e){
    showMsg('Não foi possível atualizar o índice do acervo.');
  }
}

async function saveProjetoData(p){
  try{
    await store.set('projeto:'+p.id, JSON.stringify(p));
  }catch(e){
    showMsg('Não foi possível salvar a ficha. Tente remover uma imagem e salvar de novo.');
    throw e;
  }
}

async function deleteProjetoData(id){
  try{
    await store.del('projeto:'+id);
  }catch(e){ /* ok mesmo se já não existir */ }
}

// ---------- Image handling ----------
// No Claude, cada ficha é UM registro de no máximo ~5MB (soma de todas as imagens).
// Fora dele (IndexedDB) o limite é bem maior. Os valores abaixo são em BYTES/CARACTERES reais.
const IMG_MAX_DIM = 1600;          // maior lado da imagem, em pixels
const IMG_START_QUALITY = 0.8;     // qualidade JPEG inicial
const IMG_MIN_QUALITY = 0.4;       // qualidade mínima antes de reduzir resolução
const IMG_MAX_BYTES = 320000;      // ~320KB por imagem (decodificada)
const RECORD_IMAGE_BUDGET = HAS_PLATFORM_STORAGE ? 4200000 : 20000000;  // soma das imagens (base64)
const RECORD_SAFE_LIMIT   = HAS_PLATFORM_STORAGE ? 4800000 : 25000000;  // ficha inteira

function loadImageFromFile(file){
  return new Promise((resolve, reject)=>{
    const reader = new FileReader();
    reader.onload = e=>{
      const img = new Image();
      img.onload = ()=>resolve(img);
      img.onerror = ()=>reject(new Error('Não foi possível ler essa imagem.'));
      img.src = e.target.result;
    };
    reader.onerror = ()=>reject(new Error('Não foi possível ler esse arquivo.'));
    reader.readAsDataURL(file);
  });
}

function estimateBytes(dataUrl){
  return Math.round(dataUrl.length * 0.75);
}

async function compressImage(file){
  const img = await loadImageFromFile(file);
  const w = img.width, h = img.height;

  const fit = (maxDim)=>{
    let nw = w, nh = h;
    if(nw > nh && nw > maxDim){ nh = Math.round(nh * (maxDim/nw)); nw = maxDim; }
    else if(nh >= nw && nh > maxDim){ nw = Math.round(nw * (maxDim/nh)); nh = maxDim; }
    return {nw, nh};
  };

  let maxDim = IMG_MAX_DIM;
  let quality = IMG_START_QUALITY;
  let dataUrl = '';

  for(let attempt = 0; attempt < 12; attempt++){
    const {nw, nh} = fit(maxDim);
    const canvas = document.createElement('canvas');
    canvas.width = nw; canvas.height = nh;
    const ctx = canvas.getContext('2d');
    ctx.fillStyle = '#fff'; // evita fundo preto em PNG transparente
    ctx.fillRect(0, 0, nw, nh);
    ctx.drawImage(img, 0, 0, nw, nh);
    dataUrl = canvas.toDataURL('image/jpeg', quality);

    if(estimateBytes(dataUrl) <= IMG_MAX_BYTES) return dataUrl;

    if(quality > IMG_MIN_QUALITY){
      quality -= 0.1;
    }else{
      maxDim = Math.round(maxDim * 0.8);
      quality = 0.6;
    }
  }
  return dataUrl;
}

function totalPendingImageChars(){
  return pendingImages.reduce((sum, src)=> sum + src.length, 0);
}

function updateBudgetBar(){
  const used = totalPendingImageChars();
  const pct = Math.min(100, Math.round((used / RECORD_IMAGE_BUDGET) * 100));
  const fill = document.getElementById('budgetBarFill');
  const hint = document.getElementById('budgetHint');
  fill.style.width = pct + '%';
  fill.classList.toggle('warn', pct >= 85);
  const usedMB = (used/1000000).toFixed(1);
  const totalMB = (RECORD_IMAGE_BUDGET/1000000).toFixed(1);
  hint.textContent = pct >= 85
    ? `Espaço quase no limite (${usedMB}MB de ${totalMB}MB) — evite adicionar mais imagens.`
    : `Espaço usado pelas imagens: ${usedMB}MB de ${totalMB}MB disponíveis.`;
}

function renderThumbs(){
  const area = document.getElementById('thumbsArea');
  area.innerHTML = pendingImages.map((src, i)=>`
    <div class="thumb">
      <img src="${src}">
      <button class="rm" type="button" data-i="${i}">&times;</button>
    </div>`).join('');
  area.querySelectorAll('.rm').forEach(btn=>{
    btn.addEventListener('click', ()=>{
      pendingImages.splice(parseInt(btn.getAttribute('data-i')), 1);
      renderThumbs();
    });
  });
  updateBudgetBar();
}

document.getElementById('fImagens').addEventListener('change', async e=>{
  const files = Array.from(e.target.files).slice(0, 8 - pendingImages.length);
  const saveBtn = document.getElementById('btnSave');
  let falhas = 0;
  let estourou = 0;
  saveBtn.disabled = true;
  for(const file of files){
    try{
      const compressed = await compressImage(file);
      if(totalPendingImageChars() + compressed.length > RECORD_IMAGE_BUDGET){
        estourou++;
        continue;
      }
      pendingImages.push(compressed);
      renderThumbs();
    }catch(err){
      falhas++;
    }
  }
  saveBtn.disabled = false;
  if(falhas > 0) showMsg(`${falhas} imagem(ns) não puderam ser processadas.`);
  if(estourou > 0) showMsg(`${estourou} imagem(ns) não coube(ram) — o espaço desta ficha acabou. Remova alguma imagem para adicionar outra.`);
  e.target.value = '';
});

// ---------- Rendering ----------
function statusLabel(s){
  return s === 'interessado' ? 'Interessado' : s === 'atual' ? 'Cliente atual' : 'Cliente antigo';
}
function formatDate(d, h){
  if(!d) return 'Sem data';
  const [y,m,day] = d.split('-');
  let out = `${day}/${m}/${y}`;
  if(h) out += ` às ${h}`;
  return out;
}
function escapeHtml(str){
  const div = document.createElement('div');
  div.textContent = str || '';
  return div.innerHTML.replace(/"/g, '&quot;');
}

function updateCounts(){
  const counts = {todos: projetos.length, interessado:0, atual:0, antigo:0};
  projetos.forEach(p => { if(counts[p.status] !== undefined) counts[p.status]++; });
  document.getElementById('c-todos').textContent = counts.todos;
  document.getElementById('c-interessado').textContent = counts.interessado;
  document.getElementById('c-atual').textContent = counts.atual;
  document.getElementById('c-antigo').textContent = counts.antigo;
  document.getElementById('stats').innerHTML = `
    <div class="stat"><span class="n">${counts.todos}</span><span class="l">projetos</span></div>
    <div class="stat"><span class="n">${counts.interessado}</span><span class="l">interessados</span></div>
    <div class="stat"><span class="n">${counts.antigo}</span><span class="l">antigos</span></div>
  `;
}

function getFiltered(){
  let list = [...projetos];
  if(currentFilter !== 'todos') list = list.filter(p => p.status === currentFilter);
  if(currentSearch.trim()){
    const q = currentSearch.trim().toLowerCase();
    list = list.filter(p => (p.titulo||'').toLowerCase().includes(q) || (p.cliente||'').toLowerCase().includes(q));
  }
  list.sort((a,b)=>{
    switch(currentSort){
      case 'alfabetica': return (a.titulo||'').localeCompare(b.titulo||'', 'pt-BR');
      case 'cliente': return (a.cliente||'').localeCompare(b.cliente||'', 'pt-BR');
      case 'status': return statusLabel(a.status).localeCompare(statusLabel(b.status), 'pt-BR');
      case 'data_asc': return (a.data||'') + (a.hora||'') > (b.data||'') + (b.hora||'') ? 1 : -1;
      case 'data_desc':
      default: return (a.data||'') + (a.hora||'') < (b.data||'') + (b.hora||'') ? 1 : -1;
    }
  });
  return list;
}

function render(){
  updateCounts();
  const list = getFiltered();

  if(list.length === 0){
    gridArea.innerHTML = `
      <div class="empty">
        <h3>Nenhuma ficha por aqui</h3>
        <p>${projetos.length === 0 ? 'Comece adicionando seu primeiro projeto ao acervo.' : 'Nada corresponde a esse filtro ou busca.'}</p>
      </div>`;
    return;
  }

  gridArea.innerHTML = `<div class="grid">${list.map(cardHtml).join('')}</div>`;

  gridArea.querySelectorAll('[data-edit]').forEach(btn=>{
    btn.addEventListener('click', ()=> openModal(btn.getAttribute('data-edit')));
  });
  gridArea.querySelectorAll('[data-del]').forEach(btn=>{
    btn.addEventListener('click', ()=> deleteProjeto(btn.getAttribute('data-del')));
  });
  gridArea.querySelectorAll('[data-cover]').forEach(el=>{
    el.addEventListener('click', ()=>{
      const p = projetos.find(x=>x.id===el.getAttribute('data-cover'));
      if(p && p.imagens && p.imagens.length) openLightbox(p.imagens, 0);
    });
  });
}

function cardHtml(p){
  const imgs = p.imagens || [];
  const coverHtml = imgs.length
    ? `<img src="${imgs[0]}" alt="${escapeHtml(p.titulo)}">${imgs.length>1 ? `<span class="more">+${imgs.length-1}</span>` : ''}`
    : `<span class="no-img">Sem imagens</span>`;

  const actions = viewMode === 'edicao' ? `
      <div class="card-actions">
        <button data-edit="${p.id}">Editar</button>
        <button class="del" data-del="${p.id}">Excluir</button>
      </div>` : '';

  const safeLink = /^https?:\/\//i.test(p.link || '') ? p.link : (p.link ? 'https://' + p.link : '');

  return `
    <div class="card">
      <div class="cover" ${imgs.length ? `data-cover="${p.id}"` : ''}>${coverHtml}</div>
      <div class="card-body">
        <div class="card-top">
          <h3>${escapeHtml(p.titulo)}</h3>
          <span class="badge ${p.status}">${statusLabel(p.status)}</span>
        </div>
        <div class="cliente">Cliente: <b>${escapeHtml(p.cliente)}</b></div>
        <div class="meta"><span>${formatDate(p.data, p.hora)}</span></div>
        ${p.descricao ? `<div class="desc">${escapeHtml(p.descricao)}</div>` : ''}
        ${safeLink ? `<a class="link" href="${escapeHtml(safeLink)}" target="_blank" rel="noopener">Ver projeto ↗</a>` : ''}
        ${actions}
      </div>
    </div>`;
}

// ---------- Lightbox ----------
function openLightbox(imgs, startIndex){
  lightboxImages = imgs;
  lightboxIndex = startIndex;
  updateLightbox();
  lightbox.classList.add('open');
}
function updateLightbox(){
  document.getElementById('lbImg').src = lightboxImages[lightboxIndex];
  document.getElementById('lbCount').textContent = `${lightboxIndex+1} / ${lightboxImages.length}`;
  const multi = lightboxImages.length > 1;
  document.getElementById('lbPrev').style.display = multi ? 'flex' : 'none';
  document.getElementById('lbNext').style.display = multi ? 'flex' : 'none';
}
document.getElementById('lbClose').addEventListener('click', ()=>lightbox.classList.remove('open'));
document.getElementById('lbPrev').addEventListener('click', ()=>{ lightboxIndex = (lightboxIndex-1+lightboxImages.length)%lightboxImages.length; updateLightbox(); });
document.getElementById('lbNext').addEventListener('click', ()=>{ lightboxIndex = (lightboxIndex+1)%lightboxImages.length; updateLightbox(); });
lightbox.addEventListener('click', e=>{ if(e.target === lightbox) lightbox.classList.remove('open'); });

// ---------- Modal ----------
function openModal(id){
  document.getElementById('modalTitle').textContent = id ? 'Editar ficha' : 'Nova ficha';
  document.getElementById('editId').value = id || '';
  pendingImages = [];
  if(id){
    const p = projetos.find(x=>x.id===id);
    document.getElementById('fTitulo').value = p.titulo || '';
    document.getElementById('fCliente').value = p.cliente || '';
    document.getElementById('fData').value = p.data || '';
    document.getElementById('fHora').value = p.hora || '';
    document.getElementById('fStatus').value = p.status || 'interessado';
    document.getElementById('fLink').value = p.link || '';
    document.getElementById('fDesc').value = p.descricao || '';
    pendingImages = [...(p.imagens || [])];
  }else{
    ['fTitulo','fCliente','fData','fHora','fLink','fDesc'].forEach(fid=>document.getElementById(fid).value='');
    document.getElementById('fStatus').value = 'interessado';
    document.getElementById('fData').value = new Date().toISOString().slice(0,10);
  }
  renderThumbs();
  overlay.classList.add('open');
  document.getElementById('fTitulo').focus();
}
function closeModal(){ overlay.classList.remove('open'); }

async function saveProjeto(){
  const titulo = document.getElementById('fTitulo').value.trim();
  const cliente = document.getElementById('fCliente').value.trim();
  if(!titulo || !cliente){
    showMsg('Preencha ao menos o nome do projeto e do cliente.');
    return;
  }
  const id = document.getElementById('editId').value;
  const data = {
    id: id || uid(),
    titulo, cliente,
    data: document.getElementById('fData').value,
    hora: document.getElementById('fHora').value,
    status: document.getElementById('fStatus').value,
    link: document.getElementById('fLink').value.trim(),
    descricao: document.getElementById('fDesc').value.trim(),
    imagens: [...pendingImages]
  };

  const payloadSize = JSON.stringify(data).length;
  if(payloadSize > RECORD_SAFE_LIMIT){
    const mb = (payloadSize/1000000).toFixed(1);
    showMsg(`Essa ficha ficou com ${mb}MB, acima do limite. Remova uma ou mais imagens e tente novamente.`);
    return;
  }

  const isNew = !id;
  try{
    await saveProjetoData(data);
  }catch(e){ return; }

  if(isNew){
    projetos.push(data);
    await saveIndex();
  }else{
    const idx = projetos.findIndex(p=>p.id===id);
    if(idx>-1) projetos[idx] = data;
  }
  closeModal();
  render();
  showMsg(isNew ? 'Ficha adicionada ao acervo.' : 'Ficha atualizada.');
}

async function deleteProjeto(id){
  if(!confirm('Excluir esta ficha do acervo?')) return;
  projetos = projetos.filter(p=>p.id!==id);
  await deleteProjetoData(id);
  await saveIndex();
  render();
  showMsg('Ficha excluída.');
}

// ---------- View mode ----------
function setMode(mode){
  if(isClienteLink) mode = 'cliente';
  viewMode = mode;
  document.getElementById('modeEdicao').classList.toggle('active', mode==='edicao');
  document.getElementById('modeCliente').classList.toggle('active', mode==='cliente');
  document.getElementById('clienteBanner').style.display = mode==='cliente' ? 'block' : 'none';
  document.getElementById('btnNew').style.display = mode==='edicao' ? '' : 'none';
  render();
}
document.getElementById('modeEdicao').addEventListener('click', ()=>setMode('edicao'));
document.getElementById('modeCliente').addEventListener('click', ()=>setMode('cliente'));

// ---------- Filters / search / sort ----------
document.getElementById('drawer').addEventListener('click', e=>{
  const btn = e.target.closest('.tab');
  if(!btn) return;
  document.querySelectorAll('.tab').forEach(t=>t.classList.remove('active'));
  btn.classList.add('active');
  currentFilter = btn.getAttribute('data-filter');
  render();
});
document.getElementById('searchInput').addEventListener('input', e=>{ currentSearch = e.target.value; render(); });
document.getElementById('sortSelect').addEventListener('change', e=>{ currentSort = e.target.value; render(); });
document.getElementById('btnNew').addEventListener('click', ()=>openModal(null));
document.getElementById('btnCancel').addEventListener('click', closeModal);
document.getElementById('btnSave').addEventListener('click', saveProjeto);
overlay.addEventListener('click', e=>{ if(e.target === overlay) closeModal(); });

if(new URLSearchParams(window.location.search).get('cliente') === '1'){
  isClienteLink = true;
  document.getElementById('modeToggle').style.display = 'none';
  setMode('cliente');
}

loadData();
</script>
</body>
</html>
