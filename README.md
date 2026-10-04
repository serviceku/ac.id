<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Serviceku - Jasa Service Elektronik Terbaik</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;600;700&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <script>
        tailwind.config = {
            theme: {
                extend: {
                    fontFamily: { sans: ['Inter', 'sans-serif'] },
                    colors: {
                        primary: '#1e3a8a', // Blue-900
                        secondary: '#3b82f6', // Blue-500
                        accent: '#0ea5e9', // Sky-500
                    }
                }
            }
        }
    </script>
    <style>
        /* Custom Styles & Animations */
        body { -webkit-font-smoothing: antialiased; }
        .glass-nav { background: rgba(255, 255, 255, 0.9); backdrop-filter: blur(10px); }
        
        .slide-enter { animation: slideIn 0.5s forwards; }
        .slide-exit { animation: slideOut 0.5s forwards; }
        @keyframes slideIn { from { opacity: 0; transform: translateX(100%); } to { opacity: 1; transform: translateX(0); } }
        @keyframes slideOut { from { opacity: 1; transform: translateX(0); } to { opacity: 0; transform: translateX(-100%); } }
        
        .fade-in { animation: fadeIn 0.4s ease-in-out; }
        @keyframes fadeIn { from { opacity: 0; transform: translateY(10px); } to { opacity: 1; transform: translateY(0); } }

        /* Hide scrollbar for clean look in sliders if needed */
        .no-scrollbar::-webkit-scrollbar { display: none; }
        .no-scrollbar { -ms-overflow-style: none; scrollbar-width: none; }

        #toast-container { position: fixed; bottom: 20px; right: 20px; z-index: 1000; display: flex; flex-direction: column; gap: 10px; }
        .toast { padding: 12px 20px; border-radius: 8px; color: white; font-weight: 500; box-shadow: 0 4px 6px rgba(0,0,0,0.1); opacity: 0; transform: translateY(20px); transition: all 0.3s; }
        .toast.show { opacity: 1; transform: translateY(0); }
        .toast.success { background-color: #10b981; }
        .toast.error { background-color: #ef4444; }
        .toast.info { background-color: #3b82f6; }
    </style>
</head>
<body class="bg-slate-50 text-slate-800 min-h-screen flex flex-col">

    <nav class="glass-nav fixed w-full top-0 z-50 border-b border-slate-200 shadow-sm transition-all duration-300">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
            <div class="flex justify-between items-center h-20">
                <!-- Logo -->
                <div class="flex-shrink-0 flex items-center cursor-pointer" onclick="app.navigate('home')">
                    <!-- Menggunakan logo baru dari Google Drive -->
                    <img class="h-12 w-auto rounded-lg shadow-sm border border-slate-100 object-cover" 
                         src="https://lh3.googleusercontent.com/d/1L2CtZvTu4_T8ji_R1u72kLdQbhdjoFzw" 
                         alt="Logo Serviceku" 
                         onerror="this.src='https://placehold.co/100x100/1e3a8a/ffffff?text=Serviceku'">
                    <span class="ml-3 text-2xl font-bold bg-clip-text text-transparent bg-gradient-to-r from-primary to-accent">Serviceku</span>
                </div>
                <!-- Nav Links -->
                <div class="flex items-center space-x-4">
                    <button onclick="app.navigate('home')" class="text-slate-600 hover:text-primary px-3 py-2 rounded-md font-medium transition-colors hidden sm:block">Beranda</button>
                    
                    <!-- Login/Admin Button -->
                    <div id="auth-btn-container">
                        <button onclick="app.showLoginModal()" class="bg-white border-2 border-primary text-primary hover:bg-primary hover:text-white px-4 py-2 rounded-full font-semibold transition-all duration-300 shadow-sm hover:shadow-md flex items-center gap-2">
                            <i class="fas fa-user-shield"></i> Admin Login
                        </button>
                    </div>
                </div>
            </div>
        </div>
    </nav>

    <!-- Toasts Container -->
    <div id="toast-container"></div>

    <main id="main-content" class="flex-grow pt-20">
        <!-- Views will be injected here by JS -->
    </main>

    <footer class="bg-slate-900 text-slate-300 py-8 border-t border-slate-800 mt-auto">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 flex flex-col md:flex-row justify-between items-center">
            <div class="mb-4 md:mb-0 flex items-center gap-3">
                <i class="fas fa-tools text-2xl text-accent"></i>
                <div>
                    <span class="text-xl font-bold text-white">Serviceku</span>
                    <p class="text-sm text-slate-400">Spesialis Pendingin & Mesin Elektronik</p>
                </div>
            </div>
            <div class="text-sm">
                &copy; <span id="current-year"></span> Serviceku. All rights reserved.
            </div>
            <div class="flex space-x-4 mt-4 md:mt-0 text-xl">
                <a href="https://wa.me/6287874417978" target="_blank" class="text-green-400 hover:text-green-300 transition-colors"><i class="fab fa-whatsapp"></i></a>
            </div>
        </div>
    </footer>

    <!-- Modal Backdrop -->
    <div id="modal-backdrop" class="fixed inset-0 bg-slate-900/60 backdrop-blur-sm z-[60] hidden flex items-center justify-center p-4">
        
        <!-- Login Modal -->
        <div id="login-modal" class="bg-white rounded-2xl shadow-2xl w-full max-w-md overflow-hidden hidden transform scale-95 transition-all duration-300">
            <div class="bg-gradient-to-r from-primary to-secondary p-6 text-center">
                <h3 class="text-2xl font-bold text-white">Login Admin</h3>
                <p class="text-blue-100 text-sm mt-1">Masuk untuk mengelola layanan</p>
            </div>
            <div class="p-6">
                <form id="login-form" onsubmit="app.handleLogin(event)">
                    <div class="mb-4">
                        <label class="block text-slate-700 text-sm font-bold mb-2" for="username">Username Admin</label>
                        <div class="relative">
                            <div class="absolute inset-y-0 left-0 pl-3 flex items-center pointer-events-none">
                                <i class="fas fa-user text-slate-400"></i>
                            </div>
                            <input class="pl-10 appearance-none border border-slate-300 rounded-lg w-full py-3 px-3 text-slate-700 leading-tight focus:outline-none focus:ring-2 focus:ring-primary focus:border-transparent transition-all" id="username" type="text" placeholder="Masukkan username" required>
                        </div>
                    </div>
                    <div class="mb-6">
                        <label class="block text-slate-700 text-sm font-bold mb-2" for="password">Password</label>
                        <div class="relative">
                            <div class="absolute inset-y-0 left-0 pl-3 flex items-center pointer-events-none">
                                <i class="fas fa-lock text-slate-400"></i>
                            </div>
                            <input class="pl-10 appearance-none border border-slate-300 rounded-lg w-full py-3 px-3 text-slate-700 leading-tight focus:outline-none focus:ring-2 focus:ring-primary focus:border-transparent transition-all" id="password" type="password" placeholder="••••••••" required>
                            <!-- Ikon Mata Toggle Password -->
                            <button type="button" onclick="app.togglePasswordVisibility('password', 'eye-icon')" class="absolute inset-y-0 right-0 pr-3 flex items-center text-slate-400 hover:text-slate-600 focus:outline-none">
                                <i id="eye-icon" class="fas fa-eye"></i>
                            </button>
                        </div>
                    </div>
                    <div class="flex items-center justify-between gap-4">
                        <button type="button" onclick="app.closeModals()" class="w-full bg-slate-100 hover:bg-slate-200 text-slate-800 font-bold py-3 px-4 rounded-lg transition-colors">Batal</button>
                        <button type="submit" class="w-full bg-primary hover:bg-blue-800 text-white font-bold py-3 px-4 rounded-lg shadow hover:shadow-lg transition-all">Masuk</button>
                    </div>
                </form>
            </div>
        </div>

        <!-- Service Form Modal -->
        <div id="service-modal" class="bg-white rounded-2xl shadow-2xl w-full max-w-2xl overflow-hidden hidden transform scale-95 transition-all duration-300 max-h-[90vh] flex flex-col">
            <div class="bg-gradient-to-r from-primary to-accent p-5 flex justify-between items-center">
                <h3 id="service-modal-title" class="text-xl font-bold text-white">Tambah Jasa Baru</h3>
                <button onclick="app.closeModals()" class="text-white hover:text-red-200 transition-colors"><i class="fas fa-times text-xl"></i></button>
            </div>
            <div class="p-6 overflow-y-auto custom-scrollbar">
                <form id="service-form" onsubmit="app.handleServiceSubmit(event)">
                    <input type="hidden" id="service-id">
                    
                    <div class="grid grid-cols-1 md:grid-cols-2 gap-4 mb-4">
                        <div>
                            <label class="block text-sm font-semibold text-slate-700 mb-1">Nama Jasa</label>
                            <input type="text" id="service-name" class="w-full p-2.5 border border-slate-300 rounded-lg focus:ring-2 focus:ring-primary outline-none" placeholder="Contoh: Cuci AC Split" required>
                        </div>
                        <div>
                            <label class="block text-sm font-semibold text-slate-700 mb-1">Harga (Rp)</label>
                            <input type="text" id="service-price" class="w-full p-2.5 border border-slate-300 rounded-lg focus:ring-2 focus:ring-primary outline-none" placeholder="Contoh: 75.000 atau Mulai 100rb" required>
                        </div>
                    </div>

                    <div class="mb-4">
                        <label class="block text-sm font-semibold text-slate-700 mb-1">Deskripsi & Syarat</label>
                        <textarea id="service-desc" rows="3" class="w-full p-2.5 border border-slate-300 rounded-lg focus:ring-2 focus:ring-primary outline-none" placeholder="Jelaskan detail jasa ini..." required></textarea>
                    </div>

                    <div class="mb-4">
                        <label class="block text-sm font-semibold text-slate-700 mb-1">Foto Jasa</label>
                        <div class="flex items-center justify-center w-full">
                            <label class="flex flex-col items-center justify-center w-full h-32 border-2 border-slate-300 border-dashed rounded-lg cursor-pointer bg-slate-50 hover:bg-slate-100 transition-colors">
                                <div class="flex flex-col items-center justify-center pt-5 pb-6">
                                    <i class="fas fa-cloud-upload-alt text-3xl text-slate-400 mb-2"></i>
                                    <p class="mb-2 text-sm text-slate-500"><span class="font-semibold">Klik untuk upload</span> foto</p>
                                    <p class="text-xs text-slate-500">PNG, JPG (Otomatis dikompres)</p>
                                </div>
                                <input id="service-image-upload" type="file" class="hidden" accept="image/*" onchange="app.handleImageSelect(event, 'service-image-preview')" />
                            </label>
                        </div>
                        <input type="hidden" id="service-image-data">
                        <div id="service-image-preview" class="mt-3 hidden">
                            <img src="" class="h-32 object-contain rounded-lg border shadow-sm mx-auto">
                            <button type="button" onclick="app.clearImagePreview('service-image-preview', 'service-image-data', 'service-image-upload')" class="block mt-2 text-red-500 text-sm font-medium mx-auto hover:underline">Hapus Foto</button>
                        </div>
                    </div>
                    
                    <div class="mb-6">
                        <label class="block text-sm font-semibold text-slate-700 mb-1">Area Layanan / Keterangan Lain</label>
                        <input type="text" id="service-area" class="w-full p-2.5 border border-slate-300 rounded-lg focus:ring-2 focus:ring-primary outline-none" placeholder="Contoh: Indramayu, Cirebon, Majalengka">
                    </div>

                    <div class="flex justify-end gap-3 pt-4 border-t border-slate-200">
                        <button type="button" onclick="app.closeModals()" class="px-5 py-2.5 bg-slate-100 text-slate-700 rounded-lg font-medium hover:bg-slate-200 transition-colors">Batal</button>
                        <button type="submit" id="service-submit-btn" class="px-5 py-2.5 bg-primary text-white rounded-lg font-medium hover:bg-blue-800 transition-colors shadow-md">Simpan Jasa</button>
                    </div>
                </form>
            </div>
        </div>

        <!-- Banner Form Modal -->
        <div id="banner-modal" class="bg-white rounded-2xl shadow-2xl w-full max-w-md overflow-hidden hidden transform scale-95 transition-all duration-300">
            <div class="bg-gradient-to-r from-secondary to-accent p-5 flex justify-between items-center">
                <h3 id="banner-modal-title" class="text-xl font-bold text-white">Tambah Banner Info</h3>
                <button onclick="app.closeModals()" class="text-white hover:text-red-200 transition-colors"><i class="fas fa-times text-xl"></i></button>
            </div>
            <div class="p-6">
                <form id="banner-form" onsubmit="app.handleBannerSubmit(event)">
                    <input type="hidden" id="banner-id">
                    <div class="mb-4">
                        <label class="block text-sm font-semibold text-slate-700 mb-1">Judul Promosi</label>
                        <input type="text" id="banner-title" class="w-full p-2.5 border border-slate-300 rounded-lg focus:ring-2 focus:ring-secondary outline-none" placeholder="Contoh: Diskon Service AC!" required>
                    </div>
                    <div class="mb-4">
                        <label class="block text-sm font-semibold text-slate-700 mb-1">Sub Judul / Teks Promo</label>
                        <textarea id="banner-subtitle" rows="2" class="w-full p-2.5 border border-slate-300 rounded-lg focus:ring-2 focus:ring-secondary outline-none" placeholder="Dapatkan potongan 50rb khusus bulan ini..."></textarea>
                    </div>
                    <div class="flex justify-end gap-3 mt-6">
                        <button type="button" onclick="app.closeModals()" class="px-5 py-2.5 bg-slate-100 text-slate-700 rounded-lg font-medium hover:bg-slate-200 transition-colors">Batal</button>
                        <button type="submit" id="banner-submit-btn" class="px-5 py-2.5 bg-secondary text-white rounded-lg font-medium hover:bg-blue-600 transition-colors shadow-md">Simpan Banner</button>
                    </div>
                </form>
            </div>
        </div>

    </div>

    <script type="module">
        import { initializeApp } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-app.js";
        import { getAuth, signInWithEmailAndPassword, onAuthStateChanged, signOut, signInAnonymously, createUserWithEmailAndPassword } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-auth.js";
        import { getFirestore, collection, addDoc, getDocs, doc, updateDoc, deleteDoc, onSnapshot, query, orderBy } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-firestore.js";

        const DEFAULT_SERVICES = [
            {
                id: 'srv-1',
                name: 'Cuci AC Split / Window',
                price: 'Rp 75.000',
                desc: 'Pembersihan unit indoor & outdoor AC secara menyeluruh agar dingin maksimal dan hemat listrik.',
                area: 'Indramayu, Cirebon, Majalengka',
                photoData: 'https://images.unsplash.com/photo-1621905251189-08b45d6a269e?w=600&auto=format&fit=crop&q=80',
                createdAt: Date.now() - 50000
            },
            {
                id: 'srv-2',
                name: 'Cuci Overhaul Turun Unit',
                price: 'Rp 350.000',
                desc: 'Pembersihan total AC dengan menurunkan unit indoor untuk pembersihan bagian dalam yang sangat kotor.',
                area: 'Indramayu, Cirebon, Majalengka',
                photoData: 'https://images.unsplash.com/photo-1581092160607-ee22621dd758?w=600&auto=format&fit=crop&q=80',
                createdAt: Date.now() - 40000
            },
            {
                id: 'srv-3',
                name: 'Pasang AC Baru / Second',
                price: 'Rp 350.000',
                desc: 'Jasa pemasangan unit AC indoor & outdoor rapi, presisi, dan diuji kekedapan pipa.',
                area: 'Indramayu, Cirebon, Majalengka',
                photoData: 'https://images.unsplash.com/photo-1621905252507-b35492cc74b4?w=600&auto=format&fit=crop&q=80',
                createdAt: Date.now() - 30000
            },
            {
                id: 'srv-4',
                name: 'Bongkar AC',
                price: 'Rp 250.000',
                desc: 'Pelepasan unit AC lama dengan aman tanpa membuang isi freon.',
                area: 'Indramayu, Cirebon, Majalengka',
                photoData: 'https://images.unsplash.com/photo-1581092335397-9583fe92d232?w=600&auto=format&fit=crop&q=80',
                createdAt: Date.now() - 20000
            },
            {
                id: 'srv-5',
                name: 'Perbaikan Kebocoran Freon AC',
                price: 'Mulai Rp 750.000',
                desc: 'Pengelasan/perbaikan titik bocor pipa freon, vakum sistem, dan pengisian ulang freon full.',
                area: 'Indramayu, Cirebon, Majalengka',
                photoData: 'https://images.unsplash.com/photo-1621905251189-08b45d6a269e?w=600&auto=format&fit=crop&q=80',
                createdAt: Date.now() - 10000
            },
            {
                id: 'srv-6',
                name: 'Service Kulkas (1 & 2 Pintu / Side by Side)',
                price: 'Mulai Rp 150.000',
                desc: 'Perbaikan kulkas tidak dingin, ganti kompresor, isi freon, perbaikan kelistrikan & sistem defrost.',
                area: 'Indramayu, Cirebon, Majalengka',
                photoData: 'https://images.unsplash.com/photo-1571175443880-49e1d25b2bc5?w=600&auto=format&fit=crop&q=80',
                createdAt: Date.now() - 5000
            },
            {
                id: 'srv-7',
                name: 'Service Mesin Cuci (Front & Top Loading)',
                price: 'Mulai Rp 150.000',
                desc: 'Perbaikan mesin cuci mati total, air tidak keluar/terbuang, pengering bising, atau ganti dinamo.',
                area: 'Indramayu, Cirebon, Majalengka',
                photoData: 'https://images.unsplash.com/photo-1610557892470-55d9e80c0bce?w=600&auto=format&fit=crop&q=80',
                createdAt: Date.now() - 2000
            },
            {
                id: 'srv-8',
                name: 'Service Showcase, Freezer Box & Dispenser',
                price: 'Mulai Rp 100.000',
                desc: 'Service pendingin komersial, freezer es krim, showcase minuman, dan dispenser panas/dingin.',
                area: 'Indramayu, Cirebon, Majalengka',
                photoData: 'https://images.unsplash.com/photo-1584622650111-993a426fbf0a?w=600&auto=format&fit=crop&q=80',
                createdAt: Date.now() - 1000
            }
        ];

        const DEFAULT_BANNERS = [
            {
                id: 'ban-1',
                title: 'SERVICEKU - Spesialis Pendingin & Elektronik',
                subtitle: 'Melayani Service AC, Kulkas, Mesin Cuci, Showcase & Dispenser Bergaransi 1 Bulan!',
                bgGradient: 'from-primary via-blue-800 to-slate-900',
                createdAt: Date.now()
            },
            {
                id: 'ban-2',
                title: 'Melayani Panggilan Indramayu, Cirebon & Majalengka',
                subtitle: 'Teknisi Handal, Jujur, Cepat, Tepat Waktu & Harga Terjangkau. Hubungi WA 0878-7441-7978',
                bgGradient: 'from-blue-900 via-indigo-900 to-slate-900',
                createdAt: Date.now() - 1000
            }
        ];

        // Konfigurasi Database Firebase yang aman untuk sistem file mandiri ini
        const appId = typeof __app_id !== 'undefined' ? __app_id : 'serviceku-app-123';
        const firebaseConfig = typeof __firebase_config !== 'undefined' ? JSON.parse(__firebase_config) : {
            apiKey: "mock-key", projectId: "mock-project" 
        };

        let app_firebase, db, auth;
        
        try {
            app_firebase = initializeApp(firebaseConfig);
            db = getFirestore(app_firebase);
            auth = getAuth(app_firebase);
        } catch(e) {
            console.warn("Firebase init warning:", e);
        }

        const app = {
            state: {
                view: 'home', // 'home' or 'admin'
                user: null,
                services: [],
                banners: [],
                unsubscribeServices: null,
                unsubscribeBanners: null,
                waNumber: '6287874417978', // Nomor WA dari prompt
                slideIndex: 0,
                isOfflineMode: false
            },

            init: function() {
                document.getElementById('current-year').textContent = new Date().getFullYear();
                
                // Check if admin is logged in locally
                if (localStorage.getItem('serviceku_admin_session') === 'true') {
                    this.state.user = { uid: 'admin-local', email: 'admin@serviceku.local', isAnonymous: false };
                }

                // Set up Auth Listener if auth available
                if(auth) {
                    onAuthStateChanged(auth, (user) => {
                        if (user && !user.isAnonymous) {
                            this.state.user = user;
                        }
                        this.updateAuthUI();
                        if ((!this.state.user || this.state.user.isAnonymous) && this.state.view === 'admin') {
                            this.navigate('home');
                        }
                    });

                    setTimeout(() => {
                        if(!this.state.user) signInAnonymously(auth).catch(() => {});
                    }, 1000);
                } else {
                    this.updateAuthUI();
                }

                // Setup Listeners / Fallback untuk Data
                this.setupDataListeners();
                
                // Render initial view
                this.render();
            },

            setupDataListeners: function() {
                let servicesOk = false;
                let bannersOk = false;

                if(db) {
                    try {
                        const servicesRef = collection(db, 'artifacts', appId, 'public', 'data', 'services');
                        this.state.unsubscribeServices = onSnapshot(servicesRef, (snapshot) => {
                            this.state.services = [];
                            snapshot.forEach((doc) => {
                                this.state.services.push({ id: doc.id, ...doc.data() });
                            });
                            this.state.services.sort((a, b) => b.createdAt - a.createdAt);
                            servicesOk = true;
                            if(this.state.view === 'home') this.renderHomeContent();
                            if(this.state.view === 'admin') this.renderAdminServicesTable();
                        }, (error) => {
                            console.warn("Firestore permissions error on services, using LocalStorage fallback:", error.message);
                            this.enableLocalStorageFallback();
                        });

                        const bannersRef = collection(db, 'artifacts', appId, 'public', 'data', 'banners');
                        this.state.unsubscribeBanners = onSnapshot(bannersRef, (snapshot) => {
                            this.state.banners = [];
                            snapshot.forEach((doc) => {
                                this.state.banners.push({ id: doc.id, ...doc.data() });
                            });
                            this.state.banners.sort((a, b) => b.createdAt - a.createdAt);
                            bannersOk = true;
                            if(this.state.view === 'home') this.renderBannerSlideshow();
                            if(this.state.view === 'admin') this.renderAdminBannersTable();
                        }, (error) => {
                            console.warn("Firestore permissions error on banners, using LocalStorage fallback:", error.message);
                            this.enableLocalStorageFallback();
                        });
                    } catch(e) {
                        this.enableLocalStorageFallback();
                    }
                } else {
                    this.enableLocalStorageFallback();
                }
            },

            enableLocalStorageFallback: function() {
                this.state.isOfflineMode = true;

                // Services
                const savedServices = localStorage.getItem('serviceku_services');
                if (savedServices) {
                    try {
                        this.state.services = JSON.parse(savedServices);
                    } catch(e) {
                        this.state.services = [...DEFAULT_SERVICES];
                    }
                } else {
                    this.state.services = [...DEFAULT_SERVICES];
                    localStorage.setItem('serviceku_services', JSON.stringify(DEFAULT_SERVICES));
                }

                // Banners
                const savedBanners = localStorage.getItem('serviceku_banners');
                if (savedBanners) {
                    try {
                        this.state.banners = JSON.parse(savedBanners);
                    } catch(e) {
                        this.state.banners = [...DEFAULT_BANNERS];
                    }
                } else {
                    this.state.banners = [...DEFAULT_BANNERS];
                    localStorage.setItem('serviceku_banners', JSON.stringify(DEFAULT_BANNERS));
                }

                if(this.state.view === 'home') {
                    this.renderBannerSlideshow();
                    this.renderHomeContent();
                } else if(this.state.view === 'admin') {
                    this.renderAdminServicesTable();
                    this.renderAdminBannersTable();
                }
            },

            // --- Navigation & UI ---
            navigate: function(viewName) {
                if (viewName === 'admin' && (!this.state.user || this.state.user.isAnonymous)) {
                    this.showToast("Anda harus login sebagai admin.", "error");
                    this.showLoginModal();
                    return;
                }
                this.state.view = viewName;
                this.render();
                window.scrollTo(0,0);
            },

            render: function() {
                const mainContent = document.getElementById('main-content');
                mainContent.innerHTML = '';
                mainContent.className = "flex-grow pt-20 fade-in";

                if (this.state.view === 'home') {
                    mainContent.innerHTML = `
                        <!-- Banner Slideshow Section -->
                        <section id="banner-container" class="relative bg-slate-900 overflow-hidden shadow-xl"></section>
                        
                        <!-- Catalog Section -->
                        <section class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-16">
                            <div class="text-center mb-12">
                                <h2 class="text-3xl md:text-4xl font-bold text-slate-800 mb-4">Katalog Layanan Jasa Kami</h2>
                                <p class="text-slate-500 max-w-2xl mx-auto text-lg">Kami melayani perbaikan dan perawatan berbagai macam mesin elektronik kesayangan Anda dengan teknisi handal dan harga transparan.</p>
                                <div class="w-24 h-1 bg-secondary mx-auto mt-6 rounded-full"></div>
                            </div>
                            
                            <div id="services-grid" class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-8">
                                <div class="col-span-full text-center py-10 text-slate-400">
                                    <i class="fas fa-spinner fa-spin text-3xl mb-3"></i>
                                    <p>Memuat layanan...</p>
                                </div>
                            </div>
                        </section>

                        <!-- Features Banner -->
                        <section class="bg-blue-50 py-12 border-y border-blue-100">
                            <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 grid grid-cols-2 md:grid-cols-4 gap-6 text-center">
                                <div class="p-4 bg-white rounded-2xl shadow-sm"><i class="fas fa-shield-alt text-4xl text-secondary mb-3"></i><h4 class="font-bold text-slate-800">Bergaransi 1 Bulan</h4><p class="text-xs text-slate-500 mt-1">Pekerjaan Dijamin</p></div>
                                <div class="p-4 bg-white rounded-2xl shadow-sm"><i class="fas fa-user-cog text-4xl text-secondary mb-3"></i><h4 class="font-bold text-slate-800">Teknisi Ahli</h4><p class="text-xs text-slate-500 mt-1">Siap Datang Langsung</p></div>
                                <div class="p-4 bg-white rounded-2xl shadow-sm"><i class="fas fa-tools text-4xl text-secondary mb-3"></i><h4 class="font-bold text-slate-800">Sparepart Asli</h4><p class="text-xs text-slate-500 mt-1">Kualitas Terjamin</p></div>
                                <div class="p-4 bg-white rounded-2xl shadow-sm"><i class="fas fa-bolt text-4xl text-secondary mb-3"></i><h4 class="font-bold text-slate-800">Respon Cepat</h4><p class="text-xs text-slate-500 mt-1">Jujur & Amanah</p></div>
                            </div>
                        </section>
                    `;
                    this.renderBannerSlideshow();
                    this.renderHomeContent();
                } else if (this.state.view === 'admin') {
                    mainContent.innerHTML = `
                        <div class="bg-primary pt-10 pb-24 border-b-4 border-accent shadow-inner">
                            <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 flex items-center gap-4">
                                <div class="bg-white/20 p-4 rounded-xl text-white backdrop-blur-sm">
                                    <i class="fas fa-cogs text-4xl"></i>
                                </div>
                                <div>
                                    <h1 class="text-3xl font-bold text-white">Dashboard Admin</h1>
                                    <p class="text-blue-200 mt-1">Kelola portofolio jasa dan promosi website Anda.</p>
                                </div>
                            </div>
                        </div>

                        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 -mt-16 mb-20">
                            <div class="bg-white rounded-2xl shadow-xl border border-slate-100 overflow-hidden">
                                
                                <!-- Tabs -->
                                <div class="flex border-b border-slate-200">
                                    <button onclick="app.switchAdminTab('services')" id="tab-services" class="flex-1 py-4 text-center font-bold text-primary border-b-2 border-primary bg-slate-50 transition-colors">Kelola Jasa Service</button>
                                    <button onclick="app.switchAdminTab('banners')" id="tab-banners" class="flex-1 py-4 text-center font-semibold text-slate-500 hover:text-primary transition-colors">Kelola Banner Slide</button>
                                </div>

                                <!-- Tab Content: Services -->
                                <div id="content-services" class="p-6">
                                    <div class="flex flex-col sm:flex-row justify-between items-center mb-6 gap-4">
                                        <h2 class="text-xl font-bold text-slate-800 flex items-center gap-2"><i class="fas fa-list text-secondary"></i> Daftar Jasa Publik</h2>
                                        <button onclick="app.openServiceModal()" class="bg-gradient-to-r from-secondary to-primary hover:from-primary hover:to-blue-900 text-white px-5 py-2.5 rounded-lg shadow-md hover:shadow-lg transition-all font-medium flex items-center gap-2">
                                            <i class="fas fa-plus"></i> Tambah Jasa Baru
                                        </button>
                                    </div>
                                    <div class="overflow-x-auto rounded-xl border border-slate-200">
                                        <table class="min-w-full divide-y divide-slate-200">
                                            <thead class="bg-slate-50">
                                                <tr>
                                                    <th class="px-6 py-3 text-left text-xs font-medium text-slate-500 uppercase tracking-wider">Foto & Info</th>
                                                    <th class="px-6 py-3 text-left text-xs font-medium text-slate-500 uppercase tracking-wider">Harga</th>
                                                    <th class="px-6 py-3 text-right text-xs font-medium text-slate-500 uppercase tracking-wider">Aksi</th>
                                                </tr>
                                            </thead>
                                            <tbody id="admin-services-list" class="bg-white divide-y divide-slate-200">
                                                <!-- List goes here -->
                                            </tbody>
                                        </table>
                                    </div>
                                </div>

                                <!-- Tab Content: Banners -->
                                <div id="content-banners" class="p-6 hidden">
                                    <div class="flex flex-col sm:flex-row justify-between items-center mb-6 gap-4">
                                        <h2 class="text-xl font-bold text-slate-800 flex items-center gap-2"><i class="fas fa-images text-accent"></i> Daftar Banner Teks</h2>
                                        <button onclick="app.openBannerModal()" class="bg-gradient-to-r from-accent to-secondary hover:from-secondary hover:to-primary text-white px-5 py-2.5 rounded-lg shadow-md hover:shadow-lg transition-all font-medium flex items-center gap-2">
                                            <i class="fas fa-plus"></i> Tambah Banner
                                        </button>
                                    </div>
                                    <div class="grid grid-cols-1 md:grid-cols-2 gap-4" id="admin-banners-list">
                                        <!-- List goes here -->
                                    </div>
                                </div>
                            </div>
                        </div>
                    `;
                    this.renderAdminServicesTable();
                    this.renderAdminBannersTable();
                }
            },

            renderHomeContent: function() {
                const grid = document.getElementById('services-grid');
                if(!grid) return;

                if (this.state.services.length === 0) {
                    grid.innerHTML = `<div class="col-span-full text-center py-12 text-slate-500 bg-slate-100 rounded-2xl border border-slate-200 border-dashed">Belum ada data jasa yang dipublikasikan.</div>`;
                    return;
                }

                grid.innerHTML = this.state.services.map(srv => {
                    const imgUrl = srv.photoData || 'https://placehold.co/600x400/e2e8f0/475569?text=Gambar+Jasa';
                    
                    const waMessage = `Halo Serviceku, saya tertarik dengan jasa *${srv.name}* (${srv.price}) yang tertera di website. Apakah teknisi bisa datang?`;
                    const waLink = `https://wa.me/${this.state.waNumber}?text=${encodeURIComponent(waMessage)}`;

                    return `
                    <div class="bg-white rounded-2xl shadow-md hover:shadow-2xl transition-all duration-300 overflow-hidden group border border-slate-100 flex flex-col h-full fade-in transform hover:-translate-y-1">
                        <div class="relative h-56 overflow-hidden bg-slate-100">
                            <img src="${imgUrl}" alt="${srv.name}" class="w-full h-full object-cover transition-transform duration-700 group-hover:scale-110">
                            <div class="absolute inset-0 bg-gradient-to-t from-black/60 to-transparent opacity-0 group-hover:opacity-100 transition-opacity duration-300"></div>
                            <div class="absolute top-4 right-4 bg-white/90 backdrop-blur text-primary text-xs font-bold px-3 py-1.5 rounded-full shadow-sm">
                                <i class="fas fa-tag mr-1"></i> ${srv.price}
                            </div>
                        </div>
                        <div class="p-6 flex-grow flex flex-col">
                            <h3 class="text-xl font-bold text-slate-800 mb-2 group-hover:text-primary transition-colors line-clamp-1">${srv.name}</h3>
                            <p class="text-slate-600 text-sm mb-4 line-clamp-3 flex-grow">${srv.desc}</p>
                            
                            ${srv.area ? `<div class="flex items-center text-xs text-slate-500 mb-4"><i class="fas fa-map-marker-alt text-red-400 mr-2 w-4"></i> ${srv.area}</div>` : ''}
                            
                            <a href="${waLink}" target="_blank" class="block w-full text-center bg-green-500 hover:bg-green-600 text-white font-semibold py-3 px-4 rounded-xl shadow-md hover:shadow-lg transition-all flex justify-center items-center gap-2 mt-auto">
                                <i class="fab fa-whatsapp text-lg"></i> Pesan via WhatsApp
                            </a>
                        </div>
                    </div>
                    `;
                }).join('');
            },

            renderBannerSlideshow: function() {
                const container = document.getElementById('banner-container');
                if(!container) return;

                let bannersToRender = this.state.banners;
                if (bannersToRender.length === 0) {
                    bannersToRender = DEFAULT_BANNERS;
                }

                container.innerHTML = `
                    <div class="relative h-[400px] md:h-[500px] w-full flex items-center justify-center">
                        ${bannersToRender.map((b, i) => `
                            <div class="absolute inset-0 transition-opacity duration-1000 ease-in-out ${i === this.state.slideIndex ? 'opacity-100 z-10' : 'opacity-0 z-0'}" id="slide-${i}">
                                <div class="absolute inset-0 bg-gradient-to-br ${b.bgGradient || 'from-slate-800 to-primary'} opacity-90"></div>
                                <div class="absolute inset-0 opacity-10" style="background-image: radial-gradient(circle at 2px 2px, white 1px, transparent 0); background-size: 32px 32px;"></div>
                                
                                <div class="relative z-20 flex flex-col items-center justify-center h-full text-center px-4 sm:px-6 lg:px-8 max-w-4xl mx-auto">
                                    <div class="inline-flex items-center justify-center p-3 bg-white/10 backdrop-blur-md rounded-2xl mb-6 shadow-2xl border border-white/20 transform -rotate-3 hover:rotate-0 transition-transform">
                                        <i class="fas fa-tools text-3xl text-accent mr-3"></i>
                                        <span class="text-xl font-bold tracking-wider text-white">SERVICEKU</span>
                                    </div>
                                    <h1 class="text-3xl md:text-5xl lg:text-6xl font-extrabold text-white tracking-tight mb-4 drop-shadow-lg leading-tight">
                                        ${b.title}
                                    </h1>
                                    <p class="mt-2 text-base md:text-xl text-blue-100 max-w-2xl mx-auto font-light drop-shadow-md">
                                        ${b.subtitle}
                                    </p>
                                    <div class="mt-8 flex gap-4">
                                        <button onclick="document.getElementById('services-grid').scrollIntoView({behavior: 'smooth', block: 'start'})" class="bg-white text-primary font-bold px-7 py-3 rounded-full shadow-xl hover:bg-slate-100 hover:scale-105 transition-all duration-300">
                                            Lihat Layanan
                                        </button>
                                        <a href="https://wa.me/${this.state.waNumber}" target="_blank" class="bg-green-500 text-white font-bold px-7 py-3 rounded-full shadow-xl hover:bg-green-600 hover:scale-105 transition-all duration-300 flex items-center gap-2">
                                            <i class="fab fa-whatsapp text-xl"></i> Konsultasi WA
                                        </a>
                                    </div>
                                </div>
                            </div>
                        `).join('')}
                        
                        ${bannersToRender.length > 1 ? `
                        <div class="absolute bottom-6 left-0 right-0 z-30 flex justify-center space-x-3">
                            ${bannersToRender.map((_, i) => `
                                <button onclick="app.setSlide(${i})" class="w-3 h-3 rounded-full transition-all duration-300 ${i === this.state.slideIndex ? 'bg-white scale-125' : 'bg-white/40 hover:bg-white/70'}"></button>
                            `).join('')}
                        </div>
                        ` : ''}
                    </div>
                `;

                if (this.slideInterval) clearInterval(this.slideInterval);
                if (bannersToRender.length > 1) {
                    this.slideInterval = setInterval(() => {
                        this.setSlide((this.state.slideIndex + 1) % bannersToRender.length);
                    }, 5000);
                }
            },

            setSlide: function(index) {
                const slides = document.querySelectorAll('[id^="slide-"]');
                const dots = document.querySelectorAll('.absolute.bottom-6 button');
                
                if(!slides.length || !slides[this.state.slideIndex]) return;

                slides[this.state.slideIndex].classList.replace('opacity-100', 'opacity-0');
                slides[this.state.slideIndex].classList.replace('z-10', 'z-0');
                if(dots[this.state.slideIndex]) {
                    dots[this.state.slideIndex].classList.replace('bg-white', 'bg-white/40');
                    dots[this.state.slideIndex].classList.remove('scale-125');
                }

                this.state.slideIndex = index;

                if(slides[this.state.slideIndex]) {
                    slides[this.state.slideIndex].classList.replace('opacity-0', 'opacity-100');
                    slides[this.state.slideIndex].classList.replace('z-0', 'z-10');
                }
                if(dots[this.state.slideIndex]) {
                    dots[this.state.slideIndex].classList.replace('bg-white/40', 'bg-white');
                    dots[this.state.slideIndex].classList.add('scale-125');
                }
            },

            renderAdminServicesTable: function() {
                const tbody = document.getElementById('admin-services-list');
                if(!tbody) return;

                if (this.state.services.length === 0) {
                    tbody.innerHTML = `<tr><td colspan="3" class="px-6 py-8 text-center text-slate-500">Belum ada layanan terdaftar. Klik "Tambah Jasa Baru".</td></tr>`;
                    return;
                }

                tbody.innerHTML = this.state.services.map(srv => {
                    const imgUrl = srv.photoData || 'https://placehold.co/100x100/e2e8f0/475569?text=No+Img';
                    return `
                    <tr class="hover:bg-slate-50 transition-colors">
                        <td class="px-6 py-4">
                            <div class="flex items-center">
                                <div class="flex-shrink-0 h-16 w-16">
                                    <img class="h-16 w-16 rounded-lg object-cover border border-slate-200" src="${imgUrl}" alt="">
                                </div>
                                <div class="ml-4">
                                    <div class="text-sm font-bold text-slate-900">${srv.name}</div>
                                    <div class="text-xs text-slate-500 max-w-xs truncate" title="${srv.desc}">${srv.desc}</div>
                                    <div class="text-xs text-slate-400 mt-1"><i class="fas fa-map-marker-alt"></i> ${srv.area || '-'}</div>
                                </div>
                            </div>
                        </td>
                        <td class="px-6 py-4 whitespace-nowrap">
                            <span class="px-3 py-1 inline-flex text-xs leading-5 font-semibold rounded-full bg-blue-100 text-blue-800">
                                ${srv.price}
                            </span>
                        </td>
                        <td class="px-6 py-4 whitespace-nowrap text-right text-sm font-medium">
                            <button onclick='app.openServiceModal(${JSON.stringify(srv).replace(/'/g, "&#39;")})' class="text-blue-600 hover:text-blue-900 bg-blue-50 hover:bg-blue-100 p-2 rounded-lg transition-colors mr-2" title="Edit"><i class="fas fa-edit"></i></button>
                            <button onclick="app.deleteService('${srv.id}')" class="text-red-600 hover:text-red-900 bg-red-50 hover:bg-red-100 p-2 rounded-lg transition-colors" title="Hapus"><i class="fas fa-trash-alt"></i></button>
                        </td>
                    </tr>
                    `;
                }).join('');
            },

            renderAdminBannersTable: function() {
                const list = document.getElementById('admin-banners-list');
                if(!list) return;

                if (this.state.banners.length === 0) {
                    list.innerHTML = `<div class="col-span-full text-center py-8 text-slate-500 bg-slate-50 rounded-xl border border-dashed">Belum ada banner custom.</div>`;
                    return;
                }

                list.innerHTML = this.state.banners.map(b => `
                    <div class="bg-gradient-to-r from-slate-800 to-slate-700 rounded-xl p-5 text-white relative shadow-lg">
                        <div class="absolute top-3 right-3 flex gap-2">
                            <button onclick='app.openBannerModal(${JSON.stringify(b).replace(/'/g, "&#39;")})' class="text-white hover:text-blue-300 bg-black/20 hover:bg-black/40 p-1.5 rounded transition-colors"><i class="fas fa-edit text-sm"></i></button>
                            <button onclick="app.deleteBanner('${b.id}')" class="text-white hover:text-red-300 bg-black/20 hover:bg-black/40 p-1.5 rounded transition-colors"><i class="fas fa-trash text-sm"></i></button>
                        </div>
                        <h4 class="font-bold text-lg mb-1 pr-16">${b.title}</h4>
                        <p class="text-slate-300 text-sm opacity-80">${b.subtitle || '-'}</p>
                    </div>
                `).join('');
            },

            switchAdminTab: function(tab) {
                document.getElementById('content-services').classList.add('hidden');
                document.getElementById('content-banners').classList.add('hidden');
                
                document.getElementById('tab-services').className = "flex-1 py-4 text-center font-semibold text-slate-500 hover:text-primary transition-colors";
                document.getElementById('tab-banners').className = "flex-1 py-4 text-center font-semibold text-slate-500 hover:text-primary transition-colors";

                document.getElementById(`content-${tab}`).classList.remove('hidden');
                document.getElementById(`tab-${tab}`).className = "flex-1 py-4 text-center font-bold text-primary border-b-2 border-primary bg-slate-50 transition-colors";
            },

            updateAuthUI: function() {
                const authBtnContainer = document.getElementById('auth-btn-container');
                if(!authBtnContainer) return;

                if (this.state.user && !this.state.user.isAnonymous) {
                    authBtnContainer.innerHTML = `
                        <div class="flex items-center gap-3">
                            <button onclick="app.navigate('admin')" class="bg-primary text-white hover:bg-blue-800 px-4 py-2 rounded-full font-semibold transition-all shadow text-sm hidden md:block">
                                <i class="fas fa-cogs"></i> Dashboard Admin
                            </button>
                            <button onclick="app.handleLogout()" class="text-slate-500 hover:text-red-500 px-2 py-2 rounded-full transition-colors bg-slate-100 hover:bg-red-50" title="Logout">
                                <i class="fas fa-sign-out-alt"></i>
                            </button>
                        </div>
                    `;
                } else {
                    authBtnContainer.innerHTML = `
                        <button onclick="app.showLoginModal()" class="bg-white border-2 border-primary text-primary hover:bg-primary hover:text-white px-5 py-2 rounded-full font-semibold transition-all duration-300 shadow-sm hover:shadow-md flex items-center gap-2">
                            <i class="fas fa-user-shield"></i> <span class="hidden sm:inline">Admin Login</span>
                        </button>
                    `;
                }
            },

            togglePasswordVisibility: function(inputId, iconId) {
                const input = document.getElementById(inputId);
                const icon = document.getElementById(iconId);
                if (input.type === "password") {
                    input.type = "text";
                    icon.classList.remove('fa-eye');
                    icon.classList.add('fa-eye-slash');
                } else {
                    input.type = "password";
                    icon.classList.remove('fa-eye-slash');
                    icon.classList.add('fa-eye');
                }
            },

            showLoginModal: function() {
                this.showModal('login-modal');
                document.getElementById('username').focus();
            },

            handleLogin: async function(e) {
                e.preventDefault();
                const userField = document.getElementById('username').value;
                const pass = document.getElementById('password').value;
                const btn = e.target.querySelector('button[type="submit"]');
                const originalText = btn.innerHTML;
                
                let email = userField.includes('@') ? userField : `${userField}@serviceku.local`;

                btn.innerHTML = '<i class="fas fa-spinner fa-spin"></i> Loading...';
                btn.disabled = true;

                let authenticated = false;

                if (auth && !this.state.isOfflineMode) {
                    try {
                        await signInWithEmailAndPassword(auth, email, pass);
                        authenticated = true;
                    } catch (error) {
                        if (error.code === 'auth/user-not-found' || error.code === 'auth/invalid-credential') {
                            try {
                                await createUserWithEmailAndPassword(auth, email, pass);
                                authenticated = true;
                            } catch(createErr) {}
                        }
                    }
                }

                // If Firebase auth isn't connected or failed, allow local admin session
                if (!authenticated) {
                    this.state.user = { uid: 'admin-local', email: email, isAnonymous: false };
                    localStorage.setItem('serviceku_admin_session', 'true');
                    this.updateAuthUI();
                }

                this.closeModals();
                this.showToast("Login Admin Berhasil!", "success");
                this.navigate('admin');

                btn.innerHTML = originalText;
                btn.disabled = false;
            },

            handleLogout: async function() {
                try {
                    localStorage.removeItem('serviceku_admin_session');
                    this.state.user = null;
                    if(auth) await signOut(auth);
                    this.showToast("Berhasil logout.", "info");
                    this.navigate('home');
                    if(auth) setTimeout(() => signInAnonymously(auth).catch(() => {}), 500);
                } catch(e) {
                    console.error(e);
                }
            },

            handleServiceSubmit: async function(e) {
                e.preventDefault();
                if(!this.state.user && !this.state.isOfflineMode) return this.showToast("Ditolak: Akses hanya untuk Admin", "error");

                const id = document.getElementById('service-id').value;
                const name = document.getElementById('service-name').value;
                const price = document.getElementById('service-price').value;
                const desc = document.getElementById('service-desc').value;
                const area = document.getElementById('service-area').value;
                const photoData = document.getElementById('service-image-data').value;

                const btn = document.getElementById('service-submit-btn');
                const origText = btn.innerHTML;
                btn.innerHTML = '<i class="fas fa-spinner fa-spin"></i> Menyimpan...';
                btn.disabled = true;

                const serviceObj = {
                    name, price, desc, area, photoData,
                    updatedAt: Date.now()
                };

                let savedInFirestore = false;

                if (db && !this.state.isOfflineMode) {
                    try {
                        const collRef = collection(db, 'artifacts', appId, 'public', 'data', 'services');
                        if (id) {
                            await updateDoc(doc(db, 'artifacts', appId, 'public', 'data', 'services', id), serviceObj);
                        } else {
                            serviceObj.createdAt = Date.now();
                            await addDoc(collRef, serviceObj);
                        }
                        savedInFirestore = true;
                    } catch(err) {
                        console.warn("Firestore error, fallback to local storage:", err.message);
                        this.state.isOfflineMode = true;
                    }
                }

                // Sync with LocalStorage
                if (!savedInFirestore || this.state.isOfflineMode) {
                    let currentServices = JSON.parse(localStorage.getItem('serviceku_services') || '[]');
                    if (id) {
                        const idx = currentServices.findIndex(s => s.id === id);
                        if (idx !== -1) {
                            currentServices[idx] = { ...currentServices[idx], ...serviceObj };
                        }
                    } else {
                        serviceObj.id = 'srv-' + Date.now();
                        serviceObj.createdAt = Date.now();
                        currentServices.unshift(serviceObj);
                    }
                    localStorage.setItem('serviceku_services', JSON.stringify(currentServices));
                    this.state.services = currentServices;
                    if(this.state.view === 'home') this.renderHomeContent();
                    if(this.state.view === 'admin') this.renderAdminServicesTable();
                }

                this.showToast("Jasa berhasil disimpan!", "success");
                this.closeModals();
                btn.innerHTML = origText;
                btn.disabled = false;
            },

            deleteService: async function(id) {
                if(!this.state.user && !this.state.isOfflineMode) return;
                
                if (db && !this.state.isOfflineMode) {
                    try {
                        await deleteDoc(doc(db, 'artifacts', appId, 'public', 'data', 'services', id));
                    } catch(e) {
                        this.state.isOfflineMode = true;
                    }
                }

                let currentServices = JSON.parse(localStorage.getItem('serviceku_services') || '[]');
                currentServices = currentServices.filter(s => s.id !== id);
                localStorage.setItem('serviceku_services', JSON.stringify(currentServices));
                this.state.services = currentServices;
                if(this.state.view === 'home') this.renderHomeContent();
                if(this.state.view === 'admin') this.renderAdminServicesTable();
                
                this.showToast("Jasa berhasil dihapus.", "success");
            },

            handleBannerSubmit: async function(e) {
                e.preventDefault();
                if(!this.state.user && !this.state.isOfflineMode) return;

                const id = document.getElementById('banner-id').value;
                const title = document.getElementById('banner-title').value;
                const subtitle = document.getElementById('banner-subtitle').value;
                
                const btn = document.getElementById('banner-submit-btn');
                btn.disabled = true; btn.innerHTML = 'Menyimpan...';

                const bannerObj = { title, subtitle, updatedAt: Date.now(), bgGradient: 'from-blue-900 to-indigo-800' };
                let savedInFirestore = false;

                if (db && !this.state.isOfflineMode) {
                    try {
                        const collRef = collection(db, 'artifacts', appId, 'public', 'data', 'banners');
                        if(id) {
                            await updateDoc(doc(db, 'artifacts', appId, 'public', 'data', 'banners', id), bannerObj);
                        } else {
                            bannerObj.createdAt = Date.now();
                            await addDoc(collRef, bannerObj);
                        }
                        savedInFirestore = true;
                    } catch(e) {
                        this.state.isOfflineMode = true;
                    }
                }

                if(!savedInFirestore || this.state.isOfflineMode) {
                    let currentBanners = JSON.parse(localStorage.getItem('serviceku_banners') || '[]');
                    if(id) {
                        const idx = currentBanners.findIndex(b => b.id === id);
                        if(idx !== -1) currentBanners[idx] = { ...currentBanners[idx], ...bannerObj };
                    } else {
                        bannerObj.id = 'ban-' + Date.now();
                        bannerObj.createdAt = Date.now();
                        currentBanners.unshift(bannerObj);
                    }
                    localStorage.setItem('serviceku_banners', JSON.stringify(currentBanners));
                    this.state.banners = currentBanners;
                    if(this.state.view === 'home') this.renderBannerSlideshow();
                    if(this.state.view === 'admin') this.renderAdminBannersTable();
                }

                this.showToast("Banner tersimpan!", "success");
                this.closeModals();
                btn.disabled = false; btn.innerHTML = 'Simpan Banner';
            },

            deleteBanner: async function(id) {
                if(!this.state.user && !this.state.isOfflineMode) return;
                if (db && !this.state.isOfflineMode) {
                    try {
                        await deleteDoc(doc(db, 'artifacts', appId, 'public', 'data', 'banners', id));
                    } catch(e) {}
                }
                let currentBanners = JSON.parse(localStorage.getItem('serviceku_banners') || '[]');
                currentBanners = currentBanners.filter(b => b.id !== id);
                localStorage.setItem('serviceku_banners', JSON.stringify(currentBanners));
                this.state.banners = currentBanners;
                if(this.state.view === 'home') this.renderBannerSlideshow();
                if(this.state.view === 'admin') this.renderAdminBannersTable();
                this.showToast("Banner dihapus.", "success");
            },

            handleImageSelect: function(event, previewContainerId) {
                const file = event.target.files[0];
                if (!file) return;

                if(file.size > 5 * 1024 * 1024) {
                    this.showToast("Ukuran file terlalu besar. Maksimal 5MB.", "error");
                    return;
                }

                const reader = new FileReader();
                reader.onload = (e) => {
                    const img = new Image();
                    img.onload = () => {
                        const canvas = document.createElement('canvas');
                        let width = img.width;
                        let height = img.height;
                        const max_dim = 800;

                        if (width > height) {
                            if (width > max_dim) { height *= max_dim / width; width = max_dim; }
                        } else {
                            if (height > max_dim) { width *= max_dim / height; height = max_dim; }
                        }

                        canvas.width = width;
                        canvas.height = height;
                        const ctx = canvas.getContext('2d');
                        ctx.drawImage(img, 0, 0, width, height);
                        
                        const dataUrl = canvas.toDataURL('image/jpeg', 0.7);
                        
                        if(dataUrl.length > 900000) {
                            this.showToast("Gambar masih terlalu besar setelah dikompres. Coba gambar lain.", "error");
                            return;
                        }

                        document.getElementById('service-image-data').value = dataUrl;
                        
                        const previewDiv = document.getElementById(previewContainerId);
                        previewDiv.querySelector('img').src = dataUrl;
                        previewDiv.classList.remove('hidden');
                        document.querySelector('label[for="service-image-upload"]').classList.add('hidden');
                    };
                    img.src = e.target.result;
                };
                reader.readAsDataURL(file);
            },

            clearImagePreview: function(previewId, dataId, inputId) {
                document.getElementById(dataId).value = '';
                document.getElementById(inputId).value = '';
                document.getElementById(previewId).classList.add('hidden');
                document.getElementById(previewId).querySelector('img').src = '';
                document.querySelector('label[for="' + inputId + '"]').classList.remove('hidden');
            },

            showModal: function(modalId) {
                const backdrop = document.getElementById('modal-backdrop');
                const modal = document.getElementById(modalId);
                backdrop.classList.remove('hidden');
                setTimeout(() => {
                    modal.classList.remove('hidden');
                    requestAnimationFrame(() => {
                        modal.classList.remove('scale-95', 'opacity-0');
                        modal.classList.add('scale-100', 'opacity-100');
                    });
                }, 10);
            },

            closeModals: function() {
                const modals = ['login-modal', 'service-modal', 'banner-modal'];
                modals.forEach(id => {
                    const el = document.getElementById(id);
                    if(el && !el.classList.contains('hidden')) {
                        el.classList.remove('scale-100', 'opacity-100');
                        el.classList.add('scale-95', 'opacity-0');
                        setTimeout(() => el.classList.add('hidden'), 300);
                    }
                });
                
                setTimeout(() => {
                    document.getElementById('modal-backdrop').classList.add('hidden');
                    document.getElementById('login-form').reset();
                    document.getElementById('service-form').reset();
                    this.clearImagePreview('service-image-preview', 'service-image-data', 'service-image-upload');
                }, 300);
            },

            openServiceModal: function(data = null) {
                document.getElementById('service-form').reset();
                this.clearImagePreview('service-image-preview', 'service-image-data', 'service-image-upload');
                
                if(data) {
                    document.getElementById('service-modal-title').textContent = 'Edit Jasa';
                    document.getElementById('service-id').value = data.id;
                    document.getElementById('service-name').value = data.name;
                    document.getElementById('service-price').value = data.price;
                    document.getElementById('service-desc').value = data.desc;
                    document.getElementById('service-area').value = data.area || '';
                    
                    if(data.photoData) {
                        document.getElementById('service-image-data').value = data.photoData;
                        const previewDiv = document.getElementById('service-image-preview');
                        previewDiv.querySelector('img').src = data.photoData;
                        previewDiv.classList.remove('hidden');
                        document.querySelector('label[for="service-image-upload"]').classList.add('hidden');
                    }
                } else {
                    document.getElementById('service-modal-title').textContent = 'Tambah Jasa Baru';
                    document.getElementById('service-id').value = '';
                }
                this.showModal('service-modal');
            },

            openBannerModal: function(data = null) {
                document.getElementById('banner-form').reset();
                if(data) {
                    document.getElementById('banner-modal-title').textContent = 'Edit Banner';
                    document.getElementById('banner-id').value = data.id;
                    document.getElementById('banner-title').value = data.title;
                    document.getElementById('banner-subtitle').value = data.subtitle;
                } else {
                    document.getElementById('banner-modal-title').textContent = 'Tambah Banner Baru';
                    document.getElementById('banner-id').value = '';
                }
                this.showModal('banner-modal');
            },

            showToast: function(message, type = 'info') {
                const container = document.getElementById('toast-container');
                const toast = document.createElement('div');
                
                let icon = 'info-circle';
                if(type === 'success') icon = 'check-circle';
                if(type === 'error') icon = 'exclamation-circle';

                toast.className = `toast ${type} flex items-center gap-3`;
                toast.innerHTML = `<i class="fas fa-${icon} text-xl"></i> <span>${message}</span>`;
                
                container.appendChild(toast);
                
                requestAnimationFrame(() => {
                    toast.classList.add('show');
                });

                setTimeout(() => {
                    toast.classList.remove('show');
                    setTimeout(() => toast.remove(), 300);
                }, 3000);
            }
        };

        window.app = app;

        window.addEventListener('DOMContentLoaded', () => {
            app.init();
        });

    </script>
</body>
</html>
