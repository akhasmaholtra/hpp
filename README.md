[index.html](https://github.com/user-attachments/files/24837360/index.html)
<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Kalkulator HPP Pastry</title>
    <script src="https://cdn.jsdelivr.net/npm/@tailwindcss/browser@4"></script>
    <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;500;600;700&display=swap" rel="stylesheet">
    <style>
        * { font-family: 'Poppins', sans-serif; }
    </style>
</head>
<body class="bg-gradient-to-br from-amber-50 to-orange-100 min-h-screen py-8 px-4">
    <div class="max-w-5xl mx-auto">
        <!-- Header -->
        <div class="text-center mb-8">
            <h1 class="text-4xl font-bold text-amber-800 mb-2">🥐 Kalkulator HPP Pastry</h1>
            <p class="text-amber-600">Hitung Harga Pokok Produksi dengan Mudah</p>
        </div>

        <!-- Step 1: Daftar Bahan Baku -->
        <div class="bg-white rounded-2xl shadow-xl p-6 mb-6">
            <div class="flex items-center gap-3 mb-4">
                <span class="bg-amber-500 text-white w-8 h-8 rounded-full flex items-center justify-center font-bold">1</span>
                <h2 class="text-xl font-semibold text-gray-800">Daftar Bahan Baku</h2>
            </div>
            <p class="text-gray-500 text-sm mb-4">Masukkan bahan baku, gramasi kemasan, dan harga belinya</p>

            <div id="bahanBakuContainer">
                <!-- Bahan baku rows akan ditambahkan di sini -->
            </div>

            <button onclick="tambahBahanBaku()" class="mt-4 bg-amber-500 hover:bg-amber-600 text-white px-4 py-2 rounded-lg flex items-center gap-2 transition-all">
                <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" viewBox="0 0 20 20" fill="currentColor">
                    <path fill-rule="evenodd" d="M10 3a1 1 0 011 1v5h5a1 1 0 110 2h-5v5a1 1 0 11-2 0v-5H4a1 1 0 110-2h5V4a1 1 0 011-1z" clip-rule="evenodd" />
                </svg>
                Tambah Bahan Baku
            </button>
        </div>

        <!-- Step 2: Resep Produk -->
        <div class="bg-white rounded-2xl shadow-xl p-6 mb-6">
            <div class="flex items-center gap-3 mb-4">
                <span class="bg-orange-500 text-white w-8 h-8 rounded-full flex items-center justify-center font-bold">2</span>
                <h2 class="text-xl font-semibold text-gray-800">Resep Produk</h2>
            </div>
            <p class="text-gray-500 text-sm mb-4">Pilih bahan dan masukkan gramasi yang dibutuhkan untuk resep</p>

            <div id="resepContainer">
                <!-- Resep rows akan ditambahkan di sini -->
            </div>

            <button onclick="tambahResep()" class="mt-4 bg-orange-500 hover:bg-orange-600 text-white px-4 py-2 rounded-lg flex items-center gap-2 transition-all">
                <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" viewBox="0 0 20 20" fill="currentColor">
                    <path fill-rule="evenodd" d="M10 3a1 1 0 011 1v5h5a1 1 0 110 2h-5v5a1 1 0 11-2 0v-5H4a1 1 0 110-2h5V4a1 1 0 011-1z" clip-rule="evenodd" />
                </svg>
                Tambah Bahan Resep
            </button>

            <!-- Total Biaya Bahan -->
            <div class="mt-6 p-4 bg-gradient-to-r from-orange-100 to-amber-100 rounded-xl">
                <div class="flex justify-between items-center">
                    <span class="text-lg font-semibold text-gray-700">Total Biaya Bahan:</span>
                    <span id="totalBiaya" class="text-2xl font-bold text-orange-600">Rp 0</span>
                </div>
            </div>
        </div>

        <!-- Step 3: Pembagi (HPP per Porsi) -->
        <div class="bg-white rounded-2xl shadow-xl p-6 mb-6">
            <div class="flex items-center gap-3 mb-4">
                <span class="bg-rose-500 text-white w-8 h-8 rounded-full flex items-center justify-center font-bold">3</span>
                <h2 class="text-xl font-semibold text-gray-800">HPP per Porsi/Piece</h2>
            </div>
            <p class="text-gray-500 text-sm mb-4">Bagi total biaya dengan jumlah porsi/piece yang dihasilkan</p>

            <div class="flex flex-col md:flex-row gap-4 items-center">
                <div class="flex-1 w-full">
                    <label class="block text-sm font-medium text-gray-600 mb-1">Jumlah Porsi/Piece</label>
                    <input type="number" id="jumlahPorsi" placeholder="Contoh: 10" min="1" value="1"
                        class="w-full px-4 py-3 border-2 border-gray-200 rounded-lg focus:border-rose-400 focus:outline-none transition-all text-lg"
                        oninput="hitungHPP()">
                </div>
                <div class="text-3xl text-gray-400 hidden md:block">=</div>
                <div class="flex-1 w-full p-4 bg-gradient-to-r from-rose-100 to-pink-100 rounded-xl">
                    <p class="text-sm text-gray-600 mb-1">HPP per Porsi/Piece:</p>
                    <p id="hppPerPorsi" class="text-2xl font-bold text-rose-600">Rp 0</p>
                </div>
            </div>
        </div>

        <!-- Ringkasan -->
        <div class="bg-gradient-to-r from-amber-500 to-orange-500 rounded-2xl shadow-xl p-6 text-white">
            <h2 class="text-xl font-semibold mb-4">📋 Ringkasan HPP</h2>
            <div class="grid md:grid-cols-3 gap-4">
                <div class="bg-white/20 rounded-xl p-4 backdrop-blur">
                    <p class="text-amber-100 text-sm">Total Jenis Bahan</p>
                    <p id="totalJenisBahan" class="text-2xl font-bold">0</p>
                </div>
                <div class="bg-white/20 rounded-xl p-4 backdrop-blur">
                    <p class="text-amber-100 text-sm">Total Biaya Bahan</p>
                    <p id="ringkasanTotalBiaya" class="text-2xl font-bold">Rp 0</p>
                </div>
                <div class="bg-white/20 rounded-xl p-4 backdrop-blur">
                    <p class="text-amber-100 text-sm">HPP per Porsi</p>
                    <p id="ringkasanHPP" class="text-2xl font-bold">Rp 0</p>
                </div>
            </div>
        </div>

        <!-- Footer -->
        <p class="text-center text-gray-500 text-sm mt-8">© 2024 Kalkulator HPP Pastry</p>
    </div>

    <script>
        let bahanBakuList = [];
        let resepList = [];
        let bahanBakuCounter = 0;
        let resepCounter = 0;

        // Format Rupiah
        function formatRupiah(angka) {
            return new Intl.NumberFormat('id-ID', {
                style: 'currency',
                currency: 'IDR',
                minimumFractionDigits: 0,
                maximumFractionDigits: 2
            }).format(angka);
        }

        // Tambah Bahan Baku
        function tambahBahanBaku() {
            bahanBakuCounter++;
            const id = bahanBakuCounter;
            
            const container = document.getElementById('bahanBakuContainer');
            const row = document.createElement('div');
            row.id = `bahanBaku-${id}`;
            row.className = 'grid grid-cols-1 md:grid-cols-12 gap-3 mb-3 p-4 bg-amber-50 rounded-xl items-end';
            row.innerHTML = `
                <div class="md:col-span-3">
                    <label class="block text-xs font-medium text-gray-600 mb-1">Nama Bahan</label>
                    <input type="text" id="namaBahan-${id}" placeholder="Contoh: Terigu"
                        class="w-full px-3 py-2 border-2 border-amber-200 rounded-lg focus:border-amber-400 focus:outline-none"
                        oninput="updateBahanBaku(${id})">
                </div>
                <div class="md:col-span-2">
                    <label class="block text-xs font-medium text-gray-600 mb-1">Gramasi Kemasan (gr)</label>
                    <input type="number" id="gramasiBahan-${id}" placeholder="1000"
                        class="w-full px-3 py-2 border-2 border-amber-200 rounded-lg focus:border-amber-400 focus:outline-none"
                        oninput="updateBahanBaku(${id})">
                </div>
                <div class="md:col-span-3">
                    <label class="block text-xs font-medium text-gray-600 mb-1">Harga Beli (Rp)</label>
                    <input type="number" id="hargaBahan-${id}" placeholder="15000"
                        class="w-full px-3 py-2 border-2 border-amber-200 rounded-lg focus:border-amber-400 focus:outline-none"
                        oninput="updateBahanBaku(${id})">
                </div>
                <div class="md:col-span-3">
                    <label class="block text-xs font-medium text-gray-600 mb-1">Harga per Gram</label>
                    <div id="hargaPerGram-${id}" class="w-full px-3 py-2 bg-green-100 text-green-700 font-semibold rounded-lg text-center">
                        Rp 0/gr
                    </div>
                </div>
                <div class="md:col-span-1 flex justify-center">
                    <button onclick="hapusBahanBaku(${id})" class="p-2 bg-red-100 hover:bg-red-200 text-red-500 rounded-lg transition-all">
                        <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" viewBox="0 0 20 20" fill="currentColor">
                            <path fill-rule="evenodd" d="M9 2a1 1 0 00-.894.553L7.382 4H4a1 1 0 000 2v10a2 2 0 002 2h8a2 2 0 002-2V6a1 1 0 100-2h-3.382l-.724-1.447A1 1 0 0011 2H9zM7 8a1 1 0 012 0v6a1 1 0 11-2 0V8zm5-1a1 1 0 00-1 1v6a1 1 0 102 0V8a1 1 0 00-1-1z" clip-rule="evenodd" />
                        </svg>
                    </button>
                </div>
            `;
            container.appendChild(row);
            
            bahanBakuList.push({ id, nama: '', gramasi: 0, harga: 0, hargaPerGram: 0 });
            updateDropdownResep();
        }

        // Update Bahan Baku
        function updateBahanBaku(id) {
            const nama = document.getElementById(`namaBahan-${id}`).value;
            const gramasi = parseFloat(document.getElementById(`gramasiBahan-${id}`).value) || 0;
            const harga = parseFloat(document.getElementById(`hargaBahan-${id}`).value) || 0;
            const hargaPerGram = gramasi > 0 ? harga / gramasi : 0;

            // Update display
            document.getElementById(`hargaPerGram-${id}`).textContent = `Rp ${hargaPerGram.toFixed(2)}/gr`;

            // Update list
            const bahan = bahanBakuList.find(b => b.id === id);
            if (bahan) {
                bahan.nama = nama;
                bahan.gramasi = gramasi;
                bahan.harga = harga;
                bahan.hargaPerGram = hargaPerGram;
            }

            updateDropdownResep();
            hitungTotalBiaya();
        }

        // Hapus Bahan Baku
        function hapusBahanBaku(id) {
            document.getElementById(`bahanBaku-${id}`).remove();
            bahanBakuList = bahanBakuList.filter(b => b.id !== id);
            updateDropdownResep();
            hitungTotalBiaya();
        }

        // Update Dropdown Resep
        function updateDropdownResep() {
            const selects = document.querySelectorAll('[id^="selectBahan-"]');
            selects.forEach(select => {
                const currentValue = select.value;
                select.innerHTML = '<option value="">-- Pilih Bahan --</option>';
                bahanBakuList.forEach(bahan => {
                    if (bahan.nama) {
                        const option = document.createElement('option');
                        option.value = bahan.id;
                        option.textContent = `${bahan.nama} (Rp ${bahan.hargaPerGram.toFixed(2)}/gr)`;
                        select.appendChild(option);
                    }
                });
                select.value = currentValue;
            });
        }

        // Tambah Resep
        function tambahResep() {
            resepCounter++;
            const id = resepCounter;

            const container = document.getElementById('resepContainer');
            const row = document.createElement('div');
            row.id = `resep-${id}`;
            row.className = 'grid grid-cols-1 md:grid-cols-12 gap-3 mb-3 p-4 bg-orange-50 rounded-xl items-end';
            row.innerHTML = `
                <div class="md:col-span-4">
                    <label class="block text-xs font-medium text-gray-600 mb-1">Pilih Bahan</label>
                    <select id="selectBahan-${id}" 
                        class="w-full px-3 py-2 border-2 border-orange-200 rounded-lg focus:border-orange-400 focus:outline-none"
                        onchange="hitungBiayaResep(${id})">
                        <option value="">-- Pilih Bahan --</option>
                    </select>
                </div>
                <div class="md:col-span-2">
                    <label class="block text-xs font-medium text-gray-600 mb-1">Gramasi Resep (gr)</label>
                    <input type="number" id="gramasiResep-${id}" placeholder="300"
                        class="w-full px-3 py-2 border-2 border-orange-200 rounded-lg focus:border-orange-400 focus:outline-none"
                        oninput="hitungBiayaResep(${id})">
                </div>
                <div class="md:col-span-2">
                    <label class="block text-xs font-medium text-gray-600 mb-1">Rp/gr</label>
                    <div id="rpPerGramResep-${id}" class="w-full px-3 py-2 bg-gray-100 text-gray-600 rounded-lg text-center text-sm">
                        Rp 0
                    </div>
                </div>
                <div class="md:col-span-3">
                    <label class="block text-xs font-medium text-gray-600 mb-1">Biaya</label>
                    <div id="biayaResep-${id}" class="w-full px-3 py-2 bg-green-100 text-green-700 font-semibold rounded-lg text-center">
                        Rp 0
                    </div>
                </div>
                <div class="md:col-span-1 flex justify-center">
                    <button onclick="hapusResep(${id})" class="p-2 bg-red-100 hover:bg-red-200 text-red-500 rounded-lg transition-all">
                        <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" viewBox="0 0 20 20" fill="currentColor">
                            <path fill-rule="evenodd" d="M9 2a1 1 0 00-.894.553L7.382 4H4a1 1 0 000 2v10a2 2 0 002 2h8a2 2 0 002-2V6a1 1 0 100-2h-3.382l-.724-1.447A1 1 0 0011 2H9zM7 8a1 1 0 012 0v6a1 1 0 11-2 0V8zm5-1a1 1 0 00-1 1v6a1 1 0 102 0V8a1 1 0 00-1-1z" clip-rule="evenodd" />
                        </svg>
                    </button>
                </div>
            `;
            container.appendChild(row);
            
            resepList.push({ id, bahanId: null, gramasi: 0, biaya: 0 });
            updateDropdownResep();
        }

        // Hitung Biaya Resep
        function hitungBiayaResep(id) {
            const bahanId = parseInt(document.getElementById(`selectBahan-${id}`).value);
            const gramasi = parseFloat(document.getElementById(`gramasiResep-${id}`).value) || 0;
            
            const bahan = bahanBakuList.find(b => b.id === bahanId);
            const hargaPerGram = bahan ? bahan.hargaPerGram : 0;
            const biaya = gramasi * hargaPerGram;

            // Update display
            document.getElementById(`rpPerGramResep-${id}`).textContent = `Rp ${hargaPerGram.toFixed(2)}`;
            document.getElementById(`biayaResep-${id}`).textContent = formatRupiah(biaya);

            // Update list
            const resep = resepList.find(r => r.id === id);
            if (resep) {
                resep.bahanId = bahanId;
                resep.gramasi = gramasi;
                resep.biaya = biaya;
            }

            hitungTotalBiaya();
        }

        // Hapus Resep
        function hapusResep(id) {
            document.getElementById(`resep-${id}`).remove();
            resepList = resepList.filter(r => r.id !== id);
            hitungTotalBiaya();
        }

        // Hitung Total Biaya
        function hitungTotalBiaya() {
            const total = resepList.reduce((sum, r) => sum + r.biaya, 0);
            document.getElementById('totalBiaya').textContent = formatRupiah(total);
            document.getElementById('ringkasanTotalBiaya').textContent = formatRupiah(total);
            
            // Update jumlah jenis bahan di resep
            const jenisBahan = resepList.filter(r => r.bahanId).length;
            document.getElementById('totalJenisBahan').textContent = jenisBahan;

            hitungHPP();
        }

        // Hitung HPP per Porsi
        function hitungHPP() {
            const total = resepList.reduce((sum, r) => sum + r.biaya, 0);
            const jumlahPorsi = parseFloat(document.getElementById('jumlahPorsi').value) || 1;
            const hpp = total / jumlahPorsi;

            document.getElementById('hppPerPorsi').textContent = formatRupiah(hpp);
            document.getElementById('ringkasanHPP').textContent = formatRupiah(hpp);
        }

        // Initialize dengan beberapa bahan default
        window.onload = function() {
            tambahBahanBaku();
            tambahResep();
        }
    </script>
</body>
</html>
