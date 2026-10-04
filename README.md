<html lang="Servicku.id" class="scroll-smooth">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Serviceku - Jasa Service Elektronik Indramayu, Cirebon & Majalengka</title>
    <!-- Tailwind CSS CDN -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- FontAwesome Icons -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.1/css/all.min.css">
    <!-- Google Fonts Inter -->
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700;800&display=swap" rel="stylesheet">

    <script>
        tailwind.config = {
            theme: {
                extend: {
                    colors: {
                        brand: {
                            50: '#f0f7ff',
                            100: '#e0effe',
                            500: '#0284c7',
                            600: '#0265a3',
                            700: '#0369a1',
                            800: '#075985',
                            900: '#0c4a6e',
                            gold: '#f59e0b',
                            accent: '#10b981'
                        }
                    },
                    fontFamily: {
                        sans: ['Inter', 'sans-serif'],
                    }
                }
            }
        }
    </script>
    <style>
        .gradient-banner-1 { background: linear-gradient(135deg, #0f172a 0%, #1e3a8a 50%, #0369a1 100%); }
        .gradient-banner-2 { background: linear-gradient(135deg, #022c22 0%, #065f46 50%, #0f766e 100%); }
        .gradient-banner-3 { background: linear-gradient(135deg, #31103f 0%, #701a75 50%, #0284c7 100%); }
        .glass-card {
            background: rgba(255, 255, 255, 0.95);
            backdrop-filter: blur(10px);
        }
        /* Custom scrollbar */
        ::-webkit-scrollbar { width: 8px; }
        ::-webkit-scrollbar-track { background: #f1f5f9; }
        ::-webkit-scrollbar-thumb { background: #cbd5e1; border-radius: 4px; }
        ::-webkit-scrollbar-thumb:hover { background: #94a3b8; }
    </style>
</head>
<body class="bg-slate-50 text-slate-800 font-sans antialiased flex flex-col min-h-screen selection:bg-brand-500 selection:text-white">

    <!-- HEADER & NAVBAR -->
    <header class="sticky top-0 z-40 bg-white/90 backdrop-blur-md border-b border-slate-200 shadow-sm transition-all duration-300">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 h-20 flex items-center justify-between">
            <!-- Brand Logo -->
            <a href="#" class="flex items-center gap-3 group">
                <div class="relative w-12 h-12 rounded-xl bg-gradient-to-tr from-brand-700 to-blue-500 flex items-center justify-center text-white shadow-md shadow-brand-500/20 group-hover:scale-105 transition-transform overflow-hidden">
                    <img id="header-logo-img" src="https://lh3.googleusercontent.com/d/1xLoqpa4lr1o8_sM323Zm5HYN_BlfIU0x" alt="Serviceku Logo" class="w-full h-full object-cover" onerror="this.style.display='none'; document.getElementById('fallback-logo-icon').classList.remove('hidden');">
                    <i id="fallback-logo-icon" class="fa-solid fa-screwdriver-wrench text-2xl hidden"></i>
                </div>
                <div>
                    <span class="text-2xl font-black tracking-tight text-slate-900 group-hover:text-brand-600 transition-colors">Service<span class="text-brand-500">ku</span></span>
                    <p class="text-[10px] font-semibold tracking-wider text-slate-500 uppercase -mt-1">Panggilan Elektronik</p>
                </div>
            </a>

            <!-- Desktop Nav Links -->
            <nav class="hidden md:flex items-center gap-8 text-sm font-semibold text-slate-600">
                <a href="#beranda" class="hover:text-brand-600 transition-colors">Beranda</a>
                <a href="#katalog" class="hover:text-brand-600 transition-colors">Katalog Jasa</a>
                <a href="#keunggulan" class="hover:text-brand-600 transition-colors">Keunggulan</a>
                <a href="#wilayah" class="hover:text-brand-600 transition-colors">Wilayah Layanan</a>
            </nav>

            <!-- Actions & Admin Login -->
            <div class="flex items-center gap-3">
                <a href="https://wa.me/6287874417978?text=Halo%20Serviceku,%20saya%20ingin%20konsultasi%20mengenai%20service%20elektronik." target="_blank" rel="noopener noreferrer" class="hidden sm:inline-flex items-center gap-2 bg-emerald-600 hover:bg-emerald-700 text-white px-4 py-2.5 rounded-xl font-semibold text-sm shadow-md shadow-emerald-600/20 hover:shadow-lg transition-all active:scale-95">
                    <i class="fa-brands fa-whatsapp text-lg"></i>
                    <span>Hubungi Kami</span>
                </a>

                <!-- Admin Status / Login Toggle -->
                <button id="admin-login-btn" onclick="openAdminModal()" class="inline-flex items-center gap-2 bg-slate-900 hover:bg-slate-800 text-white px-4 py-2.5 rounded-xl font-semibold text-sm shadow-sm transition-all active:scale-95">
                    <i class="fa-solid fa-user-shield text-brand-500"></i>
                    <span id="admin-btn-text">Admin Login</span>
                </button>
            </div>
        </div>
    </header>

    <!-- HERO SLIDESHOW BANNER -->
    <section id="beranda" class="relative bg-slate-900 text-white overflow-hidden">
        <div id="slideshow-container" class="relative min-h-[420px] md:min-h-[480px] flex items-center">
            <!-- Slide items will be dynamically generated via JS -->
            <div id="slides-wrapper" class="w-full h-full flex transition-transform duration-700 ease-in-out">
                <!-- Fallback Loading State -->
                <div class="w-full flex-shrink-0 gradient-banner-1 py-16 px-6 md:px-16 flex items-center">
                    <div class="max-w-4xl mx-auto text-center md:text-left space-y-4">
                        <span class="inline-block px-3 py-1 bg-white/20 backdrop-blur-md rounded-full text-xs font-bold uppercase tracking-wider text-amber-300">Spesialis Service Elektronik</span>
                        <h1 class="text-3xl md:text-5xl font-black leading-tight">Layanan Service AC, Kulkas & Mesin Cuci Terpercaya</h1>
                        <p class="text-slate-200 text-sm md:text-lg max-w-2xl">Teknisi berpengalaman, pengerjaan cepat, sparepart berkualitas & bergaransi hingga 1 bulan!</p>
                    </div>
                </div>
            </div>

            <!-- Carousel Controls -->
            <button onclick="prevSlide()" class="absolute left-4 top-1/2 -translate-y-1/2 w-10 h-10 rounded-full bg-black/40 hover:bg-black/60 text-white backdrop-blur-sm flex items-center justify-center transition-all">
                <i class="fa-solid fa-chevron-left"></i>
            </button>
            <button onclick="nextSlide()" class="absolute right-4 top-1/2 -translate-y-1/2 w-10 h-10 rounded-full bg-black/40 hover:bg-black/60 text-white backdrop-blur-sm flex items-center justify-center transition-all">
                <i class="fa-solid fa-chevron-right"></i>
            </button>

            <!-- Indicators -->
            <div id="slideshow-indicators" class="absolute bottom-4 left-1/2 -translate-x-1/2 flex gap-2 z-10">
                <!-- Dots injected via JS -->
            </div>
        </div>

        <!-- Banner Info Bar -->
        <div class="bg-slate-950/80 border-t border-slate-800 py-3 px-4 backdrop-blur-md">
            <div class="max-w-7xl mx-auto flex flex-wrap items-center justify-between gap-4 text-xs md:text-sm text-slate-300">
                <div class="flex items-center gap-2">
                    <i class="fa-solid fa-certificate text-amber-400"></i>
                    <span><strong>GARANSI 1 BULAN</strong> untuk kerusakan yang sama</span>
                </div>
                <div class="flex items-center gap-2">
                    <i class="fa-solid fa-location-dot text-red-400"></i>
                    <span>Area Layanan: <strong>Indramayu, Cirebon, Majalengka</strong></span>
                </div>
                <div class="flex items-center gap-2">
                    <i class="fa-solid fa-truck-fast text-brand-500"></i>
                    <span>Melayani Panggilan Ke Rumah Anda</span>
                </div>
            </div>
        </div>
    </section>

    <!-- MAIN CATALOGUE SECTION -->
    <main id="katalog" class="flex-grow max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-12 w-full">
        <!-- Section Header -->
        <div class="flex flex-col md:flex-row md:items-end justify-between mb-8 gap-4">
            <div>
                <span class="text-brand-600 font-bold text-xs uppercase tracking-wider">Katalog Layanan</span>
                <h2 class="text-2xl sm:text-3xl font-extrabold text-slate-900 mt-1">Daftar Jasa Serviceku</h2>
                <p class="text-slate-500 text-sm mt-1">Pilih layanan yang Anda butuhkan dan langsung pesan via WhatsApp.</p>
            </div>

            <!-- Admin Add Button Banner/Service -->
            <div id="admin-actions-bar" class="hidden flex items-center gap-2">
                <button onclick="openAddServiceModal()" class="bg-brand-600 hover:bg-brand-700 text-white text-xs sm:text-sm font-bold px-4 py-2.5 rounded-xl flex items-center gap-2 shadow-md transition-all">
                    <i class="fa-solid fa-plus-circle"></i> Tambah Jasa Baru
                </button>
                <button onclick="openManageBannersModal()" class="bg-amber-600 hover:bg-amber-700 text-white text-xs sm:text-sm font-bold px-4 py-2.5 rounded-xl flex items-center gap-2 shadow-md transition-all">
                    <i class="fa-solid fa-images"></i> Kelola Banner
                </button>
            </div>
        </div>

        <!-- Filter Categories -->
        <div class="flex items-center gap-2 overflow-x-auto pb-4 mb-8 scrollbar-none" id="category-filters">
            <button onclick="filterCategory('semua')" class="filter-btn active bg-brand-600 text-white px-4 py-2 rounded-xl text-xs sm:text-sm font-semibold whitespace-nowrap shadow-sm transition-all">Semua Jasa</button>
            <button onclick="filterCategory('AC')" class="filter-btn bg-white hover:bg-slate-100 text-slate-700 border border-slate-200 px-4 py-2 rounded-xl text-xs sm:text-sm font-semibold whitespace-nowrap transition-all">Service AC</button>
            <button onclick="filterCategory('Kulkas')" class="filter-btn bg-white hover:bg-slate-100 text-slate-700 border border-slate-200 px-4 py-2 rounded-xl text-xs sm:text-sm font-semibold whitespace-nowrap transition-all">Kulkas</button>
            <button onclick="filterCategory('Mesin Cuci')" class="filter-btn bg-white hover:bg-slate-100 text-slate-700 border border-slate-200 px-4 py-2 rounded-xl text-xs sm:text-sm font-semibold whitespace-nowrap transition-all">Mesin Cuci</button>
            <button onclick="filterCategory('Showcase & Freezer')" class="filter-btn bg-white hover:bg-slate-100 text-slate-700 border border-slate-200 px-4 py-2 rounded-xl text-xs sm:text-sm font-semibold whitespace-nowrap transition-all">Showcase / Freezer</button>
            <button onclick="filterCategory('Dispenser')" class="filter-btn bg-white hover:bg-slate-100 text-slate-700 border border-slate-200 px-4 py-2 rounded-xl text-xs sm:text-sm font-semibold whitespace-nowrap transition-all">Dispenser</button>
        </div>

        <!-- Services Grid -->
        <div id="services-grid" class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 xl:grid-cols-4 gap-6">
            <!-- Loading Skeleton -->
            <div class="animate-pulse bg-white rounded-2xl border border-slate-200 p-4 space-y-4">
                <div class="bg-slate-200 h-48 rounded-xl"></div>
                <div class="h-4 bg-slate-200 rounded w-3/4"></div>
                <div class="h-4 bg-slate-200 rounded w-1/2"></div>
            </div>
        </div>
    </main>

    <!-- KEUNGGULAN & COVERAGE SECTION -->
    <section id="keunggulan" class="bg-slate-900 text-white py-16 border-t border-slate-800">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
            <div class="text-center max-w-2xl mx-auto mb-12">
                <span class="text-brand-500 font-bold text-xs uppercase tracking-wider">Mengapa Memilih Kami?</span>
                <h2 class="text-3xl font-extrabold mt-1">Keunggulan Serviceku</h2>
                <p class="text-slate-400 text-sm mt-2">Komitmen kami untuk memberikan hasil terbaik dengan pelayanan jujur dan harga ramah dikantong.</p>
            </div>

            <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-6">
                <div class="bg-slate-800/60 p-6 rounded-2xl border border-slate-700 hover:border-brand-500/50 transition-all">
                    <div class="w-12 h-12 bg-amber-500/10 text-amber-400 rounded-xl flex items-center justify-center text-2xl mb-4">
                        <i class="fa-solid fa-shield-halved"></i>
                    </div>
                    <h3 class="text-lg font-bold">Garansi Pekerjaan</h3>
                    <p class="text-xs text-slate-400 mt-2 leading-relaxed">Garansi resmi hingga 1 bulan untuk kerusakan dan bagian yang sama. Kami tanggap mengatasi keluhan.</p>
                </div>

                <div class="bg-slate-800/60 p-6 rounded-2xl border border-slate-700 hover:border-brand-500/50 transition-all">
                    <div class="w-12 h-12 bg-brand-500/10 text-brand-400 rounded-xl flex items-center justify-center text-2xl mb-4">
                        <i class="fa-solid fa-user-gear"></i>
                    </div>
                    <h3 class="text-lg font-bold">Teknisi Berpengalaman</h3>
                    <p class="text-xs text-slate-400 mt-2 leading-relaxed">Teknisi handal, ramah, jujur dan amanah Siap datang langsung ke tempat tinggal Anda.</p>
                </div>

                <div class="bg-slate-800/60 p-6 rounded-2xl border border-slate-700 hover:border-brand-500/50 transition-all">
                    <div class="w-12 h-12 bg-emerald-500/10 text-emerald-400 rounded-xl flex items-center justify-center text-2xl mb-4">
                        <i class="fa-solid fa-bolt"></i>
                    </div>
                    <h3 class="text-lg font-bold">Cepat & Tepat Waktu</h3>
                    <p class="text-xs text-slate-400 mt-2 leading-relaxed">Proses pengerjaan dilakukan dengan akurat, efisien, cepat dan profesional tanpa menunda waktu.</p>
                </div>

                <div class="bg-slate-800/60 p-6 rounded-2xl border border-slate-700 hover:border-brand-500/50 transition-all">
                    <div class="w-12 h-12 bg-purple-500/10 text-purple-400 rounded-xl flex items-center justify-center text-2xl mb-4">
                        <i class="fa-solid fa-microchip"></i>
                    </div>
                    <h3 class="text-lg font-bold">Sparepart Berkualitas</h3>
                    <p class="text-xs text-slate-400 mt-2 leading-relaxed">Menggunakan komponen & sparepart original bersertifikasi agar elektronik awet tahan lama.</p>
                </div>
            </div>
        </div>
    </section>

    <!-- WILAYAH LAYANAN SECTION -->
    <section id="wilayah" class="py-16 bg-white border-b border-slate-200">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
            <div class="bg-gradient-to-r from-brand-900 to-slate-900 rounded-3xl p-8 sm:p-12 text-white shadow-xl relative overflow-hidden flex flex-col lg:flex-row items-center justify-between gap-8">
                <div class="max-w-2xl relative z-10 space-y-4">
                    <span class="inline-block px-3 py-1 bg-brand-500/20 text-brand-400 rounded-full text-xs font-bold uppercase">Melayani Panggilan</span>
                    <h2 class="text-3xl sm:text-4xl font-extrabold">Jangkauan Wilayah Operasional Kami</h2>
                    <p class="text-slate-300 text-sm leading-relaxed">
                        Kami siap dipanggil untuk kebutuhan perbaikan perangkat elektronik rumah tangga di wilayah:
                    </p>
                    <div class="flex flex-wrap gap-3 pt-2">
                        <span class="px-4 py-2 bg-white/10 rounded-xl text-sm font-bold flex items-center gap-2">
                            <i class="fa-solid fa-map-pin text-amber-400"></i> Indramayu
                        </span>
                        <span class="px-4 py-2 bg-white/10 rounded-xl text-sm font-bold flex items-center gap-2">
                            <i class="fa-solid fa-map-pin text-amber-400"></i> Cirebon
                        </span>
                        <span class="px-4 py-2 bg-white/10 rounded-xl text-sm font-bold flex items-center gap-2">
                            <i class="fa-solid fa-map-pin text-amber-400"></i> Majalengka
                        </span>
                    </div>
                    <p class="text-xs text-slate-400 pt-2"><i class="fa-solid fa-location-arrow text-brand-400"></i> Alamat Bengkel: Jl. Bypass Binaria - Bondan</p>
                </div>

                <div class="relative z-10 flex-shrink-0 text-center lg:text-right bg-white/10 p-6 rounded-2xl backdrop-blur-md border border-white/10">
                    <p class="text-xs text-slate-300 font-semibold uppercase">Butuh Service Hari Ini?</p>
                    <a href="https://wa.me/6287874417978?text=Halo%20Serviceku,%20saya%20butuh%20panggilan%20teknisi%20ke%20lokasi%20saya." target="_blank" rel="noopener noreferrer" class="mt-3 inline-flex items-center gap-2 bg-emerald-500 hover:bg-emerald-600 text-white px-6 py-3.5 rounded-xl font-bold text-base shadow-lg transition-all active:scale-95">
                        <i class="fa-brands fa-whatsapp text-xl"></i>
                        <span>0878-7441-7978</span>
                    </a>
                </div>
            </div>
        </div>
    </section>

    <!-- FOOTER -->
    <footer class="bg-slate-950 text-slate-400 py-12 border-t border-slate-900 text-sm">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 grid grid-cols-1 md:grid-cols-3 gap-8">
            <div class="space-y-3">
                <div class="flex items-center gap-2">
                    <div class="w-8 h-8 rounded-lg bg-brand-600 flex items-center justify-center text-white">
                        <i class="fa-solid fa-screwdriver-wrench"></i>
                    </div>
                    <span class="text-xl font-bold text-white">Serviceku</span>
                </div>
                <p class="text-xs text-slate-400 leading-relaxed">
                    Pusat layanan perbaikan & perawatan unit AC, Kulkas, Mesin Cuci, Showcase, Freezer Box & Dispenser terpercaya di wilayah Indramayu, Cirebon, Majalengka.
                </p>
            </div>

            <div>
                <h4 class="text-white font-bold mb-3">Kontak & Alamat</h4>
                <ul class="space-y-2 text-xs">
                    <li class="flex items-center gap-2"><i class="fa-solid fa-phone text-brand-500"></i> +62 878-7441-7978</li>
                    <li class="flex items-start gap-2"><i class="fa-solid fa-location-dot text-brand-500 mt-1"></i> Jl. bypass Binaria-bondan</li>
                    <li class="flex items-center gap-2"><i class="fa-solid fa-clock text-brand-500"></i> Buka Setiap Hari (08:00 - 18:00 WIB)</li>
                </ul>
            </div>

            <div>
                <h4 class="text-white font-bold mb-3">Garansi Service</h4>
                <p class="text-xs text-slate-400 leading-relaxed">
                    Semua jenis perbaikan mendapatkan jaminan garansi 1 bulan untuk item sparepart & kerusakan yang sama. Hubungi kami jika terdapat kendala pasca pengerjaan.
                </p>
            </div>
        </div>
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 mt-8 pt-6 border-t border-slate-900 text-center text-xs text-slate-600">
            &copy; <span id="year">2026</span> Serviceku. All rights reserved.
        </div>
    </footer>

    <!-- FLOATING WHATSAPP BUTTON -->
    <a href="https://wa.me/6287874417978?text=Halo%20Serviceku,%20saya%20ingin%20tanya%20jasa%20service." target="_blank" rel="noopener noreferrer" class="fixed bottom-6 right-6 z-30 bg-emerald-500 hover:bg-emerald-600 text-white w-14 h-14 rounded-full flex items-center justify-center shadow-2xl hover:scale-110 transition-all duration-300 group">
        <i class="fa-brands fa-whatsapp text-3xl"></i>
        <span class="absolute right-16 bg-slate-900 text-white text-xs font-semibold px-3 py-1.5 rounded-lg opacity-0 group-hover:opacity-100 transition-opacity whitespace-nowrap shadow-md pointer-events-none">
            Chat WhatsApp Now
        </span>
    </a>

    <!-- MODAL 1: ADMIN LOGIN MODAL -->
    <div id="admin-modal" class="fixed inset-0 z-50 bg-black/60 backdrop-blur-sm hidden flex items-center justify-center p-4">
        <div class="bg-white rounded-3xl max-w-md w-full p-6 sm:p-8 shadow-2xl border border-slate-100 relative animate-in fade-in zoom-in duration-200">
            <button onclick="closeAdminModal()" class="absolute top-4 right-4 w-8 h-8 text-slate-400 hover:text-slate-600 rounded-full flex items-center justify-center hover:bg-slate-100 transition-colors">
                <i class="fa-solid fa-xmark text-lg"></i>
            </button>

            <div class="text-center mb-6">
                <div class="w-14 h-14 bg-brand-100 text-brand-600 rounded-2xl flex items-center justify-center text-2xl mx-auto mb-3">
                    <i class="fa-solid fa-lock"></i>
                </div>
                <h3 class="text-xl font-extrabold text-slate-900">Login Administrator</h3>
                <p class="text-xs text-slate-500 mt-1">Masukkan Username dan Password untuk mengelola jasa & banner</p>
            </div>

            <form id="admin-login-form" onsubmit="handleAdminLogin(event)" class="space-y-4">
                <div>
                    <label class="block text-xs font-bold text-slate-700 uppercase mb-1">Username</label>
                    <div class="relative">
                        <i class="fa-solid fa-user absolute left-3.5 top-1/2 -translate-y-1/2 text-slate-400 text-sm"></i>
                        <input type="text" id="admin-username" required placeholder="Masukkan username admin" class="w-full pl-10 pr-4 py-2.5 bg-slate-50 border border-slate-200 rounded-xl text-sm focus:outline-none focus:border-brand-500 focus:bg-white transition-all">
                    </div>
                </div>

                <div>
                    <label class="block text-xs font-bold text-slate-700 uppercase mb-1">Password</label>
                    <div class="relative">
                        <i class="fa-solid fa-key absolute left-3.5 top-1/2 -translate-y-1/2 text-slate-400 text-sm"></i>
                        <input type="password" id="admin-password" required placeholder="Masukkan password" class="w-full pl-10 pr-10 py-2.5 bg-slate-50 border border-slate-200 rounded-xl text-sm focus:outline-none focus:border-brand-500 focus:bg-white transition-all">
                        <!-- Eye Icon Toggle -->
                        <button type="button" onclick="togglePasswordVisibility()" class="absolute right-3 top-1/2 -translate-y-1/2 text-slate-400 hover:text-slate-600">
                            <i id="password-toggle-icon" class="fa-solid fa-eye text-sm"></i>
                        </button>
                    </div>
                </div>

                <button type="submit" class="w-full bg-brand-600 hover:bg-brand-700 text-white font-bold py-3 rounded-xl text-sm shadow-md hover:shadow-lg transition-all active:scale-95">
                    Masuk ke Dashboard
                </button>
            </form>
        </div>
    </div>

    <!-- MODAL 2: ADD / EDIT SERVICE MODAL -->
    <div id="service-modal" class="fixed inset-0 z-50 bg-black/60 backdrop-blur-sm hidden flex items-center justify-center p-4 overflow-y-auto">
        <div class="bg-white rounded-3xl max-w-lg w-full p-6 sm:p-8 shadow-2xl border border-slate-100 relative my-8">
            <button onclick="closeServiceModal()" class="absolute top-4 right-4 w-8 h-8 text-slate-400 hover:text-slate-600 rounded-full flex items-center justify-center hover:bg-slate-100">
                <i class="fa-solid fa-xmark text-lg"></i>
            </button>

            <h3 id="service-modal-title" class="text-xl font-extrabold text-slate-900 mb-4">Tambah Jasa Service Baru</h3>

            <form id="service-form" onsubmit="saveService(event)" class="space-y-4 text-xs sm:text-sm">
                <input type="hidden" id="service-id">

                <div>
                    <label class="block font-bold text-slate-700 mb-1">Nama Jasa / Perbaikan *</label>
                    <input type="text" id="service-title" required placeholder="Contoh: Cuci AC Standard" class="w-full px-3 py-2.5 bg-slate-50 border border-slate-200 rounded-xl focus:outline-none focus:border-brand-500">
                </div>

                <div class="grid grid-cols-2 gap-3">
                    <div>
                        <label class="block font-bold text-slate-700 mb-1">Kategori *</label>
                        <select id="service-category" required class="w-full px-3 py-2.5 bg-slate-50 border border-slate-200 rounded-xl focus:outline-none focus:border-brand-500">
                            <option value="AC">AC</option>
                            <option value="Kulkas">Kulkas</option>
                            <option value="Mesin Cuci">Mesin Cuci</option>
                            <option value="Showcase & Freezer">Showcase & Freezer</option>
                            <option value="Dispenser">Dispenser</option>
                        </select>
                    </div>

                    <div>
                        <label class="block font-bold text-slate-700 mb-1">Harga (Rp) *</label>
                        <input type="text" id="service-price" required placeholder="Contoh: 75.000 atau 750.000" class="w-full px-3 py-2.5 bg-slate-50 border border-slate-200 rounded-xl focus:outline-none focus:border-brand-500">
                    </div>
                </div>

                <div>
                    <label class="block font-bold text-slate-700 mb-1">URL Foto Jasa *</label>
                    <input type="url" id="service-image" required placeholder="https://images.unsplash.com/..." class="w-full px-3 py-2.5 bg-slate-50 border border-slate-200 rounded-xl focus:outline-none focus:border-brand-500">
                    <p class="text-[11px] text-slate-400 mt-1">Gunakan link gambar langsung dari internet / Unsplash.</p>
                </div>

                <div>
                    <label class="block font-bold text-slate-700 mb-1">Deskripsi & Rincian Pengerjaan *</label>
                    <textarea id="service-desc" rows="3" required placeholder="Jelaskan detail garansi, proses service, atau syarat teknis..." class="w-full px-3 py-2.5 bg-slate-50 border border-slate-200 rounded-xl focus:outline-none focus:border-brand-500"></textarea>
                </div>

                <div>
                    <label class="block font-bold text-slate-700 mb-1">Wilayah Layanan</label>
                    <input type="text" id="service-location" value="Indramayu, Cirebon, Majalengka" class="w-full px-3 py-2.5 bg-slate-50 border border-slate-200 rounded-xl focus:outline-none focus:border-brand-500">
                </div>

                <div>
                    <label class="block font-bold text-slate-700 mb-1">Garansi</label>
                    <input type="text" id="service-guarantee" value="Garansi Service 1 Bulan" class="w-full px-3 py-2.5 bg-slate-50 border border-slate-200 rounded-xl focus:outline-none focus:border-brand-500">
                </div>

                <div class="pt-2 flex gap-3">
                    <button type="button" onclick="closeServiceModal()" class="w-1/2 py-2.5 border border-slate-200 rounded-xl font-bold text-slate-600 hover:bg-slate-50">Batal</button>
                    <button type="submit" class="w-1/2 py-2.5 bg-brand-600 hover:bg-brand-700 text-white font-bold rounded-xl shadow-md">Simpan Jasa</button>
                </div>
            </form>
        </div>
    </div>

    <!-- MODAL 3: MANAGE BANNERS MODAL -->
    <div id="banners-modal" class="fixed inset-0 z-50 bg-black/60 backdrop-blur-sm hidden flex items-center justify-center p-4 overflow-y-auto">
        <div class="bg-white rounded-3xl max-w-2xl w-full p-6 sm:p-8 shadow-2xl border border-slate-100 relative my-8">
            <button onclick="closeBannersModal()" class="absolute top-4 right-4 w-8 h-8 text-slate-400 hover:text-slate-600 rounded-full flex items-center justify-center hover:bg-slate-100">
                <i class="fa-solid fa-xmark text-lg"></i>
            </button>

            <h3 class="text-xl font-extrabold text-slate-900 mb-2">Kelola Banner Slide Show</h3>
            <p class="text-xs text-slate-500 mb-6">Tambah atau hapus banner promosi yang tampil di halaman depan.</p>

            <!-- Form Add Banner -->
            <form onsubmit="saveBanner(event)" class="bg-slate-50 p-4 rounded-2xl border border-slate-200 space-y-3 mb-6">
                <h4 class="font-bold text-slate-800 text-xs uppercase">Tambah Banner Baru</h4>
                <div class="grid grid-cols-1 sm:grid-cols-2 gap-3">
                    <input type="text" id="banner-title" required placeholder="Judul Promosi" class="px-3 py-2 bg-white border border-slate-200 rounded-xl text-xs focus:outline-none">
                    <input type="text" id="banner-subtitle" required placeholder="Subjudul / Deskripsi Singkat" class="px-3 py-2 bg-white border border-slate-200 rounded-xl text-xs focus:outline-none">
                </div>
                <div class="grid grid-cols-1 sm:grid-cols-2 gap-3">
                    <select id="banner-theme" class="px-3 py-2 bg-white border border-slate-200 rounded-xl text-xs focus:outline-none">
                        <option value="gradient-banner-1">Tema Biru Navy - Serviceku</option>
                        <option value="gradient-banner-2">Tema Hijau Emerald</option>
                        <option value="gradient-banner-3">Tema Ungu Modern</option>
                    </select>
                    <input type="text" id="banner-badge" placeholder="Badge (Contoh: PROMO SPESIAL)" class="px-3 py-2 bg-white border border-slate-200 rounded-xl text-xs focus:outline-none">
                </div>
                <button type="submit" class="w-full bg-amber-600 hover:bg-amber-700 text-white font-bold py-2 rounded-xl text-xs shadow">
                    + Tambahkan ke Slideshow
                </button>
            </form>

            <!-- Banners List -->
            <div class="space-y-3 max-h-60 overflow-y-auto pr-1" id="admin-banners-list">
                <!-- Injected via JS -->
            </div>
        </div>
    </div>

    <!-- MODAL 4: DETAIL SERVICE MODAL -->
    <div id="detail-modal" class="fixed inset-0 z-50 bg-black/60 backdrop-blur-sm hidden flex items-center justify-center p-4">
        <div class="bg-white rounded-3xl max-w-lg w-full p-6 sm:p-8 shadow-2xl border border-slate-100 relative">
            <button onclick="closeDetailModal()" class="absolute top-4 right-4 w-8 h-8 text-slate-400 hover:text-slate-600 rounded-full flex items-center justify-center hover:bg-slate-100">
                <i class="fa-solid fa-xmark text-lg"></i>
            </button>

            <div id="detail-content">
                <!-- Dynamically filled -->
            </div>
        </div>
    </div>

    <!-- CUSTOM TOAST NOTIFICATION -->
    <div id="toast" class="fixed bottom-6 left-1/2 -translate-x-1/2 z-50 bg-slate-900 text-white px-5 py-3 rounded-2xl shadow-2xl border border-slate-700 text-xs sm:text-sm font-semibold hidden flex items-center gap-3 transition-all duration-300">
        <i id="toast-icon" class="fa-solid fa-circle-check text-emerald-400"></i>
        <span id="toast-message">Pesan sukses disini</span>
    </div>

    <!-- FIREBASE & JS SCRIPT -->
    <script type="module">
        import { initializeApp } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-app.js";
        import { getAuth, signInAnonymously, signInWithCustomToken, onAuthStateChanged } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-auth.js";
        import { getFirestore, collection, doc, setDoc, deleteDoc, onSnapshot } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-firestore.js";

        // Firebase Configuration & System Constants
        const firebaseConfig = typeof __firebase_config !== 'undefined' 
            ? JSON.parse(__firebase_config) 
            : { apiKey: "demo", authDomain: "demo.firebaseapp.com", projectId: "demo-app" };

        const appId = typeof __app_id !== 'undefined' ? __app_id : 'serviceku-app';

        // Initialize Firebase Apps
        const app = initializeApp(firebaseConfig);
        const auth = getAuth(app);
        const db = getFirestore(app);

        // Global Application State
        window.state = {
            currentUser: null,
            isAdmin: false,
            services: [],
            banners: [],
            activeCategory: 'semua',
            currentSlideIndex: 0,
            slideshowInterval: null
        };

        // Standard Initial Services Data from User Requirements
        const INITIAL_SERVICES = [
            {
                id: "srv-1",
                title: "Cuci AC Standard",
                category: "AC",
                price: "75.000",
                image: "https://images.unsplash.com/photo-1621905251189-08b45d6a269e?auto=format&fit=crop&w=600&q=80",
                desc: "Pembersihan komplit unit indoor & outdoor AC. Menghilangkan debu, jamur, bau tak sedap dan mengembalikan kesegaran pendingin ruangan.",
                location: "Indramayu, Cirebon, Majalengka",
                guarantee: "Garansi Service 1 Bulan"
            },
            {
                id: "srv-2",
                title: "Cuci Overhaul Turun Unit AC",
                category: "AC",
                price: "350.000",
                image: "https://images.unsplash.com/photo-1581092160607-ee22621dd758?auto=format&fit=crop&w=600&q=80",
                desc: "Pembersihan total dengan mencopot/turun unit dari dinding. Cocok untuk AC yang tersumbat parah, berlendir, atau berbau menyengat.",
                location: "Indramayu, Cirebon, Majalengka",
                guarantee: "Garansi Service 1 Bulan"
            },
            {
                id: "srv-3",
                title: "Pasang AC Baru / Second",
                category: "AC",
                price: "350.000",
                image: "https://images.unsplash.com/photo-1614633833026-0e10f135b53d?auto=format&fit=crop&w=600&q=80",
                desc: "Pemasangan unit indoor & outdoor rapi, vacum sistem panggunaan pipa presisi agar dingin maksimal dan terhindar bocor freon.",
                location: "Indramayu, Cirebon, Majalengka",
                guarantee: "Garansi Instalasi 1 Bulan"
            },
            {
                id: "srv-4",
                title: "Bongkar AC",
                category: "AC",
                price: "250.000",
                image: "https://images.unsplash.com/photo-1504328345606-18bbc8c9d7d1?auto=format&fit=crop&w=600&q=80",
                desc: "Pelepasan unit AC aman tanpa membuang freon (pump down) untuk pindah lokasi atau renovasi rumah.",
                location: "Indramayu, Cirebon, Majalengka",
                guarantee: "Garansi Pengerjaan Rapi"
            },
            {
                id: "srv-5",
                title: "Perbaikan Kebocoran Freon AC",
                category: "AC",
                price: "750.000",
                image: "https://images.unsplash.com/photo-1621905252507-b35492cc74b4?auto=format&fit=crop&w=600&q=80",
                desc: "Deteksi titik bocor pipa/evaporator, pengelasan kebocoran, pengisian ulang freon R22 / R32 / R410a. Harga disesuaikan tingkat kesulitan.",
                location: "Indramayu, Cirebon, Majalengka",
                guarantee: "Garansi Kebocoran 1 Bulan"
            },
            {
                id: "srv-6",
                title: "Perbaikan Module Control AC",
                category: "AC",
                price: "350.000",
                image: "https://images.unsplash.com/photo-1518770660439-4636190af475?auto=format&fit=crop&w=600&q=80",
                desc: "Perbaikan pcb komputer AC matot, error sensor, atau remote tidak merespon.",
                location: "Indramayu, Cirebon, Majalengka",
                guarantee: "Garansi Service 1 Bulan"
            },
            {
                id: "srv-7",
                title: "Penggantian Module Universal AC",
                category: "AC",
                price: "450.000",
                image: "https://images.unsplash.com/photo-1597733336794-12d05021d510?auto=format&fit=crop&w=600&q=80",
                desc: "Penggantian board PCB dengan module universal berkualitas tinggi lengkap dengan remote baru.",
                location: "Indramayu, Cirebon, Majalengka",
                guarantee: "Garansi Module 1 Bulan"
            },
            {
                id: "srv-8",
                title: "Service Kulkas (2 Pintu & Side By Side)",
                category: "Kulkas",
                price: "150.000 - 350.000",
                image: "https://images.unsplash.com/photo-1584269600464-37b1b58a9fe7?auto=format&fit=crop&w=600&q=80",
                desc: "Perbaikan kulkas kurang dingin, tidak beku, ganti kompresor, kelistrikan defrost, isi freon, atau kebocoran kondensor.",
                location: "Indramayu, Cirebon, Majalengka",
                guarantee: "Garansi Service 1 Bulan"
            },
            {
                id: "srv-9",
                title: "Service Mesin Cuci (Front & Top Loading)",
                category: "Mesin Cuci",
                price: "150.000 - 300.000",
                image: "https://images.unsplash.com/photo-1610557892470-55d9e80c0bce?auto=format&fit=crop&w=600&q=80",
                desc: "Perbaikan mesin cuci tidak berputar, air tidak mengalir/mampet, suara bising, atau pcb kontrol error.",
                location: "Indramayu, Cirebon, Majalengka",
                guarantee: "Garansi Service 1 Bulan"
            },
            {
                id: "srv-10",
                title: "Service Showcase & Freezer Box",
                category: "Showcase & Freezer",
                price: "200.000 - 450.000",
                image: "https://images.unsplash.com/photo-1571175443880-49e1d25b2bc5?auto=format&fit=crop&w=600&q=80",
                desc: "Perbaikan freezer box dan showcase tempat minuman / jualan toko agar kembali dingin maksimal.",
                location: "Indramayu, Cirebon, Majalengka",
                guarantee: "Garansi Service 1 Bulan"
            },
            {
                id: "srv-11",
                title: "Service Dispenser Hot & Cold",
                category: "Dispenser",
                price: "100.000 - 200.000",
                image: "https://images.unsplash.com/photo-1527515637462-cff94eecc1ac?auto=format&fit=crop&w=600&q=80",
                desc: "Perbaikan dispenser tidak dingin, tidak panas, bocor air, atau mati total.",
                location: "Indramayu, Cirebon, Majalengka",
                guarantee: "Garansi Service 1 Bulan"
            }
        ];

        const INITIAL_BANNERS = [
            {
                id: "ban-1",
                title: "JASA SERVICE ELEKTRONIK TERBAIK",
                subtitle: "Melayani Panggilan Ke Rumah Area Indramayu, Cirebon & Majalengka",
                theme: "gradient-banner-1",
                badge: "LAYANAN CEPAT & AMANAH"
            },
            {
                id: "ban-2",
                title: "SERVICE AC & KULKAS BERGARANSI",
                subtitle: "Pengerjaan Tepat Waktu, Teknisi Handal & Garansi Penuh 1 Bulan",
                theme: "gradient-banner-2",
                badge: "GARANSI 1 BULAN"
            },
            {
                id: "ban-3",
                title: "SPAREPART ORIGINAL & HARGA BERSAHABAT",
                subtitle: "Percayakan Kendala Perangkat Rumah Tangga Anda Pada Serviceku",
                theme: "gradient-banner-3",
                badge: "HARGA TERBAIK"
            }
        ];

        // Authenticate Firebase user
        async function initAuth() {
            try {
                if (typeof __initial_auth_token !== 'undefined' && __initial_auth_token) {
                    await signInWithCustomToken(auth, __initial_auth_token);
                } else {
                    await signInAnonymously(auth);
                }
            } catch (err) {
                console.warn("Auth initialization fallback:", err);
            }
        }

        // Initialize Firestore Data Listeners following mandatory paths
        function setupRealtimeListeners() {
            const user = auth.currentUser;
            if (!user) return;

            const servicesRef = collection(db, 'artifacts', appId, 'public', 'data', 'services');
            const bannersRef = collection(db, 'artifacts', appId, 'public', 'data', 'banners');

            // Listen to Services
            onSnapshot(servicesRef, (snapshot) => {
                if (snapshot.empty) {
                    seedInitialData();
                    return;
                }
                const items = [];
                snapshot.forEach((doc) => {
                    items.push({ id: doc.id, ...doc.data() });
                });
                window.state.services = items;
                renderServices();
            }, (error) => {
                console.error("Firestore Services Error:", error);
                if (window.state.services.length === 0) {
                    window.state.services = INITIAL_SERVICES;
                    renderServices();
                }
            });

            // Listen to Banners
            onSnapshot(bannersRef, (snapshot) => {
                if (snapshot.empty) return;
                const bannerItems = [];
                snapshot.forEach((doc) => {
                    bannerItems.push({ id: doc.id, ...doc.data() });
                });
                window.state.banners = bannerItems;
                renderSlideshow();
                renderAdminBannerList();
            }, (error) => {
                console.error("Firestore Banners Error:", error);
                if (window.state.banners.length === 0) {
                    window.state.banners = INITIAL_BANNERS;
                    renderSlideshow();
                    renderAdminBannerList();
                }
            });
        }

        // Seed initial data into Firestore
        async function seedInitialData() {
            const user = auth.currentUser;
            if (!user) return;

            for (const service of INITIAL_SERVICES) {
                const docRef = doc(db, 'artifacts', appId, 'public', 'data', 'services', service.id);
                await setDoc(docRef, service);
            }

            for (const banner of INITIAL_BANNERS) {
                const docRef = doc(db, 'artifacts', appId, 'public', 'data', 'banners', banner.id);
                await setDoc(docRef, banner);
            }
        }

        // Render Services Cards
        function renderServices() {
            const container = document.getElementById('services-grid');
            const category = window.state.activeCategory;

            const filtered = category === 'semua' 
                ? window.state.services 
                : window.state.services.filter(s => s.category.toLowerCase() === category.toLowerCase());

            if (filtered.length === 0) {
                container.innerHTML = `
                    <div class="col-span-full text-center py-12 bg-white rounded-2xl border border-slate-200">
                        <i class="fa-solid fa-box-open text-4xl text-slate-300 mb-3"></i>
                        <p class="text-slate-500 font-semibold">Belum ada data jasa untuk kategori ini.</p>
                    </div>
                `;
                return;
            }

            container.innerHTML = filtered.map(item => `
                <div class="bg-white rounded-2xl border border-slate-200/80 shadow-sm hover:shadow-xl hover:-translate-y-1 transition-all duration-300 flex flex-col overflow-hidden group">
                    <div class="relative h-48 overflow-hidden bg-slate-100">
                        <img src="${item.image}" alt="${item.title}" class="w-full h-full object-cover group-hover:scale-105 transition-transform duration-500" onerror="this.src='https://placehold.co/600x400/0284c7/white?text=Serviceku'">
                        <span class="absolute top-3 left-3 bg-slate-900/80 backdrop-blur-md text-amber-400 text-[10px] font-bold px-2.5 py-1 rounded-lg">
                            ${item.category}
                        </span>
                        ${item.guarantee ? `
                        <span class="absolute top-3 right-3 bg-emerald-600/90 backdrop-blur-md text-white text-[10px] font-bold px-2 py-0.5 rounded-md">
                            ${item.guarantee}
                        </span>` : ''}
                    </div>

                    <div class="p-5 flex flex-col flex-grow justify-between space-y-4">
                        <div>
                            <h3 class="font-bold text-slate-900 text-base group-hover:text-brand-600 transition-colors line-clamp-1">${item.title}</h3>
                            <p class="text-xs text-slate-500 mt-2 line-clamp-2 leading-relaxed">${item.desc}</p>
                        </div>

                        <div class="space-y-3 pt-2 border-t border-slate-100">
                            <div class="flex items-baseline justify-between">
                                <span class="text-[11px] font-semibold text-slate-400">Biaya Service:</span>
                                <span class="text-brand-600 font-extrabold text-base">Rp ${item.price}</span>
                            </div>

                            <div class="text-[11px] text-slate-500 flex items-center gap-1">
                                <i class="fa-solid fa-location-dot text-red-500"></i>
                                <span class="truncate">${item.location || 'Indramayu, Cirebon, Majalengka'}</span>
                            </div>

                            <div class="flex gap-2">
                                <button onclick="openDetailModal('${item.id}')" class="flex-1 py-2 bg-slate-100 hover:bg-slate-200 text-slate-700 font-bold rounded-xl text-xs transition-colors">
                                    Detail
                                </button>
                                <a href="https://wa.me/6287874417978?text=Halo%20Serviceku,%20saya%20ingin%20pesan%20jasa%20*${encodeURIComponent(item.title)}*%20dengan%20estimasi%20biaya%20Rp%20${encodeURIComponent(item.price)}." target="_blank" rel="noopener noreferrer" class="flex-1 py-2 bg-emerald-600 hover:bg-emerald-700 text-white font-bold rounded-xl text-xs flex items-center justify-center gap-1.5 shadow-sm transition-all">
                                    <i class="fa-brands fa-whatsapp text-sm"></i>
                                    <span>Pesan WA</span>
                                </a>
                            </div>

                            ${window.state.isAdmin ? `
                            <div class="flex gap-2 pt-2 border-t border-dashed border-slate-200">
                                <button onclick="openEditServiceModal('${item.id}')" class="flex-1 py-1 bg-amber-100 text-amber-800 font-bold rounded-lg text-[11px] hover:bg-amber-200">
                                    <i class="fa-solid fa-pen"></i> Edit
                                </button>
                                <button onclick="deleteService('${item.id}')" class="flex-1 py-1 bg-red-100 text-red-700 font-bold rounded-lg text-[11px] hover:bg-red-200">
                                    <i class="fa-solid fa-trash"></i> Hapus
                                </button>
                            </div>
                            ` : ''}
                        </div>
                    </div>
                </div>
            `).join('');
        }

        // Render Slideshow Banner
        function renderSlideshow() {
            const wrapper = document.getElementById('slides-wrapper');
            const indicators = document.getElementById('slideshow-indicators');

            const banners = window.state.banners.length > 0 ? window.state.banners : INITIAL_BANNERS;

            wrapper.innerHTML = banners.map((b, idx) => `
                <div class="w-full flex-shrink-0 ${b.theme || 'gradient-banner-1'} py-16 px-6 md:px-16 flex items-center">
                    <div class="max-w-4xl mx-auto text-center md:text-left space-y-4">
                        <span class="inline-block px-3.5 py-1 bg-white/20 backdrop-blur-md rounded-full text-xs font-bold uppercase tracking-wider text-amber-300 border border-white/10">
                            ${b.badge || 'Serviceku Infografis'}
                        </span>
                        <h1 class="text-3xl sm:text-4xl md:text-5xl font-black leading-tight tracking-tight text-white">
                            ${b.title}
                        </h1>
                        <p class="text-slate-200 text-sm md:text-base max-w-2xl leading-relaxed">
                            ${b.subtitle}
                        </p>
                        <div class="pt-2 flex flex-wrap justify-center md:justify-start gap-3">
                            <a href="#katalog" class="bg-white text-slate-900 font-bold px-6 py-3 rounded-xl text-xs sm:text-sm shadow-lg hover:bg-slate-100 transition-all">
                                Lihat Katalog Jasa
                            </a>
                            <a href="https://wa.me/6287874417978?text=Halo%20Serviceku,%20saya%20ingin%20konsultasi." target="_blank" class="bg-emerald-600 hover:bg-emerald-700 text-white font-bold px-6 py-3 rounded-xl text-xs sm:text-sm shadow-lg flex items-center gap-2 transition-all">
                                <i class="fa-brands fa-whatsapp text-lg"></i>
                                <span>Hubungi WA</span>
                            </a>
                        </div>
                    </div>
                </div>
            `).join('');

            indicators.innerHTML = banners.map((_, idx) => `
                <button onclick="goToSlide(${idx})" class="w-2.5 h-2.5 rounded-full transition-all ${idx === window.state.currentSlideIndex ? 'bg-amber-400 w-8' : 'bg-white/50'}"></button>
            `).join('');

            updateSlidePosition();
        }

        function updateSlidePosition() {
            const wrapper = document.getElementById('slides-wrapper');
            const idx = window.state.currentSlideIndex;
            wrapper.style.transform = `translateX(-${idx * 100}%)`;
            renderSlideshowIndicators();
        }

        function renderSlideshowIndicators() {
            const dots = document.querySelectorAll('#slideshow-indicators button');
            dots.forEach((dot, idx) => {
                if (idx === window.state.currentSlideIndex) {
                    dot.className = "w-8 h-2.5 bg-amber-400 rounded-full transition-all";
                } else {
                    dot.className = "w-2.5 h-2.5 bg-white/50 rounded-full transition-all";
                }
            });
        }

        window.nextSlide = function() {
            const banners = window.state.banners.length > 0 ? window.state.banners : INITIAL_BANNERS;
            window.state.currentSlideIndex = (window.state.currentSlideIndex + 1) % banners.length;
            updateSlidePosition();
        }

        window.prevSlide = function() {
            const banners = window.state.banners.length > 0 ? window.state.banners : INITIAL_BANNERS;
            window.state.currentSlideIndex = (window.state.currentSlideIndex - 1 + banners.length) % banners.length;
            updateSlidePosition();
        }

        window.goToSlide = function(index) {
            window.state.currentSlideIndex = index;
            updateSlidePosition();
        }

        // Auto slideshow timer
        function startSlideshowAutoplay() {
            if (window.state.slideshowInterval) clearInterval(window.state.slideshowInterval);
            window.state.slideshowInterval = setInterval(() => {
                window.nextSlide();
            }, 6000);
        }

        // Render Admin Banner Management List
        function renderAdminBannerList() {
            const container = document.getElementById('admin-banners-list');
            const banners = window.state.banners.length > 0 ? window.state.banners : INITIAL_BANNERS;

            container.innerHTML = banners.map(b => `
                <div class="flex items-center justify-between p-3 bg-slate-100 rounded-xl border border-slate-200 text-xs">
                    <div>
                        <p class="font-bold text-slate-800">${b.title}</p>
                        <p class="text-slate-500 text-[11px]">${b.subtitle}</p>
                    </div>
                    <button onclick="deleteBanner('${b.id}')" class="text-red-600 hover:text-red-800 p-2 font-bold">
                        <i class="fa-solid fa-trash"></i>
                    </button>
                </div>
            `).join('');
        }

        // Filter Category Click Handler
        window.filterCategory = function(cat) {
            window.state.activeCategory = cat;
            document.querySelectorAll('.filter-btn').forEach(btn => {
                if (btn.innerText.toLowerCase().includes(cat.toLowerCase()) || (cat === 'semua' && btn.innerText.includes('Semua'))) {
                    btn.className = "filter-btn active bg-brand-600 text-white px-4 py-2 rounded-xl text-xs sm:text-sm font-semibold whitespace-nowrap shadow-sm transition-all";
                } else {
                    btn.className = "filter-btn bg-white hover:bg-slate-100 text-slate-700 border border-slate-200 px-4 py-2 rounded-xl text-xs sm:text-sm font-semibold whitespace-nowrap transition-all";
                }
            });
            renderServices();
        }

        // Admin Auth Handler
        window.handleAdminLogin = function(e) {
            e.preventDefault();
            const user = document.getElementById('admin-username').value.trim();
            const pass = document.getElementById('admin-password').value.trim();

            if (user === 'admin' && pass === 'admin123') {
                window.state.isAdmin = true;
                showToast("Berhasil login sebagai Admin Serviceku!");
                closeAdminModal();

                // Update UI state
                document.getElementById('admin-btn-text').innerText = "Admin (Aktif)";
                document.getElementById('admin-login-btn').className = "inline-flex items-center gap-2 bg-emerald-600 text-white px-4 py-2.5 rounded-xl font-semibold text-sm shadow-sm";
                document.getElementById('admin-actions-bar').classList.remove('hidden');

                renderServices();
                renderAdminBannerList();
            } else {
                showToast("Username atau Password salah!", "error");
            }
        }

        window.togglePasswordVisibility = function() {
            const input = document.getElementById('admin-password');
            const icon = document.getElementById('password-toggle-icon');
            if (input.type === 'password') {
                input.type = 'text';
                icon.className = 'fa-solid fa-eye-slash text-sm';
            } else {
                input.type = 'password';
                icon.className = 'fa-solid fa-eye text-sm';
            }
        }

        // Service Modal Operations
        window.openAddServiceModal = function() {
            document.getElementById('service-modal-title').innerText = "Tambah Jasa Service Baru";
            document.getElementById('service-id').value = "";
            document.getElementById('service-form').reset();
            document.getElementById('service-modal').classList.remove('hidden');
        }

        window.openEditServiceModal = function(id) {
            const service = window.state.services.find(s => s.id === id);
            if (!service) return;

            document.getElementById('service-modal-title').innerText = "Edit Jasa Service";
            document.getElementById('service-id').value = service.id;
            document.getElementById('service-title').value = service.title;
            document.getElementById('service-category').value = service.category;
            document.getElementById('service-price').value = service.price;
            document.getElementById('service-image').value = service.image;
            document.getElementById('service-desc').value = service.desc;
            document.getElementById('service-location').value = service.location || "Indramayu, Cirebon, Majalengka";
            document.getElementById('service-guarantee').value = service.guarantee || "Garansi Service 1 Bulan";

            document.getElementById('service-modal').classList.remove('hidden');
        }

        window.saveService = async function(e) {
            e.preventDefault();
            const user = auth.currentUser;
            if (!user) return;

            const id = document.getElementById('service-id').value || `srv-${Date.now()}`;
            const data = {
                id,
                title: document.getElementById('service-title').value,
                category: document.getElementById('service-category').value,
                price: document.getElementById('service-price').value,
                image: document.getElementById('service-image').value,
                desc: document.getElementById('service-desc').value,
                location: document.getElementById('service-location').value,
                guarantee: document.getElementById('service-guarantee').value
            };

            try {
                const docRef = doc(db, 'artifacts', appId, 'public', 'data', 'services', id);
                await setDoc(docRef, data);
                showToast("Data jasa berhasil dipublikasikan secara permanen!");
                closeServiceModal();
            } catch (err) {
                console.error("Save Service Error:", err);
                showToast("Gagal menyimpan data ke database", "error");
            }
        }

        window.deleteService = async function(id) {
            if (!confirm("Apakah Anda yakin ingin menghapus jasa ini secara permanen?")) return;
            const user = auth.currentUser;
            if (!user) return;

            try {
                const docRef = doc(db, 'artifacts', appId, 'public', 'data', 'services', id);
                await deleteDoc(docRef);
                showToast("Jasa berhasil dihapus.");
            } catch (err) {
                console.error("Delete Service Error:", err);
                showToast("Gagal menghapus data", "error");
            }
        }

        // Banner Modal Operations
        window.openManageBannersModal = function() {
            renderAdminBannerList();
            document.getElementById('banners-modal').classList.remove('hidden');
        }

        window.saveBanner = async function(e) {
            e.preventDefault();
            const user = auth.currentUser;
            if (!user) return;

            const id = `ban-${Date.now()}`;
            const bannerData = {
                id,
                title: document.getElementById('banner-title').value,
                subtitle: document.getElementById('banner-subtitle').value,
                theme: document.getElementById('banner-theme').value,
                badge: document.getElementById('banner-badge').value || "PROMO SERVICE"
            };

            try {
                const docRef = doc(db, 'artifacts', appId, 'public', 'data', 'banners', id);
                await setDoc(docRef, bannerData);
                showToast("Banner slideshow baru berhasil diterbitkan!");
                e.target.reset();
            } catch (err) {
                console.error("Save Banner Error:", err);
                showToast("Gagal menyimpan banner", "error");
            }
        }

        window.deleteBanner = async function(id) {
            const user = auth.currentUser;
            if (!user) return;

            try {
                const docRef = doc(db, 'artifacts', appId, 'public', 'data', 'banners', id);
                await deleteDoc(docRef);
                showToast("Banner berhasil dihapus.");
            } catch (err) {
                console.error("Delete Banner Error:", err);
            }
        }

        // Service Detail Modal View
        window.openDetailModal = function(id) {
            const item = window.state.services.find(s => s.id === id);
            if (!item) return;

            const container = document.getElementById('detail-content');
            container.innerHTML = `
                <div class="space-y-4">
                    <img src="${item.image}" alt="${item.title}" class="w-full h-52 object-cover rounded-2xl shadow-sm">
                    <div>
                        <span class="text-xs font-bold text-brand-600 uppercase bg-brand-50 px-2.5 py-1 rounded-md">${item.category}</span>
                        <h3 class="text-2xl font-extrabold text-slate-900 mt-2">${item.title}</h3>
                        <p class="text-xl font-black text-brand-600 mt-1">Rp ${item.price}</p>
                    </div>

                    <div class="bg-slate-50 p-4 rounded-xl border border-slate-200 text-xs sm:text-sm text-slate-700 leading-relaxed">
                        <p class="font-bold text-slate-900 mb-1">Deskripsi Pengerjaan:</p>
                        ${item.desc}
                    </div>

                    <div class="space-y-2 text-xs">
                        <div class="flex items-center gap-2 text-slate-600">
                            <i class="fa-solid fa-shield text-emerald-600 text-base"></i>
                            <span>${item.guarantee || 'Garansi Service 1 Bulan'}</span>
                        </div>
                        <div class="flex items-center gap-2 text-slate-600">
                            <i class="fa-solid fa-location-dot text-red-500 text-base"></i>
                            <span>Melayani: ${item.location || 'Indramayu, Cirebon, Majalengka'}</span>
                        </div>
                    </div>

                    <a href="https://wa.me/6287874417978?text=Halo%20Serviceku,%20saya%20ingin%20memesan%20jasa%20*${encodeURIComponent(item.title)}*%20dengan%20biaya%20Rp%20${encodeURIComponent(item.price)}." target="_blank" rel="noopener noreferrer" class="w-full bg-emerald-600 hover:bg-emerald-700 text-white font-bold py-3.5 rounded-xl text-center flex items-center justify-center gap-2 text-sm shadow-lg transition-all">
                        <i class="fa-brands fa-whatsapp text-xl"></i>
                        <span>Pesan Jasa via WhatsApp (+62 878-7441-7978)</span>
                    </a>
                </div>
            `;

            document.getElementById('detail-modal').classList.remove('hidden');
        }

        // Modal Closers
        window.closeAdminModal = () => document.getElementById('admin-modal').classList.add('hidden');
        window.openAdminModal = () => document.getElementById('admin-modal').classList.remove('hidden');
        window.closeServiceModal = () => document.getElementById('service-modal').classList.add('hidden');
        window.closeBannersModal = () => document.getElementById('banners-modal').classList.add('hidden');
        window.closeDetailModal = () => document.getElementById('detail-modal').classList.add('hidden');

        // Toast Helper
        function showToast(msg, type = "success") {
            const toast = document.getElementById('toast');
            const icon = document.getElementById('toast-icon');
            const message = document.getElementById('toast-message');

            message.innerText = msg;
            if (type === "error") {
                icon.className = "fa-solid fa-circle-xmark text-red-400 text-lg";
            } else {
                icon.className = "fa-solid fa-circle-check text-emerald-400 text-lg";
            }

            toast.classList.remove('hidden');
            setTimeout(() => {
                toast.classList.add('hidden');
            }, 3500);
        }

        // Initialize App
        window.onload = async function() {
            await initAuth();
            setupRealtimeListeners();
            startSlideshowAutoplay();
        };
    </script>
</body>
</html>
