<!DOCTYPE html>
<html lang="id" class="light">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>TUGAS SEKBID 3 OSIS</title>
    <!-- Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    <script>
        tailwind.config = {
            darkMode: 'class',
            theme: {
                extend: {
                    colors: {
                        brand: {
                            50: '#eff6ff',
                            100: '#dbeafe',
                            500: '#3b82f6',
                            600: '#2563eb',
                            700: '#1d4ed8',
                        }
                    }
                }
            }
        }
    </script>
    <!-- FontAwesome icons -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <!-- Google Fonts Inter -->
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&display=swap" rel="stylesheet">
    <style>
        body { font-family: 'Inter', sans-serif\\\; }
    </style>
</head>
<body class="bg-gray-50 dark:bg-gray-900 text-gray-800 dark:text-gray-100 min-h-screen flex flex-col transition-colors duration-200">

    <!-- Header / Navbar -->
    <header class="bg-white dark:bg-gray-800 border-b border-gray-200 dark:border-gray-700 sticky top-0 z-30 shadow-sm">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 h-16 flex items-center justify-between">
            <div class="flex items-center space-x-3">
                <div class="bg-brand-600 text-white p-2 rounded-xl shadow-md flex items-center justify-center w-10 h-10">
                    <i class="fa-solid fa-list-check text-lg"></i>
                </div>
                <div>
                    <h1 class="font-bold text-lg leading-tight">TUGAS SEKBID 3</h1>
                    <p class="text-xs text-gray-500 dark:text-gray-400" id="currentRoleText"</p>
                </div>
            </div>

            <div class="flex items-center space-x-3">
                <!-- Dark mode toggle -->
                <button onclick="toggleDarkMode()" class="p-2 rounded-lg bg-gray-100 dark:bg-gray-700 text-gray-600 dark:text-gray-300 hover:bg-gray-200 dark:hover:bg-gray-600 transition" title="Ganti Mode Tema">
                    <i id="themeIcon" class="fa-solid fa-moon"></i>
                </button>

                <!-- Auth Button / Status -->
                <div id="navAuthContainer">
                    <button onclick="openLoginModal()" class="inline-flex items-center px-4 py-2 bg-brand-600 hover:bg-brand-700 text-white text-sm font-medium rounded-xl shadow-sm transition">
                        <i class="fa-solid fa-right-to-bracket mr-2"></i> Login Admin
                    </button>
                </div>
            </div>
        </div>
    </header>

    <!-- Main Content Container -->
    <main class="flex-grow max-w-7xl w-full mx-auto px-4 sm:px-6 lg:px-8 py-8 space-y-8">
        
        <!-- Notification Banner Container -->
        <div id="notificationContainer" class="hidden fixed bottom-5 right-5 z-50 transition-all transform translate-y-0"></div>

        <!-- Statistics & Progress Widget -->
        <section class="grid grid-cols-1 md:grid-cols-4 gap-4">
            <div class="bg-white dark:bg-gray-800 p-5 rounded-2xl border border-gray-200 dark:border-gray-700 shadow-sm flex items-center justify-between">
                <div>
                    <p class="text-xs font-semibold uppercase tracking-wider text-gray-500 dark:text-gray-400">Total Tugas</p>
                    <h3 id="statTotal" class="text-3xl font-bold mt-1">0</h3>
                </div>
                <div class="p-3 bg-blue-50 dark:bg-blue-900/30 text-brand-600 dark:text-blue-400 rounded-xl">
                    <i class="fa-solid fa-clipboard-list text-xl"></i>
                </div>
            </div>
            <div class="bg-white dark:bg-gray-800 p-5 rounded-2xl border border-gray-200 dark:border-gray-700 shadow-sm flex items-center justify-between">
                <div>
                    <p class="text-xs font-semibold uppercase tracking-wider text-gray-500 dark:text-gray-400">Belum Mulai</p>
                    <h3 id="statTodo" class="text-3xl font-bold mt-1 text-amber-500">0</h3>
                </div>
                <div class="p-3 bg-amber-50 dark:bg-amber-900/30 text-amber-600 rounded-xl">
                    <i class="fa-solid fa-hourglass-start text-xl"></i>
                </div>
            </div>
            <div class="bg-white dark:bg-gray-800 p-5 rounded-2xl border border-gray-200 dark:border-gray-700 shadow-sm flex items-center justify-between">
                <div>
                    <p class="text-xs font-semibold uppercase tracking-wider text-gray-500 dark:text-gray-400">Sedang Dikerjakan</p>
                    <h3 id="statInProgress" class="text-3xl font-bold mt-1 text-blue-500">0</h3>
                </div>
                <div class="p-3 bg-blue-50 dark:bg-blue-900/30 text-blue-600 rounded-xl">
                    <i class="fa-solid fa-spinner text-xl"></i>
                </div>
            </div>
            <div class="bg-white dark:bg-gray-800 p-5 rounded-2xl border border-gray-200 dark:border-gray-700 shadow-sm flex items-center justify-between">
                <div>
                    <p class="text-xs font-semibold uppercase tracking-wider text-gray-500 dark:text-gray-400">Selesai</p>
                    <h3 id="statDone" class="text-3xl font-bold mt-1 text-emerald-500">0</h3>
                </div>
                <div class="p-3 bg-emerald-50 dark:bg-emerald-900/30 text-emerald-600 rounded-xl">
                    <i class="fa-solid fa-circle-check text-xl"></i>
                </div>
            </div>
        </section>

        <!-- Progress Bar Card -->
        <section class="bg-white dark:bg-gray-800 p-6 rounded-2xl border border-gray-200 dark:border-gray-700 shadow-sm">
            <div class="flex justify-between items-center mb-2">
                <span class="text-sm font-semibold text-gray-700 dark:text-gray-300">Progress Penyelesaian Tugas</span>
                <span id="progressPercentage" class="text-sm font-bold text-brand-600 dark:text-brand-400">0%</span>
            </div>
            <div class="w-full bg-gray-200 dark:bg-gray-700 h-3 rounded-full overflow-hidden">
                <div id="progressBarFill" class="bg-emerald-500 h-full transition-all duration-500 rounded-full" style="width: 0%"></div>
            </div>
        </section>

        <!-- Controls & Filter Toolbar -->
        <section class="bg-white dark:bg-gray-800 p-5 rounded-2xl border border-gray-200 dark:border-gray-700 shadow-sm flex flex-col lg:flex-row gap-4 items-center justify-between">
            <div class="grid grid-cols-1 sm:grid-cols-3 gap-3 w-full lg:w-auto flex-grow">
                <!-- Search -->
                <div class="relative">
                    <span class="absolute inset-y-0 left-0 pl-3 flex items-center pointer-events-none text-gray-400">
                        <i class="fa-solid fa-search"></i>
                    </span>
                    <input type="text" id="filterSearch" oninput="applyFilters()" placeholder="Cari judul atau penanggung jawab..." class="w-full pl-10 pr-4 py-2 bg-gray-50 dark:bg-gray-700 border border-gray-300 dark:border-gray-600 rounded-xl text-sm focus:outline-none focus:ring-2 focus:ring-brand-500">
                </div>
                <!-- Status Filter -->
                <select id="filterStatus" onchange="applyFilters()" class="w-full px-3 py-2 bg-gray-50 dark:bg-gray-700 border border-gray-300 dark:border-gray-600 rounded-xl text-sm focus:outline-none focus:ring-2 focus:ring-brand-500">
                    <option value="">Semua Status</option>
                    <option value="Belum Dikerjakan">Belum Dikerjakan</option>
                    <option value="Sedang Dikerjakan">Sedang Dikerjakan</option>
                    <option value="Selesai">Selesai</option>
                </select>
                <!-- Priority Filter -->
                <select id="filterPriority" onchange="applyFilters()" class="w-full px-3 py-2 bg-gray-50 dark:bg-gray-700 border border-gray-300 dark:border-gray-600 rounded-xl text-sm focus:outline-none focus:ring-2 focus:ring-brand-500">
                    <option value="">Semua Prioritas</option>
                    <option value="Rendah">Rendah</option>
                    <option value="Sedang">Sedang</option>
                    <option value="Tinggi">Tinggi</option>
                </select>
            </div>

            <!-- Admin Action Button (Hidden for Spectators) -->
            <div id="adminActionContainer" class="w-full lg:w-auto flex justify-end">
                <!-- Rendered dynamically based on auth state -->
            </div>
        </section>

        <!-- Task Grid Container -->
        <section>
            <div class="flex items-center justify-between mb-4">
                <h2 class="text-lg font-bold">Daftar Tugas</h2>
                <span id="taskCountLabel" class="text-xs text-gray-500 dark:text-gray-400">Menampilkan 0 tugas</span>
            </div>
            <div id="tasksContainer" class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
                <!-- Task Cards injected via JavaScript -->
            </div>
        </section>

    </main>

    <!-- Footer -->
    <footer class="mt-auto py-6 border-t border-gray-200 dark:border-gray-700 bg-white dark:bg-gray-800 text-center text-xs text-gray-500 dark:text-gray-400">
        <p>SEKBID 3 OSIS 2026/2027</p>
    </footer>

    <!-- Login Modal -->
    <div id="loginModal" class="fixed inset-0 z-50 bg-black/50 backdrop-blur-sm hidden flex items-center justify-center p-4">
        <div class="bg-white dark:bg-gray-800 rounded-2xl shadow-xl max-w-md w-full p-6 border border-gray-200 dark:border-gray-700 relative animate-in fade-in zoom-in duration-200">
            <div class="flex justify-between items-center mb-4">
                <div class="flex items-center space-x-2">
                    <div class="bg-brand-600 text-white p-2 rounded-lg">
                        <i class="fa-solid fa-lock text-sm"></i>
                    </div>
                    <h3 class="font-bold text-lg">Login Admin</h3>
                </div>
                <button onclick="closeLoginModal()" class="text-gray-400 hover:text-gray-600 dark:hover:text-gray-200 p-1">
                    <i class="fa-solid fa-xmark text-lg"></i>
                </button>
            </div>
            <form id="loginForm" onsubmit="handleLogin(event)" class="space-y-4">
                <div>
                    <label class="block text-xs font-semibold uppercase tracking-wider text-gray-600 dark:text-gray-300 mb-1">Username Admin</label>
                    <input type="text" id="loginUsername" required placeholder="Masukkan username admin" class="w-full px-4 py-2.5 bg-gray-50 dark:bg-gray-700 border border-gray-300 dark:border-gray-600 rounded-xl text-sm focus:outline-none focus:ring-2 focus:ring-brand-500">
                </div>
                <div>
                    <label class="block text-xs font-semibold uppercase tracking-wider text-gray-600 dark:text-gray-300 mb-1">Password</label>
                    <input type="password" id="loginPassword" required placeholder="Masukkan password" class="w-full px-4 py-2.5 bg-gray-50 dark:bg-gray-700 border border-gray-300 dark:border-gray-600 rounded-xl text-sm focus:outline-none focus:ring-2 focus:ring-brand-500">
                </div>
                <div id="loginErrorMsg" class="hidden text-xs text-red-500 font-medium bg-red-50 dark:bg-red-900/30 p-2.5 rounded-lg border border-red-200 dark:border-red-800"></div>
                <div class="flex justify-end space-x-3 pt-2">
                    <button type="button" onclick="closeLoginModal()" class="px-4 py-2 bg-gray-100 dark:bg-gray-700 hover:bg-gray-200 dark:hover:bg-gray-600 text-sm font-medium rounded-xl transition">Batal</button>
                    <button type="submit" class="px-5 py-2 bg-brand-600 hover:bg-brand-700 text-white text-sm font-medium rounded-xl shadow transition">Masuk</button>
                </div>
            </form>
            <div class="mt-4 pt-4 border-t border-gray-100 dark:border-gray-700 text-center">
            </div>
        </div>
    </div>

    <!-- Task Modal (Add/Edit) -->
    <div id="taskModal" class="fixed inset-0 z-50 bg-black/50 backdrop-blur-sm hidden flex items-center justify-center p-4">
        <div class="bg-white dark:bg-gray-800 rounded-2xl shadow-xl max-w-lg w-full p-6 border border-gray-200 dark:border-gray-700 relative">
            <div class="flex justify-between items-center mb-4">
                <h3 id="taskModalTitle" class="font-bold text-lg">Tambah Tugas Baru</h3>
                <button onclick="closeTaskModal()" class="text-gray-400 hover:text-gray-600 dark:hover:text-gray-200 p-1">
                    <i class="fa-solid fa-xmark text-lg"></i>
                </button>
            </div>
            <form id="taskForm" onsubmit="handleSaveTask(event)" class="space-y-4">
                <input type="hidden" id="taskId">
                <div>
                    <label class="block text-xs font-semibold uppercase tracking-wider text-gray-600 dark:text-gray-300 mb-1">Judul Tugas *</label>
                    <input type="text" id="taskTitleInput" required maxlength="100" placeholder="Contoh: Desain Halaman Landing" class="w-full px-4 py-2 bg-gray-50 dark:bg-gray-700 border border-gray-300 dark:border-gray-600 rounded-xl text-sm focus:outline-none focus:ring-2 focus:ring-brand-500">
                </div>
                <div>
                    <label class="block text-xs font-semibold uppercase tracking-wider text-gray-600 dark:text-gray-300 mb-1">Deskripsi</label>
                    <textarea id="taskDescInput" rows="3" placeholder="Deskripsi detail tugas..." class="w-full px-4 py-2 bg-gray-50 dark:bg-gray-700 border border-gray-300 dark:border-gray-600 rounded-xl text-sm focus:outline-none focus:ring-2 focus:ring-brand-500"></textarea>
                </div>
                <div class="grid grid-cols-1 sm:grid-cols-2 gap-4">
                    <div>
                        <label class="block text-xs font-semibold uppercase tracking-wider text-gray-600 dark:text-gray-300 mb-1">Penanggung Jawab *</label>
                        <input type="text" id="taskAssigneeInput" required placeholder="Nama Anggota Tim" class="w-full px-4 py-2 bg-gray-50 dark:bg-gray-700 border border-gray-300 dark:border-gray-600 rounded-xl text-sm focus:outline-none focus:ring-2 focus:ring-brand-500">
                    </div>
                    <div>
                        <label class="block text-xs font-semibold uppercase tracking-wider text-gray-600 dark:text-gray-300 mb-1">Tenggat (Deadline) *</label>
                        <input type="date" id="taskDeadlineInput" required class="w-full px-4 py-2 bg-gray-50 dark:bg-gray-700 border border-gray-300 dark:border-gray-600 rounded-xl text-sm focus:outline-none focus:ring-2 focus:ring-brand-500">
                    </div>
                </div>
                <div class="grid grid-cols-1 sm:grid-cols-2 gap-4">
                    <div>
                        <label class="block text-xs font-semibold uppercase tracking-wider text-gray-600 dark:text-gray-300 mb-1">Prioritas</label>
                        <select id="taskPriorityInput" class="w-full px-4 py-2 bg-gray-50 dark:bg-gray-700 border border-gray-300 dark:border-gray-600 rounded-xl text-sm focus:outline-none focus:ring-2 focus:ring-brand-500">
                            <option value="Rendah">Rendah</option>
                            <option value="Sedang" selected>Sedang</option>
                            <option value="Tinggi">Tinggi</option>
                        </select>
                    </div>
                    <div>
                        <label class="block text-xs font-semibold uppercase tracking-wider text-gray-600 dark:text-gray-300 mb-1">Status</label>
                        <select id="taskStatusInput" class="w-full px-4 py-2 bg-gray-50 dark:bg-gray-700 border border-gray-300 dark:border-gray-600 rounded-xl text-sm focus:outline-none focus:ring-2 focus:ring-brand-500">
                            <option value="Belum Dikerjakan">Belum Dikerjakan</option>
                            <option value="Sedang Dikerjakan">Sedang Dikerjakan</option>
                            <option value="Selesai">Selesai</option>
                        </select>
                    </div>
                </div>
                <div class="flex justify-end space-x-3 pt-3">
                    <button type="button" onclick="closeTaskModal()" class="px-4 py-2 bg-gray-100 dark:bg-gray-700 hover:bg-gray-200 dark:hover:bg-gray-600 text-sm font-medium rounded-xl transition">Batal</button>
                    <button type="submit" class="px-5 py-2 bg-brand-600 hover:bg-brand-700 text-white text-sm font-medium rounded-xl shadow transition">Simpan Tugas</button>
                </div>
            </form>
        </div>
    </div>

    <!-- Application JavaScript -->
    <script>
        // Mock state database & current user session
        let currentUser = null; // null = spectator, { username: 'ADMIN1' } = admin
        let tasks = [
            {
                id: 1,
                title: 'SUMPAH PEMUDA',
                description: '',
                assignee: '',
                priority: 'Rendah',
                status: 'Sedang dikerjakan',
                deadline: '2026-10-27'
            },
            {
                id: 2,
                title: 'Konfigurasi Middleware Autentikasi',
                description: 'Implementasi session cookie dan hashing bcrypt dengan rate limiter.',
                assignee: 'Siti Rahma',
                priority: 'Tinggi',
                status: 'Sedang Dikerjakan',
                deadline: '2026-04-18'
            },
            {
                id: 3,
                title: 'Desain Antarmuka Tailwind CSS',
                description: 'Membuat layout responsif dengan dukungan mode gelap dan terang.',
                assignee: 'Ahmad Fauzi',
                priority: 'Sedang',
                status: 'Belum Dikerjakan',
                deadline: '2026-04-25'
            },
            {
                id: 4,
                title: 'Pengujian Unit API & Keamanan XSS',
                description: 'Memastikan semua endpoint terlindungi dan teks ter-escape dengan aman.',
                assignee: 'Dewi Lestari',
                priority: 'Rendah',
                status: 'Belum Dikerjakan',
                deadline: '2026-04-05' // Past deadline for testing overdue logic
            },
            {
                id: 5,
                title: 'Dokumentasi Panduan Penggunaan README',
                description: 'Menyusun langkah instalasi dan konfigurasi file env.',
                assignee: 'Budi Santoso',
                priority: 'Sedang',
                status: 'Selesai',
                deadline: '2026-04-12'
            }
        ];

        // On page load
        window.onload = function() {
            // Check stored theme preference
            if (localStorage.theme === 'dark' || (!('theme' in localStorage) && window.matchMedia('(prefers-color-scheme: dark)').matches)) {
                document.documentElement.classList.add('dark');
                document.getElementById('themeIcon').className = 'fa-solid fa-sun';
            } else {
                document.documentElement.classList.remove('dark');
                document.getElementById('themeIcon').className = 'fa-solid fa-moon';
            }

            // Check if simulated admin session exists in sessionStorage
            const sessionAdmin = sessionStorage.getItem('adminUser');
            if (sessionAdmin) {
                currentUser = { username: sessionAdmin };
            }

            renderApp();
        };

        // Dark Mode Toggle
        function toggleDarkMode() {
            if (document.documentElement.classList.contains('dark')) {
                document.documentElement.classList.remove('dark');
                localStorage.theme = 'light';
                document.getElementById('themeIcon').className = 'fa-solid fa-moon';
            } else {
                document.documentElement.classList.add('dark');
                localStorage.theme = 'dark';
                document.getElementById('themeIcon').className = 'fa-solid fa-sun';
            }
        }

        // Render entire app based on auth state
        function renderApp() {
            renderNavbarAuth();
            renderAdminAction();
            updateStatistics();
            applyFilters();
        }

        // Render Navbar Authentication area
        function renderNavbarAuth() {
            const container = document.getElementById('navAuthContainer');
            const roleText = document.getElementById('currentRoleText');

            if (currentUser) {
                roleText.innerHTML = `<span class="text-emerald-600 dark:text-emerald-400 font-semibold">Admin: ${escapeHtml(currentUser.username)}</span>`;
                container.innerHTML = `
                    <button onclick="handleLogout()" class="inline-flex items-center px-3.5 py-2 bg-red-50 hover:bg-red-100 text-red-600 dark:bg-red-900/30 dark:hover:bg-red-900/50 dark:text-red-400 text-sm font-medium rounded-xl transition">
                        <i class="fa-solid fa-right-from-bracket mr-2"></i> Logout
                    </button>
                `;
            } else {
                roleText.innerText = 'Mode Penonton (Read-Only)';
                container.innerHTML = `
                    <button onclick="openLoginModal()" class="inline-flex items-center px-4 py-2 bg-brand-600 hover:bg-brand-700 text-white text-sm font-medium rounded-xl shadow-sm transition">
                        <i class="fa-solid fa-right-to-bracket mr-2"></i> Login Admin
                    </button>
                `;
            }
        }

        // Render Admin action button above task list
        function renderAdminAction() {
            const container = document.getElementById('adminActionContainer');
            if (currentUser) {
                container.innerHTML = `
                    <button onclick="openTaskModal()" class="w-full lg:w-auto inline-flex items-center justify-center px-4 py-2.5 bg-emerald-600 hover:bg-emerald-700 text-white text-sm font-medium rounded-xl shadow-sm transition">
                        <i class="fa-solid fa-plus mr-2"></i> Tambah Tugas Baru
                    </button>
                `;
            } else {
                container.innerHTML = '';
            }
        }

        // Update statistics counters & progress bar
        function updateStatistics() {
            const total = tasks.length;
            const todo = tasks.filter(t => t.status === 'Belum Dikerjakan').length;
            const inProgress = tasks.filter(t => t.status === 'Sedang Dikerjakan').length;
            const done = tasks.filter(t => t.status === 'Selesai').length;

            document.getElementById('statTotal').innerText = total;
            document.getElementById('statTodo').innerText = todo;
            document.getElementById('statInProgress').innerText = inProgress;
            document.getElementById('statDone').innerText = done;

            const percentage = total > 0 ? Math.round((done / total) * 100) : 0;
            document.getElementById('progressPercentage').innerText = percentage + '%';
            document.getElementById('progressBarFill').style.width = percentage + '%';
        }

        // Apply filters and render task cards
        function applyFilters() {
            const searchQuery = document.getElementById('filterSearch').value.toLowerCase();
            const statusFilter = document.getElementById('filterStatus').value;
            const priorityFilter = document.getElementById('filterPriority').value;

            const filtered = tasks.filter(t => {
                const matchSearch = t.title.toLowerCase().includes(searchQuery) || t.assignee.toLowerCase().includes(searchQuery);
                const matchStatus = statusFilter === '' || t.status === statusFilter;
                const matchPriority = priorityFilter === '' || t.priority === priorityFilter;
                return matchSearch && matchStatus && matchPriority;
            });

            document.getElementById('taskCountLabel').innerText = `Menampilkan ${filtered.length} dari ${tasks.length} tugas`;
            renderTasks(filtered);
        }

        // Render task cards into the grid container
        function renderTasks(taskList) {
            const container = document.getElementById('tasksContainer');
            
            if (taskList.length === 0) {
                container.innerHTML = `
                    <div class="col-span-full py-12 text-center bg-white dark:bg-gray-800 rounded-2xl border border-gray-200 dark:border-gray-700">
                        <div class="text-gray-400 mb-2">
                            <i class="fa-solid fa-folder-open text-3xl"></i>
                        </div>
                        <p class="text-gray-500 dark:text-gray-400 text-sm font-medium">Tidak ada tugas yang ditemukan.</p>
                    </div>
                `;
                return;
            }

            const today = new Date().toISOString().split('T')[0];

            container.innerHTML = taskList.map(task => {
                const isOverdue = task.deadline < today && task.status !== 'Selesai';
                
                // Priority Badge Style
                let priorityBadge = 'bg-blue-50 text-blue-700 dark:bg-blue-900/30 dark:text-blue-300';
                if (task.priority === 'Tinggi') priorityBadge = 'bg-red-50 text-red-700 dark:bg-red-900/30 dark:text-red-300';
                if (task.priority === 'Sedang') priorityBadge = 'bg-amber-50 text-amber-700 dark:bg-amber-900/30 dark:text-amber-300';

                // Status Badge Style
                let statusBadge = 'bg-gray-100 text-gray-700 dark:bg-gray-700 dark:text-gray-300';
                if (task.status === 'Belum Dikerjakan') statusBadge = 'bg-amber-50 text-amber-700 dark:bg-amber-900/30 dark:text-amber-300';
                if (task.status === 'Sedang Dikerjakan') statusBadge = 'bg-blue-50 text-blue-700 dark:bg-blue-900/30 dark:text-blue-300';
                if (task.status === 'Selesai') statusBadge = 'bg-emerald-50 text-emerald-700 dark:bg-emerald-900/30 dark:text-emerald-300';

                return `
                    <div class="bg-white dark:bg-gray-800 rounded-2xl border border-gray-200 dark:border-gray-700 shadow-sm hover:shadow-md transition flex flex-col justify-between p-5 relative overflow-hidden">
                        ${isOverdue ? '<div class="absolute top-0 right-0 bg-red-500 text-white text-[10px] font-bold px-3 py-1 rounded-bl-xl uppercase tracking-wider">Terlambat</div>' : ''}
                        
                        <div>
                            <div class="flex items-start justify-between gap-2 mb-3">
                                <span class="px-2.5 py-1 text-xs font-semibold rounded-lg ${priorityBadge}">${escapeHtml(task.priority)}</span>
                                <span class="px-2.5 py-1 text-xs font-semibold rounded-lg ${statusBadge}">${escapeHtml(task.status)}</span>
                            </div>

                            <h3 class="font-bold text-base mb-1.5 line-clamp-2">${escapeHtml(task.title)}</h3>
                            <p class="text-xs text-gray-500 dark:text-gray-400 mb-4 line-clamp-3">${escapeHtml(task.description || 'Tidak ada deskripsi.')}</p>
                        </div>

                        <div class="border-t border-gray-100 dark:border-gray-700 pt-4 mt-2 space-y-3">
                            <div class="flex items-center justify-between text-xs text-gray-600 dark:text-gray-300">
                                <span class="flex items-center"><i class="fa-solid fa-user-circle mr-1.5 text-gray-400"></i> ${escapeHtml(task.assignee)}</span>
                                <span class="flex items-center ${isOverdue ? 'text-red-500 font-semibold' : ''}"><i class="fa-regular fa-calendar mr-1.5 text-gray-400"></i> ${escapeHtml(task.deadline)}</span>
                            </div>

                            <!-- Admin Quick Status Change & Edit/Delete Actions -->
                            ${currentUser ? `
                                <div class="flex items-center justify-between pt-2 border-t border-dashed border-gray-200 dark:border-gray-700">
                                    <select onchange="quickUpdateStatus(${task.id}, this.value)" class="text-xs px-2 py-1 bg-gray-50 dark:bg-gray-700 border border-gray-300 dark:border-gray-600 rounded-lg focus:outline-none">
                                        <option value="Belum Dikerjakan" ${task.status === 'Belum Dikerjakan' ? 'selected' : ''}>Belum</option>
                                        <option value="Sedang Dikerjakan" ${task.status === 'Sedang Dikerjakan' ? 'selected' : ''}>Proses</option>
                                        <option value="Selesai" ${task.status === 'Selesai' ? 'selected' : ''}>Selesai</option>
                                    </select>
                                    <div class="flex space-x-1">
                                        <button onclick="openEditTaskModal(${task.id})" class="p-1.5 text-brand-600 hover:bg-brand-50 dark:hover:bg-gray-700 rounded-lg transition" title="Edit Tugas">
                                            <i class="fa-solid fa-pen-to-square text-xs"></i>
                                        </button>
                                        <button onclick="deleteTask(${task.id})" class="p-1.5 text-red-600 hover:bg-red-50 dark:hover:bg-gray-700 rounded-lg transition" title="Hapus Tugas">
                                            <i class="fa-solid fa-trash text-xs"></i>
                                        </button>
                                    </div>
                                </div>
                            ` : ''}
                        </div>
                    </div>
                `;
            }).join('');
        }

        // XSS Escape helper
        function escapeHtml(str) {
            if (!str) return '';
            return String(str)
                .replace(/&/g, '&amp;')
                .replace(/</g, '&lt;')
                .replace(/>/g, '&gt;')
                .replace(/"/g, '&quot;')
                .replace(/'/g, '&#039;');
        }

        // Notification popup toast
        function showNotification(message, type = 'success') {
            const container = document.getElementById('notificationContainer');
            const bgClass = type === 'success' ? 'bg-emerald-600 text-white' : 'bg-red-600 text-white';
            container.className = `fixed bottom-5 right-5 z-50 px-4 py-3 rounded-xl shadow-lg text-sm font-medium ${bgClass} transition-all transform translate-y-0`;
            container.innerHTML = `<div class="flex items-center space-x-2"><i class="fa-solid ${type === 'success' ? 'fa-circle-check' : 'fa-triangle-exclamation'}"></i><span>${message}</span></div>`;
            container.classList.remove('hidden');
            setTimeout(() => {
                container.classList.add('hidden');
            }, 3000);
        }

        // Login Modal Controls
        function openLoginModal() {
            document.getElementById('loginUsername').value = '';
            document.getElementById('loginPassword').value = '';
            document.getElementById('loginErrorMsg').classList.add('hidden');
            document.getElementById('loginModal').classList.remove('hidden');
        }
        function closeLoginModal() {
            document.getElementById('loginModal').classList.add('hidden');
        }

        // Handle Login Submission
        function handleLogin(event) {
            event.preventDefault();
            const username = document.getElementById('loginUsername').value.trim();
            const password = document.getElementById('loginPassword').value;

            // Simulated authentication check matching .env requirements (ADMIN1 / ADMIN123)
            if (username === 'ADMIN1' && password === 'ADMIN123') {
                currentUser = { username: 'ADMIN1' };
                sessionStorage.setItem('adminUser', 'ADMIN1');
                closeLoginModal();
                showNotification('Login berhasil! Selamat datang Admin.');
                renderApp();
            } else {
                const errBox = document.getElementById('loginErrorMsg');
                errBox.innerText = 'BUKAN ADMMIN GA USAH COBA COBA.';
                errBox.classList.remove('hidden');
            }
        }

        // Handle Logout
        function handleLogout() {
            currentUser = null;
            sessionStorage.removeItem('adminUser');
            showNotification('Berhasil logout dari mode admin.', 'success');
            renderApp();
        }

        // Task Modal Controls (Add/Edit)
        function openTaskModal() {
            document.getElementById('taskId').value = '';
            document.getElementById('taskModalTitle').innerText = 'Tambah Tugas Baru';
            document.getElementById('taskTitleInput').value = '';
            document.getElementById('taskDescInput').value = '';
            document.getElementById('taskAssigneeInput').value = '';
            document.getElementById('taskDeadlineInput').value = new Date().toISOString().split('T')[0];
            document.getElementById('taskPriorityInput').value = 'Sedang';
            document.getElementById('taskStatusInput').value = 'Belum Dikerjakan';
            document.getElementById('taskModal').classList.remove('hidden');
        }

        function openEditTaskModal(id) {
            const task = tasks.find(t => t.id === id);
            if (!task) return;

            document.getElementById('taskId').value = task.id;
            document.getElementById('taskModalTitle').innerText = 'Edit Tugas';
            document.getElementById('taskTitleInput').value = task.title;
            document.getElementById('taskDescInput').value = task.description;
            document.getElementById('taskAssigneeInput').value = task.assignee;
            document.getElementById('taskDeadlineInput').value = task.deadline;
            document.getElementById('taskPriorityInput').value = task.priority;
            document.getElementById('taskStatusInput').value = task.status;
            document.getElementById('taskModal').classList.remove('hidden');
        }

        function closeTaskModal() {
            document.getElementById('taskModal').classList.add('hidden');
        }

        // Handle Save Task (Create or Update)
        function handleSaveTask(event) {
            event.preventDefault();
            if (!currentUser) {
                showNotification('Akses ditolak. Anda bukan admin.', 'error');
                return;
            }

            const id = document.getElementById('taskId').value;
            const title = document.getElementById('taskTitleInput').value.trim();
            const description = document.getElementById('taskDescInput').value.trim();
            const assignee = document.getElementById('taskAssigneeInput').value.trim();
            const deadline = document.getElementById('taskDeadlineInput').value;
            const priority = document.getElementById('taskPriorityInput').value;
            const status = document.getElementById('taskStatusInput').value;

            if (!title || !assignee || !deadline) {
                showNotification('Harap isi semua field yang wajib.', 'error');
                return;
            }

            if (id) {
                // Update existing task
                const index = tasks.findIndex(t => t.id == id);
                if (index !== -1) {
                    tasks[index] = { ...tasks[index], title, description, assignee, deadline, priority, status };
                    showNotification('Tugas berhasil diperbarui!');
                }
            } else {
                // Create new task
                const newTask = {
                    id: tasks.length > 0 ? Math.max(...tasks.map(t => t.id)) + 1 : 1,
                    title,
                    description,
                    assignee,
                    deadline,
                    priority,
                    status
                };
                tasks.push(newTask);
                showNotification('Tugas baru berhasil ditambahkan!');
            }

            closeTaskModal();
            renderApp();
        }

        // Quick status update from task card
        function quickUpdateStatus(id, newStatus) {
            if (!currentUser) return;
            const task = tasks.find(t => t.id === id);
            if (task) {
                task.status = newStatus;
                showNotification(`Status tugas diubah ke "${newStatus}"`);
                renderApp();
            }
        }

        // Delete task with confirmation
        function deleteTask(id) {
            if (!currentUser) return;
            if (confirm('Apakah Anda yakin ingin menghapus tugas ini?')) {
                tasks = tasks.filter(t => t.id !== id);
                showNotification('Tugas berhasil dihapus.');
                renderApp();
            }
        }
    </script>
</body>
</html>
