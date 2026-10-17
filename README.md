<!DOCTYPE html>
<html lang="id">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Kantin Kejujuran - SMP Negeri 17 Denpasar</title>
  <!-- Tailwind CSS via CDN -->
  <script src="https://cdn.tailwindcss.com"></script>
  <!-- Custom Styling Extensions -->
  <style>
    /* Smooth transitions and scroll behavior */
    html {
      scroll-behavior: smooth;
    }
    body {
      font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Helvetica, Arial, sans-serif;
    }
    /* Hide scrollbars for clean UI while keeping scrollability */
    .no-scrollbar::-webkit-scrollbar {
      display: none;
    }
    .no-scrollbar {
      -ms-overflow-style: none;
      scrollbar-width: none;
    }
  </style>
</head>
<body class="bg-blue-50 text-slate-800 min-h-screen flex flex-col items-center justify-between pb-20 selection:bg-blue-200">

  <!-- Outer Mobile Container -->
  <div class="w-full max-w-md bg-white min-h-screen shadow-xl flex flex-col relative overflow-hidden border-x border-blue-100">

    <!-- Header Section (Dominant Blue & White Theme) -->
    <header class="bg-gradient-to-r from-blue-700 to-blue-600 text-white p-5 rounded-b-2xl shadow-md relative z-10">
      <div class="flex items-center space-x-3">
        <!-- Logo Sekolah / Placeholder -->
        <div class="w-12 h-12 bg-white/10 rounded-full flex items-center justify-center p-1 border border-white/20 shrink-0">
          <img src="logo.png" 
               alt="Logo Sekolah" 
               class="w-full h-full object-contain" 
               onerror="this.onerror=null; this.src='https://via.placeholder.com/100/1E40AF/FFFFFF?text=SMPN17';">
        </div>
        <div>
          <h1 class="text-xl font-black tracking-wide leading-tight">KANTIN KEJUJURAN</h1>
          <p class="text-xs font-medium text-blue-100 tracking-wider">SMP NEGERI 17 DENPASAR</p>
        </div>
      </div>
    </header>

    <!-- Main Dynamic Content Area -->
    <main class="flex-1 p-4 overflow-y-auto no-scrollbar">

      <!-- ================= 1. TAB BERANDA (KATALOG) ================= -->
      <section id="tab-beranda" class="space-y-4">
        
        <!-- Search Bar -->
        <div class="relative">
          <input type="text" 
                 id="search-input" 
                 oninput="filterProduk()"
                 placeholder="Cari makanan atau minuman..." 
                 class="w-full pl-10 pr-4 py-2.5 bg-slate-50 border border-slate-200 rounded-xl text-sm focus:outline-none focus:ring-2 focus:ring-blue-500 focus:bg-white transition-all shadow-sm">
          <svg class="w-4 h-4 text-slate-400 absolute left-3.5 top-3.5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M21 21l-6-6m2-5a7 7 0 11-14 0 7 7 0 0114 0z"></path>
          </svg>
        </div>

        <!-- Banner Info Kejujuran -->
        <div class="bg-blue-50 border border-blue-200 rounded-xl p-3 flex items-start space-x-3 text-blue-900 text-xs">
          <span class="text-lg">💡</span>
          <div>
            <p class="font-bold">Ambil Sendiri, Bayar Jujur!</p>
            <p class="text-blue-700 mt-0.5">Pastikan uang dimasukkan sesuai harga tertera ke dalam kotak kasir kejujuran.</p>
          </div>
        </div>

        <!-- Grid Katalog Produk -->
        <div id="produk-container" class="grid grid-cols-2 gap-3.5 pt-1">
          <!-- Items injected dynamically by JS -->
        </div>

        <!-- Empty State (if no match) -->
        <div id="empty-state" class="hidden text-center py-12 space-y-2">
          <p class="text-3xl">🔍</p>
          <p class="text-sm font-semibold text-slate-600">Jajanan tidak ditemukan</p>
          <p class="text-xs text-slate-400">Coba cari dengan kata kunci lain.</p>
        </div>

      </section>

      <!-- ================= 2. TAB PENJUAL (GUIDE & EDITOR) ================= -->
      <section id="tab-penjual" class="hidden space-y-5">
        
        <!-- Header Info Penjual -->
        <div class="border-b border-slate-100 pb-3">
          <h2 class="text-base font-bold text-slate-800">Panduan & Generator Data Kantin</h2>
          <p class="text-xs text-slate-500 mt-1">Kelola daftar jajanan dan stok secara langsung untuk dipasang di GitHub.</p>
        </div>

        <!-- Form Generator Data Baru -->
        <div class="bg-white border border-blue-100 p-4 rounded-xl shadow-sm space-y-3">
          <h3 class="text-xs font-bold uppercase tracking-wider text-blue-700">1. Tambah / Update Item Sementara</h3>
          
          <form id="editor-form" onsubmit="tambahItemKeJSON(event)" class="space-y-3 text-xs">
            <div>
              <label class="block font-semibold text-slate-700 mb-1">Nama Barang</label>
              <input type="text" id="input-nama" required placeholder="Contoh: Nasi Jinggo" class="w-full border p-2 rounded-lg focus:ring-1 focus:ring-blue-500 outline-none">
            </div>
            
            <div class="grid grid-cols-2 gap-2">
              <div>
                <label class="block font-semibold text-slate-700 mb-1">Harga (Rp)</label>
                <input type="number" id="input-harga" required placeholder="5000" class="w-full border p-2 rounded-lg focus:ring-1 focus:ring-blue-500 outline-none">
              </div>
              <div>
                <label class="block font-semibold text-slate-700 mb-1">Jumlah Stok</label>
                <input type="number" id="input-stok" required placeholder="10" class="w-full border p-2 rounded-lg focus:ring-1 focus:ring-blue-500 outline-none">
              </div>
            </div>

            <div>
              <label class="block font-semibold text-slate-700 mb-1">URL Foto / Path Gambar</label>
              <input type="text" id="input-foto" required placeholder="images/nasi-jinggo.jpg" class="w-full border p-2 rounded-lg focus:ring-1 focus:ring-blue-500 outline-none">
            </div>

            <button type="submit" class="w-full bg-blue-600 hover:bg-blue-700 text-white font-bold py-2.5 rounded-lg shadow-sm transition">
              + Masukkan Ke Generator Code
            </button>
          </form>
        </div>

        <!-- Code Generator Result & Copy Guide -->
        <div class="bg-slate-900 text-slate-100 p-4 rounded-xl space-y-3 text-xs">
          <div class="flex justify-between items-center">
            <h3 class="font-bold text-blue-400">2. Hasil Kode JSON (`data.json`)</h3>
            <button onclick="salinKodeJSON()" class="bg-blue-600 hover:bg-blue-500 text-white text-[10px] font-bold px-2.5 py-1 rounded">
              📋 Salin JSON
            </button>
          </div>
          <p class="text-slate-400 text-[11px]">Salin semua kode di bawah ini dan tempelkan (*paste*) ke file <code class="text-yellow-300">data.json</code> di repository GitHub milikmu.</p>
          
          <pre id="json-preview" class="bg-slate-950 p-3 rounded-lg font-mono text-[11px] overflow-x-auto text-green-400 border border-slate-800 max-h-48 no-scrollbar"></pre>
        </div>

        <!-- Steps Guide GitHub -->
        <div class="bg-amber-50 border border-amber-200 rounded-xl p-3 text-xs space-y-1.5 text-amber-900">
          <p class="font-bold flex items-center gap-1">📌 Langkah Update di GitHub HP/PC:</p>
          <ol class="list-decimal pl-4 space-y-1 text-amber-800 text-[11px]">
            <li>Buka Repository GitHub Kantin milikmu.</li>
            <li>Buka file <b>data.json</b> lalu klik ikon pensil (<i>Edit</i>).</li>
            <li>Hapus semua isinya, lalu <b>Paste (Tempel)</b> kode JSON di atas.</li>
            <li>Klik tombol hijau <b>Commit Changes</b>. Data otomatis diperbarui di web!</li>
          </ol>
        </div>

      </section>

      <!-- ================= 3. TAB BAGIKAN (QR CODE & LINK) ================= -->
      <section id="tab-bagikan" class="hidden space-y-5 text-center py-4">
        
        <div class="space-y-1">
          <h2 class="text-base font-bold text-slate-800">Bagikan Akses Kantin Digital</h2>
          <p class="text-xs text-slate-500">Tempel QR Code ini di meja atau area fisik Kantin Kejujuran.</p>
        </div>

        <!-- Card QR Code -->
        <div class="bg-white p-6 rounded-2xl border border-blue-100 shadow-md inline-block space-y-4 max-w-[280px] mx-auto">
          <div class="bg-blue-50 p-3 rounded-xl border border-blue-100 inline-block">
            <!-- Dynamic QR Code API -->
            <img id="qr-code-img" 
                 src="" 
                 alt="QR Code Kantin" 
                 class="w-48 h-48 mx-auto rounded-lg shadow-sm">
          </div>
          <div>
            <p class="text-xs font-bold text-blue-900">Scan Pakai HP</p>
            <p class="text-[10px] text-slate-500">Langsung cek daftar jajanan & stok yang tersedia</p>
          </div>
        </div>

        <!-- Action Button Copy Link -->
        <div class="px-4">
          <button onclick="salinLinkAplikasi()" 
                  class="w-full bg-blue-600 hover:bg-blue-700 text-white font-bold py-3 px-4 rounded-xl shadow-md transition flex items-center justify-center space-x-2 text-sm">
            <span>🔗</span>
            <span>Salin Link Kantin Kejujuran</span>
          </button>
        </div>

      </section>

    </main>

    <!-- Bottom Navigation Bar (Fixed Bottom) -->
    <nav class="bg-white border-t border-slate-200 flex justify-around items-center p-2 shadow-lg relative z-20">
      <button onclick="switchTab('beranda')" id="nav-beranda" class="flex-1 py-1.5 flex flex-col items-center text-blue-600 font-bold transition">
        <svg class="w-5 h-5 mb-0.5" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 12l2-2m0 0l7-7 7 7M5 10v10a1 1 0 001 1h3m10-11l2 2m-2-2v10a1 1 0 01-1 1h-3m-6 0a1 1 0 001-1v-4a1 1 0 011-1h2a1 1 0 011 1v4a1 1 0 001 1m-6 0h6"></path></svg>
        <span class="text-[10px]">Beranda</span>
      </button>

      <button onclick="switchTab('penjual')" id="nav-penjual" class="flex-1 py-1.5 flex flex-col items-center text-slate-400 font-medium hover:text-blue-600 transition">
        <svg class="w-5 h-5 mb-0.5" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M11 5H6a2 2 0 00-2 2v11a2 2 0 002 2h11a2 2 0 002-2v-5m-1.414-9.414a2 2 0 112.828 2.828L11.828 15H9v-2.828l8.586-8.586z"></path></svg>
        <span class="text-[10px]">Penjual</span>
      </button>

      <button onclick="switchTab('bagikan')" id="nav-bagikan" class="flex-1 py-1.5 flex flex-col items-center text-slate-400 font-medium hover:text-blue-600 transition">
        <svg class="w-5 h-5 mb-0.5" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M8.684 13.342C8.886 12.938 9 12.482 9 12c0-.482-.114-.938-.316-1.342m0 2.684a3 3 0 110-2.684m0 2.684l6.632 3.316m-6.632-6l6.632-3.316m0 0a3 3 0 105.367-2.684 3 3 0 00-5.367 2.684zm0 9.316a3 3 0 105.368 2.684 3 3 0 00-5.368-2.684z"></path></svg>
        <span class="text-[10px]">Bagikan</span>
      </button>
    </nav>

    <!-- Toast Notification Message Box -->
    <div id="toast" class="fixed bottom-16 left-1/2 transform -translate-x-1/2 bg-slate-900/90 text-white text-xs px-4 py-2 rounded-full shadow-lg transition-all duration-300 opacity-0 pointer-events-none z-50">
      Notifikasi
    </div>

  </div>

  <!-- JavaScript Logic -->
  <script>
    // Mock Data Default (digunakan sebagai fallback jika data.json belum dibuat di GitHub)
    const fallbackData = [
      {
        "nama": "Nasi Jinggo Ayam",
        "harga": 5000,
        "stok": 12,
        "foto": "https://images.unsplash.com/photo-1546069901-ba9599a7e63c?w=400&q=80"
      },
      {
        "nama": "Es Teh Manis",
        "harga": 2000,
        "stok": 8,
        "foto": "https://images.unsplash.com/photo-1556679343-c7306c1976bc?w=400&q=80"
      },
      {
        "nama": "Roti Cokelat",
        "harga": 3000,
        "stok": 0,
        "foto": "https://images.unsplash.com/photo-1509440159596-0249088772ff?w=400&q=80"
      },
      {
        "nama": "Kripik Singkong",
        "harga": 2000,
        "stok": 5,
        "foto": "https://images.unsplash.com/photo-1566478989037-eec170784d0b?w=400&q=80"
      }
    ];

    let currentProduk = [];

    // Initialize Application
    window.onload = function() {
      fetchDataJSON();
      generateQRCode();
    };

    // 1. Fetch Data dari data.json
    async function fetchDataJSON() {
      try {
        const response = await fetch('data.json');
        if (!response.ok) throw new Error('File data.json belum ditemukan');
        currentProduk = await response.json();
      } catch (err) {
        console.warn('Menggunakan data fallback/demo karena data.json belum siap:', err.message);
        currentProduk = [...fallbackData];
      } finally {
        renderProduk(currentProduk);
        updateJSONPreview();
      }
    }

    // 2. Render List Produk ke Beranda
    function renderProduk(data) {
      const container = document.getElementById('produk-container');
      const emptyState = document.getElementById('empty-state');
      container.innerHTML = '';

      if (data.length === 0) {
        emptyState.classList.remove('hidden');
        return;
      } else {
        emptyState.classList.add('hidden');
      }

      data.forEach(item => {
        const isAvailable = item.stok > 0;
        
        const cardHTML = `
          <div class="bg-white rounded-xl border border-blue-100 shadow-sm overflow-hidden flex flex-col justify-between transition hover:shadow-md">
            <div>
              <!-- Foto Produk -->
              <div class="relative w-full h-28 bg-slate-100">
                <img src="${item.foto}" 
                     alt="${item.nama}" 
                     class="w-full h-full object-cover"
                     onerror="this.onerror=null; this.src='https://placehold.co/300x200/1E40AF/FFFFFF?text=Foto+Jajanan';">
                
                <!-- Badge Stok Top-Right -->
                <span class="absolute top-2 right-2 px-2 py-0.5 rounded-md text-[10px] font-bold shadow-sm ${
                  isAvailable ? 'bg-blue-600 text-white' : 'bg-red-500 text-white'
                }">
                  ${isAvailable ? `Stok: ${item.stok}` : 'Habis'}
                </span>
              </div>

              <!-- Detail Barang -->
              <div class="p-3">
                <h3 class="font-bold text-slate-800 text-xs line-clamp-2 leading-snug">${item.nama}</h3>
                <p class="text-blue-600 font-extrabold text-sm mt-1">
                  Rp ${Number(item.harga).toLocaleString('id-ID')}
                </p>
              </div>
            </div>

            <!-- Footer Badge Indikator Kejujuran -->
            <div class="px-3 pb-3">
              <div class="w-full text-center py-1 rounded bg-slate-50 text-[10px] font-semibold text-slate-500 border border-slate-100">
                Display Sah
              </div>
            </div>
          </div>
        `;
        container.insertAdjacentHTML('beforeend', cardHTML);
      });
    }

    // 3. Filter / Search Produk
    function filterProduk() {
      const query = document.getElementById('search-input').value.toLowerCase();
      const filtered = currentProduk.filter(item => 
        item.nama.toLowerCase().includes(query)
      );
      renderProduk(filtered);
    }

    // 4. Switch Tab Navigation
    function switchTab(tabName) {
      // Hide all tabs
      document.getElementById('tab-beranda').classList.add('hidden');
      document.getElementById('tab-penjual').classList.add('hidden');
      document.getElementById('tab-bagikan').classList.add('hidden');

      // Reset nav button styling
      const tabs = ['beranda', 'penjual', 'bagikan'];
      tabs.forEach(t => {
        const btn = document.getElementById(`nav-${t}`);
        btn.className = "flex-1 py-1.5 flex flex-col items-center text-slate-400 font-medium hover:text-blue-600 transition";
      });

      // Active tab styling
      document.getElementById(`tab-${tabName}`).classList.remove('hidden');
      const activeBtn = document.getElementById(`nav-${tabName}`);
      activeBtn.className = "flex-1 py-1.5 flex flex-col items-center text-blue-600 font-bold transition";
    }

    // 5. Tambah Item Baru & Update JSON Preview
    function tambahItemKeJSON(e) {
      e.preventDefault();
      
      const nama = document.getElementById('input-nama').value;
      const harga = Number(document.getElementById('input-harga').value);
      const stok = Number(document.getElementById('input-stok').value);
      const foto = document.getElementById('input-foto').value;

      const newItem = { nama, harga, stok, foto };
      
      // Tambahkan di paling atas list
      currentProduk.unshift(newItem);
      
      // Update UI dan JSON Preview
      renderProduk(currentProduk);
      updateJSONPreview();
      
      // Reset Form Input
      document.getElementById('editor-form').reset();
      showToast('Berhasil ditambahkan ke kode JSON!');
    }

    function updateJSONPreview() {
      const jsonStr = JSON.stringify(currentProduk, null, 2);
      document.getElementById('json-preview').textContent = jsonStr;
    }

    // 6. Salin Kode JSON ke Clipboard
    function salinKodeJSON() {
      const code = document.getElementById('json-preview').textContent;
      copyToClipboard(code);
      showToast('Kode JSON berhasil disalin!');
    }

    // 7. Generate QR Code untuk Link Aplikasi
    function generateQRCode() {
      const appUrl = window.location.href;
      const qrApiUrl = `https://api.qrserver.com/v1/create-qr-code/?size=200x200&data=${encodeURIComponent(appUrl)}`;
      document.getElementById('qr-code-img').src = qrApiUrl;
    }

    // 8. Salin Link Aplikasi
    function salinLinkAplikasi() {
      copyToClipboard(window.location.href);
      showToast('Link Kantin berhasil disalin!');
    }

    // Helper Copy to Clipboard with fallback
    function copyToClipboard(text) {
      if (navigator.clipboard && window.isSecureContext) {
        navigator.clipboard.writeText(text);
      } else {
        // Legacy copy approach for iframe restrictions
        const textArea = document.createElement("textarea");
        textArea.value = text;
        document.body.appendChild(textArea);
        textArea.select();
        document.execCommand('copy');
        document.body.removeChild(textArea);
      }
    }

    // Helper Toast Message
    function showToast(message) {
      const toast = document.getElementById('toast');
      toast.textContent = message;
      toast.classList.remove('opacity-0', 'pointer-events-none');
      
      setTimeout(() => {
        toast.classList.add('opacity-0', 'pointer-events-none');
      }, 2500);
    }
  </script>
</body>
</html>
