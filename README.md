<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Perpustakaan Digital</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&display=swap');
        body { font-family: 'Inter', sans-serif; }
        
        .notification-slide {
            animation: slideIn 0.5s ease-out;
        }
        
        @keyframes slideIn {
            from { transform: translateX(100%); opacity: 0; }
            to { transform: translateX(0); opacity: 1; }
        }
        
        .fade-out {
            animation: fadeOut 0.5s ease-out forwards;
        }
        
        @keyframes fadeOut {
            from { opacity: 1; }
            to { opacity: 0; }
        }
    </style>
</head>
<body class="bg-gradient-to-br from-blue-50 to-white min-h-screen">
    <!-- Navigation -->
    <nav class="bg-white shadow-lg border-b-4 border-blue-500">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
            <div class="flex justify-between h-16">
                <div class="flex items-center">
                    <div class="flex-shrink-0">
                        <h1 class="text-2xl font-bold text-blue-600">📚 Perpustakaan Jala Taruna AAL</h1>
                    </div>
                </div>
                <div class="flex items-center space-x-4">
                    <button onclick="showPage('home')" class="nav-btn bg-blue-500 hover:bg-blue-600 text-white px-4 py-2 rounded-lg transition-colors">
                        🏠 Beranda
                    </button>
                    <button onclick="showPage('borrowers')" class="nav-btn bg-white hover:bg-blue-50 text-blue-600 border-2 border-blue-500 px-4 py-2 rounded-lg transition-colors">
                        📋 Data Peminjam
                    </button>
                </div>
            </div>
        </div>
    </nav>

    <!-- Notification Container -->
    <div id="notificationContainer" class="fixed top-20 right-4 z-50 space-y-2"></div>

    <!-- Homepage -->
    <div id="homePage" class="page">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-12">
            <!-- Hero Section -->
            <div class="text-center mb-16">
                <h2 class="text-5xl font-bold text-blue-800 mb-6">Selamat Datang di Perpustakaan Jala Taruna AAL</h2>
                <p class="text-xl text-blue-600 mb-8 max-w-3xl mx-auto">
                    Kelola peminjaman buku dengan mudah dan efisien. Sistem otomatis akan memberikan notifikasi untuk peminjaman yang melewati batas waktu.
                </p>
                <div class="flex justify-center space-x-4">
                    <button onclick="showPage('borrowers')" class="bg-blue-600 hover:bg-blue-700 text-white px-8 py-4 rounded-xl text-lg font-semibold transition-colors shadow-lg">
                        📊 Lihat Data Peminjam
                    </button>
                    <button onclick="addNewBorrower()" class="bg-white hover:bg-blue-50 text-blue-600 border-2 border-blue-500 px-8 py-4 rounded-xl text-lg font-semibold transition-colors shadow-lg">
                        ➕ Tambah Peminjam Baru
                    </button>
                </div>
            </div>

            <!-- Stats Cards -->
            <div class="grid md:grid-cols-3 gap-8 mb-16">
                <div class="bg-white rounded-2xl p-8 shadow-xl border-l-4 border-blue-500">
                    <div class="flex items-center">
                        <div class="p-3 bg-blue-100 rounded-full">
                            <span class="text-2xl">📚</span>
                        </div>
                        <div class="ml-4">
                            <h3 class="text-lg font-semibold text-gray-700">Total Peminjam</h3>
                            <p id="totalBorrowers" class="text-3xl font-bold text-blue-600">0</p>
                        </div>
                    </div>
                </div>
                
                <div class="bg-white rounded-2xl p-8 shadow-xl border-l-4 border-green-500">
                    <div class="flex items-center">
                        <div class="p-3 bg-green-100 rounded-full">
                            <span class="text-2xl">✅</span>
                        </div>
                        <div class="ml-4">
                            <h3 class="text-lg font-semibold text-gray-700">Tepat Waktu</h3>
                            <p id="onTimeBorrowers" class="text-3xl font-bold text-green-600">0</p>
                        </div>
                    </div>
                </div>
                
                <div class="bg-white rounded-2xl p-8 shadow-xl border-l-4 border-red-500">
                    <div class="flex items-center">
                        <div class="p-3 bg-red-100 rounded-full">
                            <span class="text-2xl">⚠️</span>
                        </div>
                        <div class="ml-4">
                            <h3 class="text-lg font-semibold text-gray-700">Terlambat</h3>
                            <p id="overdueBorrowers" class="text-3xl font-bold text-red-600">0</p>
                        </div>
                    </div>
                </div>
            </div>

            <!-- Features -->
            <div class="bg-white rounded-2xl p-12 shadow-xl">
                <h3 class="text-3xl font-bold text-blue-800 text-center mb-12">Fitur Unggulan</h3>
                <div class="grid md:grid-cols-2 lg:grid-cols-4 gap-8">
                    <div class="text-center">
                        <div class="bg-blue-100 w-16 h-16 rounded-full flex items-center justify-center mx-auto mb-4">
                            <span class="text-2xl">🔔</span>
                        </div>
                        <h4 class="font-semibold text-gray-800 mb-2">Notifikasi Otomatis</h4>
                        <p class="text-gray-600 text-sm">Peringatan otomatis untuk peminjaman yang terlambat</p>
                    </div>
                    
                    <div class="text-center">
                        <div class="bg-blue-100 w-16 h-16 rounded-full flex items-center justify-center mx-auto mb-4">
                            <span class="text-2xl">📱</span>
                        </div>
                        <h4 class="font-semibold text-gray-800 mb-2">Responsif</h4>
                        <p class="text-gray-600 text-sm">Dapat diakses dari berbagai perangkat</p>
                    </div>
                    
                    <div class="text-center">
                        <div class="bg-blue-100 w-16 h-16 rounded-full flex items-center justify-center mx-auto mb-4">
                            <span class="text-2xl">⚡</span>
                        </div>
                        <h4 class="font-semibold text-gray-800 mb-2">Cepat & Mudah</h4>
                        <p class="text-gray-600 text-sm">Interface yang intuitif dan mudah digunakan</p>
                    </div>
                    
                    <div class="text-center">
                        <div class="bg-blue-100 w-16 h-16 rounded-full flex items-center justify-center mx-auto mb-4">
                            <span class="text-2xl">🔒</span>
                        </div>
                        <h4 class="font-semibold text-gray-800 mb-2">Aman</h4>
                        <p class="text-gray-600 text-sm">Data tersimpan dengan aman di browser</p>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <!-- Borrowers Page -->
    <div id="borrowersPage" class="page hidden">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-8">
            <div class="flex justify-between items-center mb-8">
                <h2 class="text-3xl font-bold text-blue-800">📋 Data Peminjam Buku</h2>
                <button onclick="addNewBorrower()" class="bg-blue-600 hover:bg-blue-700 text-white px-6 py-3 rounded-lg font-semibold transition-colors shadow-lg">
                    ➕ Tambah Peminjam Baru
                </button>
            </div>

            <!-- Search and Filter -->
            <div class="bg-white rounded-xl p-6 shadow-lg mb-8">
                <div class="flex flex-col md:flex-row gap-4">
                    <div class="flex-1">
                        <input type="text" id="searchInput" placeholder="🔍 Cari nama peminjam..." 
                               class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-transparent"
                               oninput="filterBorrowers()">
                    </div>
                    <select id="statusFilter" onchange="filterBorrowers()" 
                            class="px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-transparent">
                        <option value="all">Semua Status</option>
                        <option value="ontime">Tepat Waktu</option>
                        <option value="overdue">Terlambat</option>
                    </select>
                    <button onclick="checkOverdueBooks()" class="bg-red-500 hover:bg-red-600 text-white px-6 py-3 rounded-lg font-semibold transition-colors">
                        🔔 Cek Keterlambatan
                    </button>
                </div>
            </div>

            <!-- Borrowers Table -->
            <div class="bg-white rounded-xl shadow-lg overflow-hidden">
                <div class="overflow-x-auto">
                    <table class="w-full">
                        <thead class="bg-blue-600 text-white">
                            <tr>
                                <th class="px-6 py-4 text-left font-semibold">Nama Peminjam</th>
                                <th class="px-6 py-4 text-left font-semibold">Nomor Telepon</th>
                                <th class="px-6 py-4 text-left font-semibold">Judul Buku</th>
                                <th class="px-6 py-4 text-left font-semibold">Tanggal Pinjam</th>
                                <th class="px-6 py-4 text-left font-semibold">Batas Kembali</th>
                                <th class="px-6 py-4 text-left font-semibold">Status</th>
                                <th class="px-6 py-4 text-left font-semibold">Aksi</th>
                            </tr>
                        </thead>
                        <tbody id="borrowersTableBody" class="divide-y divide-gray-200">
                            <!-- Data will be populated by JavaScript -->
                        </tbody>
                    </table>
                </div>
                
                <div id="emptyState" class="text-center py-16 hidden">
                    <div class="text-6xl mb-4">📚</div>
                    <h3 class="text-xl font-semibold text-gray-600 mb-2">Belum ada data peminjam</h3>
                    <p class="text-gray-500 mb-6">Tambahkan peminjam baru untuk mulai mengelola perpustakaan</p>
                    <button onclick="addNewBorrower()" class="bg-blue-600 hover:bg-blue-700 text-white px-6 py-3 rounded-lg font-semibold transition-colors">
                        ➕ Tambah Peminjam Pertama
                    </button>
                </div>
            </div>
        </div>
    </div>

    <!-- Add/Edit Borrower Modal -->
    <div id="borrowerModal" class="fixed inset-0 bg-black bg-opacity-50 hidden items-center justify-center z-40">
        <div class="bg-white rounded-2xl p-8 max-w-md w-full mx-4 shadow-2xl">
            <h3 id="modalTitle" class="text-2xl font-bold text-blue-800 mb-6">Tambah Peminjam Baru</h3>
            
            <form id="borrowerForm" onsubmit="saveBorrower(event)">
                <div class="space-y-4">
                    <div>
                        <label class="block text-sm font-semibold text-gray-700 mb-2">Nama Peminjam</label>
                        <input type="text" id="borrowerName" required 
                               class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-transparent"
                               placeholder="Masukkan nama lengkap">
                    </div>
                    
                    <div>
                        <label class="block text-sm font-semibold text-gray-700 mb-2">Nomor Telepon</label>
                        <input type="tel" id="borrowerPhone" required 
                               class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-transparent"
                               placeholder="Contoh: 08123456789">
                    </div>
                    
                    <div>
                        <label class="block text-sm font-semibold text-gray-700 mb-2">Judul Buku</label>
                        <input type="text" id="bookTitle" required 
                               class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-transparent"
                               placeholder="Masukkan judul buku">
                    </div>
                    
                    <div>
                        <label class="block text-sm font-semibold text-gray-700 mb-2">Tanggal Kembali</label>
                        <input type="date" id="returnDate" required 
                               class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-transparent">
                    </div>
                </div>
                
                <div class="flex space-x-4 mt-8">
                    <button type="button" onclick="closeModal()" 
                            class="flex-1 bg-gray-300 hover:bg-gray-400 text-gray-700 py-3 rounded-lg font-semibold transition-colors">
                        Batal
                    </button>
                    <button type="submit" 
                            class="flex-1 bg-blue-600 hover:bg-blue-700 text-white py-3 rounded-lg font-semibold transition-colors">
                        Simpan
                    </button>
                </div>
            </form>
        </div>
    </div>

    <script>
        // Data storage
        let borrowers = JSON.parse(localStorage.getItem('borrowers')) || [];
        let editingIndex = -1;

        // Initialize the app
        document.addEventListener('DOMContentLoaded', function() {
            showPage('home');
            updateStats();
            renderBorrowers();
            
            // Set minimum date for return date input to tomorrow
            const tomorrow = new Date();
            tomorrow.setDate(tomorrow.getDate() + 1);
            document.getElementById('returnDate').min = tomorrow.toISOString().split('T')[0];
            
            // Check for overdue books on load
            setTimeout(() => {
                checkOverdueBooks();
            }, 1000);
        });

        // Navigation
        function showPage(pageId) {
            document.querySelectorAll('.page').forEach(page => page.classList.add('hidden'));
            
            if (pageId === 'home') {
                document.getElementById('homePage').classList.remove('hidden');
                updateStats();
            } else if (pageId === 'borrowers') {
                document.getElementById('borrowersPage').classList.remove('hidden');
                renderBorrowers();
            }
            
            // Update nav buttons
            document.querySelectorAll('.nav-btn').forEach(btn => {
                btn.classList.remove('bg-blue-500', 'text-white');
                btn.classList.add('bg-white', 'text-blue-600', 'border-2', 'border-blue-500');
            });
            
            if (pageId === 'home') {
                document.querySelector('button[onclick="showPage(\'home\')"]').classList.add('bg-blue-500', 'text-white');
                document.querySelector('button[onclick="showPage(\'home\')"]').classList.remove('bg-white', 'text-blue-600', 'border-2', 'border-blue-500');
            } else {
                document.querySelector('button[onclick="showPage(\'borrowers\')"]').classList.add('bg-blue-500', 'text-white');
                document.querySelector('button[onclick="showPage(\'borrowers\')"]').classList.remove('bg-white', 'text-blue-600', 'border-2', 'border-blue-500');
            }
        }

        // Modal functions
        function addNewBorrower() {
            editingIndex = -1;
            document.getElementById('modalTitle').textContent = 'Tambah Peminjam Baru';
            document.getElementById('borrowerForm').reset();
            document.getElementById('borrowerModal').classList.remove('hidden');
            document.getElementById('borrowerModal').classList.add('flex');
        }

        function editBorrower(index) {
            editingIndex = index;
            const borrower = borrowers[index];
            
            document.getElementById('modalTitle').textContent = 'Edit Data Peminjam';
            document.getElementById('borrowerName').value = borrower.name;
            document.getElementById('borrowerPhone').value = borrower.phone;
            document.getElementById('bookTitle').value = borrower.bookTitle;
            
            // Set return date in YYYY-MM-DD format for date input
            const returnDate = new Date(borrower.returnDate);
            document.getElementById('returnDate').value = returnDate.toISOString().split('T')[0];
            
            document.getElementById('borrowerModal').classList.remove('hidden');
            document.getElementById('borrowerModal').classList.add('flex');
        }

        function closeModal() {
            document.getElementById('borrowerModal').classList.add('hidden');
            document.getElementById('borrowerModal').classList.remove('flex');
        }

        // Save borrower
        function saveBorrower(event) {
            event.preventDefault();
            
            const name = document.getElementById('borrowerName').value;
            const phone = document.getElementById('borrowerPhone').value;
            const bookTitle = document.getElementById('bookTitle').value;
            const returnDateInput = document.getElementById('returnDate').value;
            
            const borrowDate = new Date();
            const returnDate = new Date(returnDateInput);
            
            // Validate return date is not in the past
            if (returnDate <= borrowDate) {
                showNotification('Tanggal kembali harus setelah hari ini!', 'error');
                return;
            }
            
            const borrower = {
                name,
                phone,
                bookTitle,
                borrowDate: borrowDate.toISOString(),
                returnDate: returnDate.toISOString(),
                returned: false
            };
            
            if (editingIndex >= 0) {
                borrowers[editingIndex] = borrower;
                showNotification('Data peminjam berhasil diperbarui!', 'success');
            } else {
                borrowers.push(borrower);
                showNotification('Peminjam baru berhasil ditambahkan!', 'success');
            }
            
            localStorage.setItem('borrowers', JSON.stringify(borrowers));
            closeModal();
            renderBorrowers();
            updateStats();
        }

        // Delete borrower
        function deleteBorrower(index) {
            if (confirm('Apakah Anda yakin ingin menghapus data peminjam ini?')) {
                borrowers.splice(index, 1);
                localStorage.setItem('borrowers', JSON.stringify(borrowers));
                renderBorrowers();
                updateStats();
                showNotification('Data peminjam berhasil dihapus!', 'success');
            }
        }

        // Ma
