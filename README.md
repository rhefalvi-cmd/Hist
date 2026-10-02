<!DOCTYPE html>
<html lang="id" class="scroll-smooth">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>EsHist - Eksplorasi Sejarah Pergerakan Nasional Indonesia</title>
    <!-- Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- Google Fonts -->
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Merriweather:ital,wght@0,400;0,700;1,400&family=Plus+Jakarta+Sans:wght@400;500;600;700;800&display=swap" rel="stylesheet">
    <!-- FontAwesome Icons -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    
    <script>
        tailwind.config = {
            theme: {
                extend: {
                    colors: {
                        brand: {
                            red: '#991B1B',      /* Crimson Batik */
                            darkred: '#7F1D1D',
                            gold: '#D97706',     /* Historical Gold */
                            lightgold: '#FBBF24',
                            cream: '#FEF3C7',    /* Vintage Cream */
                            paper: '#FAF5EF',    /* Vintage Paper Background */
                            dark: '#1E1B18',     /* Deep Slate Ink */
                            card: '#FFFFFF'
                        }
                    },
                    fontFamily: {
                        sans: ['"Plus Jakarta Sans"', 'sans-serif'],
                        serif: ['Merriweather', 'serif']
                    }
                }
            }
        }
    </script>

    <style>
        body {
            background-color: #F8F5F0;
            color: #1E1B18;
            font-family: 'Plus Jakarta Sans', sans-serif;
            overflow-x: hidden;
        }

        .hero-pattern {
            background-color: #851818;
            background-image: radial-gradient(#d97706 0.75px, transparent 0.75px), radial-gradient(#d97706 0.75px, #851818 0.75px);
            background-size: 30px 30px;
            background-position: 0 0, 15px 15px;
            opacity: 0.98;
        }

        .view-section {
            display: none;
            opacity: 0;
            transform: translateY(12px);
            transition: opacity 0.35s ease-out, transform 0.35s ease-out;
        }

        .view-section.active {
            display: block;
            opacity: 1;
            transform: translateY(0);
        }

        .custom-scrollbar::-webkit-scrollbar {
            width: 6px;
            height: 6px;
        }
        .custom-scrollbar::-webkit-scrollbar-track {
            background: #F1EAD9;
            border-radius: 4px;
        }
        .custom-scrollbar::-webkit-scrollbar-thumb {
            background: #D97706;
            border-radius: 4px;
        }

        /* Timeline Connector Styling */
        .timeline-line::before {
            content: '';
            position: absolute;
            top: 24px;
            bottom: 24px;
            left: 50%;
            width: 4px;
            background: #D97706;
            transform: translateX(-50%);
            z-index: 0;
        }

        @media (max-width: 768px) {
            .timeline-line::before {
                left: 28px;
            }
        }

        /* Memory Card Game Styling */
        .perspective-1000 {
            perspective: 1000px;
        }
        .transform-style-3d {
            transform-style: preserve-3d;
            transition: transform 0.5s ease-in-out;
        }
        .backface-hidden {
            backface-visibility: hidden;
            -webkit-backface-visibility: hidden;
        }
        .rotate-y-180 {
            transform: rotateY(180deg);
        }
    </style>
</head>
<body class="min-h-screen flex flex-col justify-between selection:bg-brand-gold selection:text-white">

    <header class="sticky top-0 z-40 bg-white/95 backdrop-blur-md border-b border-amber-200/80 shadow-sm">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
            <div class="flex items-center justify-between h-20">
                <!-- Logo -->
                <div class="flex items-center space-x-3 cursor-pointer" onclick="switchTab('beranda')">
                    <div class="w-12 h-12 bg-gradient-to-br from-brand-red to-brand-darkred rounded-xl flex items-center justify-center text-white shadow-md shadow-red-900/20 transform transition hover:scale-105">
                        <i class="fa-solid fa-book-bookmark text-xl text-amber-300"></i>
                    </div>
                    <div>
                        <span class="text-2xl font-extrabold tracking-tight text-brand-darkred flex items-center gap-1.5 font-serif">
                            EsHist <span class="text-xs bg-amber-100 text-amber-800 font-sans font-bold px-2 py-0.5 rounded-full border border-amber-300">SMA XI</span>
                        </span>
                        <p class="text-xs text-amber-900/70 font-medium hidden sm:block">Eksplorasi Sejarah Pergerakan Nasional</p>
                    </div>
                </div>

                <!-- Desktop Navigation Menu -->
                <nav class="hidden lg:flex items-center space-x-1">
                    <button onclick="switchTab('beranda')" id="nav-beranda" class="nav-btn px-3.5 py-2 rounded-lg text-sm font-semibold transition flex items-center gap-2 text-slate-700 hover:bg-amber-100/60">
                        <i class="fa-solid fa-house text-amber-600"></i> Beranda
                    </button>
                    <button onclick="switchTab('materi')" id="nav-materi" class="nav-btn px-3.5 py-2 rounded-lg text-sm font-semibold transition flex items-center gap-2 text-slate-700 hover:bg-amber-100/60">
                        <i class="fa-solid fa-book-open text-amber-600"></i> Materi
                    </button>
                    <button onclick="switchTab('organisasi')" id="nav-organisasi" class="nav-btn px-3.5 py-2 rounded-lg text-sm font-semibold transition flex items-center gap-2 text-slate-700 hover:bg-amber-100/60">
                        <i class="fa-solid fa-sitemap text-amber-600"></i> Organisasi
                    </button>
                    <button onclick="switchTab('video')" id="nav-video" class="nav-btn px-3.5 py-2 rounded-lg text-sm font-semibold transition flex items-center gap-2 text-slate-700 hover:bg-amber-100/60">
                        <i class="fa-solid fa-circle-play text-amber-600"></i> Video Edukasi
                    </button>
                    <button onclick="switchTab('game')" id="nav-game" class="nav-btn px-3.5 py-2 rounded-lg text-sm font-semibold transition flex items-center gap-2 text-slate-700 hover:bg-amber-100/60">
                        <i class="fa-solid fa-gamepad text-amber-600"></i> Game
                    </button>
                    <button onclick="switchTab('evaluasi')" id="nav-evaluasi" class="nav-btn px-3.5 py-2 rounded-lg text-sm font-semibold transition flex items-center gap-2 text-slate-700 hover:bg-amber-100/60">
                        <i class="fa-solid fa-square-check text-amber-600"></i> Evaluasi
                    </button>
                </nav>

                <!-- Mobile Menu Toggle Button -->
                <div class="lg:hidden">
                    <button id="mobile-menu-btn" onclick="toggleMobileMenu()" class="p-2.5 rounded-lg text-slate-700 hover:bg-amber-100 transition">
                        <i class="fa-solid fa-bars text-xl"></i>
                    </button>
                </div>
            </div>
        </div>

        <!-- Progress Indicator Ribbon -->
        <div class="bg-amber-50 border-t border-amber-200/60 px-4 py-1.5 text-xs text-amber-900 flex justify-between items-center max-w-7xl mx-auto font-medium">
            <div class="flex items-center gap-2">
                <span class="font-bold uppercase tracking-wider text-[10px] text-amber-700">Progres Belajar:</span>
                <span id="progress-text" class="text-slate-700 font-semibold">1 / 6 Modul Dikunjungi</span>
            </div>
            <div class="w-32 sm:w-48 bg-amber-200 h-2 rounded-full overflow-hidden">
                <div id="progress-bar-inner" class="bg-gradient-to-r from-amber-500 to-brand-red h-full w-1/6 transition-all duration-500"></div>
            </div>
        </div>

        <!-- Mobile Menu Dropdown -->
        <div id="mobile-menu" class="hidden lg:hidden border-t border-amber-200 bg-white px-4 pt-2 pb-4 space-y-1 shadow-lg">
            <button onclick="switchTab('beranda'); toggleMobileMenu()" class="w-full text-left px-3 py-2.5 rounded-md text-slate-700 font-medium hover:bg-amber-50 flex items-center gap-3">
                <i class="fa-solid fa-house w-5 text-amber-600"></i> Beranda
            </button>
            <button onclick="switchTab('materi'); toggleMobileMenu()" class="w-full text-left px-3 py-2.5 rounded-md text-slate-700 font-medium hover:bg-amber-50 flex items-center gap-3">
                <i class="fa-solid fa-book-open w-5 text-amber-600"></i> Materi Pembelajaran
            </button>
            <button onclick="switchTab('organisasi'); toggleMobileMenu()" class="w-full text-left px-3 py-2.5 rounded-md text-slate-700 font-medium hover:bg-amber-50 flex items-center gap-3">
                <i class="fa-solid fa-sitemap w-5 text-amber-600"></i> Organisasi Pergerakan
            </button>
            <button onclick="switchTab('video'); toggleMobileMenu()" class="w-full text-left px-3 py-2.5 rounded-md text-slate-700 font-medium hover:bg-amber-50 flex items-center gap-3">
                <i class="fa-solid fa-circle-play w-5 text-amber-600"></i> Video Edukasi
            </button>
            <button onclick="switchTab('game'); toggleMobileMenu()" class="w-full text-left px-3 py-2.5 rounded-md text-slate-700 font-medium hover:bg-amber-50 flex items-center gap-3">
                <i class="fa-solid fa-gamepad w-5 text-amber-600"></i> Game Interaktif
            </button>
            <button onclick="switchTab('evaluasi'); toggleMobileMenu()" class="w-full text-left px-3 py-2.5 rounded-md text-slate-700 font-medium hover:bg-amber-50 flex items-center gap-3">
                <i class="fa-solid fa-square-check w-5 text-amber-600"></i> Evaluasi Kuis
            </button>
        </div>
    </header>

    <main class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-8 flex-grow w-full">

        <!-- ==================== 1. BERANDA VIEW ==================== -->
        <section id="view-beranda" class="view-section active">
            <!-- Hero Banner -->
            <div class="relative rounded-3xl overflow-hidden hero-pattern text-white shadow-2xl mb-12 p-8 sm:p-12 lg:p-16 border border-amber-600/30">
                <div class="relative z-10 max-w-3xl">
                    <span class="inline-flex items-center gap-2 px-3.5 py-1.5 rounded-full text-xs font-bold uppercase tracking-wider bg-amber-500/20 text-amber-200 border border-amber-400/30 mb-6 backdrop-blur-sm">
                        <i class="fa-solid fa-award text-amber-300"></i> Modul Sejarah SMA/MA Kelas XI
                    </span>
                    <h1 class="text-4xl sm:text-5xl lg:text-6xl font-extrabold tracking-tight font-serif leading-tight text-amber-50 mb-4">
                        EsHist
                    </h1>
                    <p class="text-xl sm:text-2xl font-semibold text-amber-200 mb-6 font-serif italic">
                        "Eksplorasi Sejarah Pergerakan Nasional Indonesia"
                    </p>
                    <p class="text-slate-100 text-base sm:text-lg leading-relaxed mb-8 max-w-2xl font-normal">
                        Belajar sejarah tidak hanya dengan membaca. Jelajahi materi interaktif, kenali organisasi pergerakan nasional, tonton video edukasi pilihan, bermain game pencocokan lambang, dan uji pemahamanmu melalui evaluasi kuis!
                    </p>
                    <div class="flex flex-wrap gap-4">
                        <button onclick="switchTab('materi')" class="px-8 py-4 bg-gradient-to-r from-amber-500 to-amber-600 hover:from-amber-600 hover:to-amber-700 text-slate-950 font-bold rounded-xl shadow-lg shadow-amber-900/40 transition transform hover:-translate-y-0.5 flex items-center gap-3">
                            <i class="fa-solid fa-play text-lg"></i> Mulai Belajar
                        </button>
                        <button onclick="switchTab('organisasi')" class="px-7 py-4 bg-white/10 hover:bg-white/20 text-white font-semibold rounded-xl backdrop-blur-md border border-white/20 transition flex items-center gap-2">
                            <i class="fa-solid fa-sitemap text-amber-300"></i> Jelajahi Organisasi
                        </button>
                    </div>
                </div>

                <div class="absolute right-6 bottom-6 opacity-15 sm:opacity-25 pointer-events-none hidden md:block">
                    <i class="fa-solid fa-landmark text-[280px] text-amber-100"></i>
                </div>
            </div>

            <!-- Features Cards Grid -->
            <div class="mb-12">
                <div class="text-center max-w-2xl mx-auto mb-10">
                    <h2 class="text-2xl sm:text-3xl font-bold font-serif text-brand-darkred">Fitur Pembelajaran Utama</h2>
                    <p class="text-slate-600 mt-2 text-sm sm:text-base">Dirancang khusus sesuai Kurikulum SMA/MA Kelas XI.</p>
                </div>

                <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-6">
                    <div onclick="switchTab('materi')" class="bg-white rounded-2xl p-6 border border-amber-200/80 shadow-md hover:shadow-xl transition transform hover:-translate-y-1 cursor-pointer group">
                        <div class="w-14 h-14 bg-amber-100 text-amber-800 rounded-2xl flex items-center justify-center text-2xl mb-5 group-hover:bg-brand-red group-hover:text-white transition">
                            <i class="fa-solid fa-scroll"></i>
                        </div>
                        <h3 class="text-lg font-bold text-slate-900 group-hover:text-brand-red transition mb-2">Materi Sistematis</h3>
                        <p class="text-slate-600 text-sm leading-relaxed">
                            Latar belakang, faktor internal, faktor eksternal, hingga timeline peristiwa 1908-1942.
                        </p>
                    </div>

                    <div onclick="switchTab('organisasi')" class="bg-white rounded-2xl p-6 border border-amber-200/80 shadow-md hover:shadow-xl transition transform hover:-translate-y-1 cursor-pointer group">
                        <div class="w-14 h-14 bg-amber-100 text-amber-800 rounded-2xl flex items-center justify-center text-2xl mb-5 group-hover:bg-brand-red group-hover:text-white transition">
                            <i class="fa-solid fa-sitemap"></i>
                        </div>
                        <h3 class="text-lg font-bold text-slate-900 group-hover:text-brand-red transition mb-2">Database Organisasi</h3>
                        <p class="text-slate-600 text-sm leading-relaxed">
                            Kartu informasi 10 organisasi lengkap dengan lambang, tokoh, tujuan, serta modal detail.
                        </p>
                    </div>

                    <div onclick="switchTab('game')" class="bg-white rounded-2xl p-6 border border-amber-200/80 shadow-md hover:shadow-xl transition transform hover:-translate-y-1 cursor-pointer group">
                        <div class="w-14 h-14 bg-amber-100 text-amber-800 rounded-2xl flex items-center justify-center text-2xl mb-5 group-hover:bg-brand-red group-hover:text-white transition">
                            <i class="fa-solid fa-gamepad"></i>
                        </div>
                        <h3 class="text-lg font-bold text-slate-900 group-hover:text-brand-red transition mb-2">Game Cocok Gambar</h3>
                        <p class="text-slate-600 text-sm leading-relaxed">
                            Asah ingatanmu mencocokkan pasangan lambang organisasi melalui flip card game.
                        </p>
                    </div>

                    <div onclick="switchTab('evaluasi')" class="bg-white rounded-2xl p-6 border border-amber-200/80 shadow-md hover:shadow-xl transition transform hover:-translate-y-1 cursor-pointer group">
                        <div class="w-14 h-14 bg-amber-100 text-amber-800 rounded-2xl flex items-center justify-center text-2xl mb-5 group-hover:bg-brand-red group-hover:text-white transition">
                            <i class="fa-solid fa-square-check"></i>
                        </div>
                        <h3 class="text-lg font-bold text-slate-900 group-hover:text-brand-red transition mb-2">Evaluasi 20 Soal</h3>
                        <p class="text-slate-600 text-sm leading-relaxed">
                            Uji pemahamanmu dengan 20 kuis pilihan ganda komprehensif beserta analisis nilai akhir.
                        </p>
                    </div>
                </div>
            </div>

            <!-- Quote Banner -->
            <div class="bg-gradient-to-r from-amber-900 via-brand-darkred to-amber-950 text-white rounded-2xl p-8 border border-amber-500/30 text-center relative overflow-hidden shadow-lg">
                <i class="fa-solid fa-quote-left text-5xl text-amber-500/20 absolute top-4 left-6"></i>
                <blockquote class="relative z-10 text-lg sm:text-xl font-serif italic max-w-3xl mx-auto text-amber-100">
                    "Jangan sekali-kali meninggalkan sejarah (JASMERAH). Bangsa yang besar adalah bangsa yang menghargai jasa para pahlawannya."
                </blockquote>
                <p class="mt-3 text-sm font-bold text-amber-400 tracking-wide uppercase">— Ir. Soekarno</p>
            </div>
        </section>

        <!-- ==================== 2. MATERI VIEW ==================== -->
        <section id="view-materi" class="view-section">
            <div class="flex flex-col md:flex-row md:items-center justify-between gap-4 bg-white p-6 rounded-2xl border border-amber-200 shadow-sm mb-6">
                <div>
                    <h2 class="text-3xl font-extrabold text-brand-darkred font-serif">Materi Pembelajaran</h2>
                    <p class="text-slate-600 text-sm mt-1">Pergerakan Nasional Indonesia (Awal Abad ke-20 s.d. 1942)</p>
                </div>
                <div class="flex flex-wrap gap-2">
                    <button onclick="switchTab('beranda')" class="px-4 py-2 bg-slate-100 hover:bg-slate-200 text-slate-700 text-sm font-semibold rounded-lg transition flex items-center gap-2">
                        <i class="fa-solid fa-arrow-left"></i> Beranda
                    </button>
                    <button onclick="switchTab('organisasi')" class="px-4 py-2 bg-brand-red hover:bg-brand-darkred text-white text-sm font-semibold rounded-lg transition flex items-center gap-2">
                        Lanjut ke Organisasi <i class="fa-solid fa-arrow-right"></i>
                    </button>
                </div>
            </div>

            <!-- Subbab Tabs -->
            <div class="flex overflow-x-auto gap-2 pb-3 mb-8 custom-scrollbar border-b border-amber-200">
                <button onclick="switchMateriSub('materi-a')" id="subtab-materi-a" class="subtab-btn px-4 py-2.5 rounded-xl text-xs sm:text-sm font-bold whitespace-nowrap bg-brand-red text-white shadow-sm">
                    A. Latar Belakang
                </button>
                <button onclick="switchMateriSub('materi-b')" id="subtab-materi-b" class="subtab-btn px-4 py-2.5 rounded-xl text-xs sm:text-sm font-bold whitespace-nowrap bg-white text-slate-700 hover:bg-amber-100 border border-amber-200">
                    B. Pengertian & Karakteristik
                </button>
                <button onclick="switchMateriSub('materi-c')" id="subtab-materi-c" class="subtab-btn px-4 py-2.5 rounded-xl text-xs sm:text-sm font-bold whitespace-nowrap bg-white text-slate-700 hover:bg-amber-100 border border-amber-200">
                    C. Faktor Internal
                </button>
                <button onclick="switchMateriSub('materi-d')" id="subtab-materi-d" class="subtab-btn px-4 py-2.5 rounded-xl text-xs sm:text-sm font-bold whitespace-nowrap bg-white text-slate-700 hover:bg-amber-100 border border-amber-200">
                    D. Faktor Eksternal
                </button>
                <button onclick="switchMateriSub('materi-e')" id="subtab-materi-e" class="subtab-btn px-4 py-2.5 rounded-xl text-xs sm:text-sm font-bold whitespace-nowrap bg-white text-slate-700 hover:bg-amber-100 border border-amber-200">
                    E. Timeline Interaktif
                </button>
            </div>

            <!-- Subbab A -->
            <div id="materi-a" class="materi-content bg-white p-6 sm:p-8 rounded-2xl border border-amber-200 shadow-sm space-y-6">
                <div class="border-b border-amber-200 pb-4">
                    <span class="text-xs font-extrabold text-amber-800 uppercase tracking-widest bg-amber-100 px-3 py-1 rounded-full border border-amber-300">Subbab A</span>
                    <h3 class="text-2xl font-bold text-slate-900 font-serif mt-3">Latar Belakang Pergerakan Nasional</h3>
                </div>

                <p class="text-slate-700 leading-relaxed text-sm sm:text-base">
                    Lahirnya Pergerakan Nasional Indonesia pada awal abad ke-20 merupakan hasil akumulasi penderitaan rakyat akibat eksploitasi kolonial Belanda, serta dampak penerapan kebijakan <strong>Politik Etis (Ethische Politiek)</strong> yang dicanangkan oleh Ratu Wilhelmina pada tahun 1901 atas gagasan C. Th. van Deventer.
                </p>

                <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                    <div class="bg-amber-50/80 p-5 rounded-xl border border-amber-200">
                        <h4 class="font-bold text-brand-darkred text-base mb-2 flex items-center gap-2">
                            <i class="fa-solid fa-graduation-cap text-amber-600"></i> Munculnya Kaum Terpelajar
                        </h4>
                        <p class="text-xs sm:text-sm text-slate-600 leading-relaxed">
                            Edukasi Politik Etis melahirkan golongan priyayi baru dan pemuda terpelajar (lulusan STOVIA, OSVIA, NIAS). Kaum terpelajar ini menyadari ketidakadilan penjajahan dan memelopori perjuangan modern.
                        </p>
                    </div>

                    <div class="bg-amber-50/80 p-5 rounded-xl border border-amber-200">
                        <h4 class="font-bold text-brand-darkred text-base mb-2 flex items-center gap-2">
                            <i class="fa-solid fa-newspaper text-amber-600"></i> Perkembangan Pers & Komunikasi
                        </h4>
                        <p class="text-sm text-slate-600 leading-relaxed">
                            Surat kabar seperti <em>Medan Prijaji</em> (didirikan Tirto Adhi Soerjo tahun 1907) menyebarkan gagasan kebangsaan, memprotes kesewenang-wenangan kolonial, dan menyatukan pandangan rakyat Nusantara.
                        </p>
                    </div>
                </div>
            </div>

            <!-- Subbab B -->
            <div id="materi-b" class="materi-content hidden bg-white p-6 sm:p-8 rounded-2xl border border-amber-200 shadow-sm space-y-6">
                <div class="border-b border-amber-200 pb-4">
                    <span class="text-xs font-extrabold text-amber-800 uppercase tracking-widest bg-amber-100 px-3 py-1 rounded-full border border-amber-300">Subbab B</span>
                    <h3 class="text-2xl font-bold text-slate-900 font-serif mt-3">Pengertian & Karakteristik Pergerakan Nasional</h3>
                </div>

                <p class="text-slate-700 leading-relaxed text-sm sm:text-base">
                    <strong>Pergerakan Nasional</strong> adalah masa perjuangan kemerdekaan bangsa Indonesia yang dilakukan secara terorganisir, bersifat nasional seluas wilayah Hindia Belanda, mengandalkan diplomasi dan organisasi modern, serta dipimpin oleh kaum terpelajar.
                </p>

                <div class="bg-amber-900 text-amber-50 p-6 rounded-2xl shadow-inner">
                    <h4 class="font-bold text-lg mb-4 text-amber-300 font-serif">Perbandingan Perjuangan Bangsa Indonesia</h4>
                    <div class="grid grid-cols-1 md:grid-cols-2 gap-4 text-xs sm:text-sm">
                        <div class="bg-white/10 p-4 rounded-xl border border-amber-500/30">
                            <span class="font-bold text-amber-300 block mb-2 text-sm border-b border-amber-400/30 pb-1">Sebelum Tahun 1908</span>
                            <ul class="list-disc list-inside space-y-1.5 text-slate-200">
                                <li>Bersifat lokal / kedaerahan.</li>
                                <li>Menggunakan perlawanan fisik/senjata.</li>
                                <li>Dipimpin oleh raja, bangsawan, atau tokoh agama.</li>
                                <li>Sangat bergantung pada kepemimpinan tunggal.</li>
                                <li>Mudah dipecah belah (<em>Devide et Impera</em>).</li>
                            </ul>
                        </div>
                        <div class="bg-white/10 p-4 rounded-xl border border-amber-500/30">
                            <span class="font-bold text-amber-300 block mb-2 text-sm border-b border-amber-400/30 pb-1">Sesudah Tahun 1908</span>
                            <ul class="list-disc list-inside space-y-1.5 text-slate-200">
                                <li>Bersifat Nasional seluas Nusantara.</li>
                                <li>Menggunakan organisasi modern, pers, dan diplomasi.</li>
                                <li>Dipimpin oleh pemuda kaum terpelajar.</li>
                                <li>Memiliki visi jelas: Indonesia Merdeka.</li>
                                <li>Memiliki struktur organisasi yang berkelanjutan.</li>
                            </ul>
                        </div>
                    </div>
                </div>
            </div>

            <!-- Subbab C -->
            <div id="materi-c" class="materi-content hidden bg-white p-6 sm:p-8 rounded-2xl border border-amber-200 shadow-sm space-y-6">
                <div class="border-b border-amber-200 pb-4">
                    <span class="text-xs font-extrabold text-amber-800 uppercase tracking-widest bg-amber-100 px-3 py-1 rounded-full border border-amber-300">Subbab C</span>
                    <h3 class="text-2xl font-bold text-slate-900 font-serif mt-3">Faktor Internal Pendorong Pergerakan</h3>
                </div>

                <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
                    <div class="p-5 border border-slate-200 rounded-xl hover:border-amber-400 transition bg-slate-50">
                        <span class="w-8 h-8 rounded-lg bg-brand-red text-white font-bold flex items-center justify-center mb-3 text-sm">1</span>
                        <h4 class="font-bold text-slate-900 mb-1">Penderitaan Akibat Kolonialisme</h4>
                        <p class="text-xs text-slate-600">Sistem Tanam Paksa (Cultuurstelsel), kerja rodi, serta monopoli ekonomi menimbulkan kemiskinan dan penderitaan bagi rakyat.</p>
                    </div>
                    <div class="p-5 border border-slate-200 rounded-xl hover:border-amber-400 transition bg-slate-50">
                        <span class="w-8 h-8 rounded-lg bg-brand-red text-white font-bold flex items-center justify-center mb-3 text-sm">2</span>
                        <h4 class="font-bold text-slate-900 mb-1">Kenangan Kejayaan Masa Lalu</h4>
                        <p class="text-xs text-slate-600">Ingatan sejarah akan keagungan Kerajaan Sriwijaya dan Majapahit membangkitkan kebanggaan bahwa Nusantara pernah bersatu dan berdaulat.</p>
                    </div>
                    <div class="p-5 border border-slate-200 rounded-xl hover:border-amber-400 transition bg-slate-50">
                        <span class="w-8 h-8 rounded-lg bg-brand-red text-white font-bold flex items-center justify-center mb-3 text-sm">3</span>
                        <h4 class="font-bold text-slate-900 mb-1">Lahirnya Golongan Terpelajar</h4>
                        <p class="text-xs text-slate-600">Lulusan lembaga pendidikan barat menyerap pemikiran demokrasi, hak asasi manusia, serta nasionalisme.</p>
                    </div>
                    <div class="p-5 border border-slate-200 rounded-xl hover:border-amber-400 transition bg-slate-50">
                        <span class="w-8 h-8 rounded-lg bg-brand-red text-white font-bold flex items-center justify-center mb-3 text-sm">4</span>
                        <h4 class="font-bold text-slate-900 mb-1">Bahasa Melayu Sebagai Lingua Franca</h4>
                        <p class="text-xs text-slate-600">Penggunaan Bahasa Melayu mempermudah komunikasi antarsuku di seluruh kawasan wilayah Hindia Belanda.</p>
                    </div>
                </div>
            </div>

            <!-- Subbab D -->
            <div id="materi-d" class="materi-content hidden bg-white p-6 sm:p-8 rounded-2xl border border-amber-200 shadow-sm space-y-6">
                <div class="border-b border-amber-200 pb-4">
                    <span class="text-xs font-extrabold text-amber-800 uppercase tracking-widest bg-amber-100 px-3 py-1 rounded-full border border-amber-300">Subbab D</span>
                    <h3 class="text-2xl font-bold text-slate-900 font-serif mt-3">Faktor Eksternal (Pengaruh Luar Negeri)</h3>
                </div>

                <div class="space-y-4">
                    <div class="flex gap-4 p-4 rounded-xl border border-amber-200 bg-amber-50/50 items-start">
                        <div class="w-12 h-12 rounded-xl bg-amber-600 text-white flex-shrink-0 flex items-center justify-center font-extrabold text-sm sm:text-base">1905</div>
                        <div>
                            <h4 class="font-bold text-slate-900 text-base">Kemenangan Jepang atas Rusia (1905)</h4>
                            <p class="text-xs sm:text-sm text-slate-600 mt-1">
                                Kemenangan armada militer Jepang atas Rusia meruntuhkan mitos bahwa bangsa ras kulit putih mustahil dikalahkan oleh bangsa Asia. Hal ini membakar percaya diri pemuda Indonesia.
                            </p>
                        </div>
                    </div>

                    <div class="flex gap-4 p-4 rounded-xl border border-amber-200 bg-amber-50/50 items-start">
                        <div class="w-12 h-12 rounded-xl bg-brand-red text-white flex-shrink-0 flex items-center justify-center font-extrabold text-lg"><i class="fa-solid fa-globe"></i></div>
                        <div>
                            <h4 class="font-bold text-slate-900 text-base">Gerakan Nasionalisme di Asia & Afrika</h4>
                            <ul class="text-xs sm:text-sm text-slate-600 mt-1 space-y-1 list-disc list-inside">
                                <li><strong>India:</strong> Perjuangan Mahatma Gandhi dengan asas <em>Ahimsa</em> (tanpa kekerasan) & <em>Satyagraha</em>.</li>
                                <li><strong>Tiongkok:</strong> Revolusi Tiongkok 1911 yang dipimpin Dr. Sun Yat Sen dengan tiga asas ideologi <em>San Min Chu I</em>.</li>
                                <li><strong>Turki:</strong> Gerakan Turki Muda (1908) yang dipimpin Mustafa Kemal Pasha.</li>
                                <li><strong>Filipina:</strong> Perjuangan Liga Filipina yang dipimpin Dr. Jose Rizal.</li>
                            </ul>
                        </div>
                    </div>
                </div>
            </div>

            <!-- Subbab E: Timeline Interaktif -->
            <div id="materi-e" class="materi-content hidden bg-white p-6 sm:p-8 rounded-2xl border border-amber-200 shadow-sm space-y-8">
                <div class="border-b border-amber-200 pb-4 text-center max-w-2xl mx-auto">
                    <span class="text-xs font-extrabold text-amber-800 uppercase tracking-widest bg-amber-100 px-3 py-1 rounded-full border border-amber-300">Subbab E</span>
                    <h3 class="text-2xl font-bold text-slate-900 font-serif mt-3">Timeline Peristiwa Penting (1908 - 1942)</h3>
                    <p class="text-xs sm:text-sm text-slate-600 mt-1">Klik pada setiap nodus tahun untuk membaca ringkasan peristiwa sejarah!</p>
                </div>

                <div class="relative timeline-line max-w-3xl mx-auto py-6 space-y-8">
                    
                    <!-- Timeline Node 1908 -->
                    <div onclick="openTimelineModal('1908')" class="relative z-10 flex flex-col md:flex-row items-center cursor-pointer group">
                        <div class="w-full md:w-1/2 md:pr-8 text-center md:text-right mb-2 md:mb-0">
                            <span class="text-2xl font-black text-brand-red font-serif group-hover:scale-110 transition inline-block">1908</span>
                            <h4 class="font-bold text-slate-800">Lahirnya Budi Utomo</h4>
                        </div>
                        <div class="w-10 h-10 rounded-full bg-brand-gold border-4 border-white shadow text-white flex items-center justify-center font-bold text-sm my-2 md:my-0 group-hover:bg-brand-red transition">
                            <i class="fa-solid fa-seedling"></i>
                        </div>
                        <div class="w-full md:w-1/2 md:pl-8 text-center md:text-left text-xs text-slate-500">
                            Awal Kebangkitan Nasional (20 Mei 1908) oleh para mahasiswa STOVIA.
                        </div>
                    </div>

                    <!-- Timeline Node 1912 -->
                    <div onclick="openTimelineModal('1912')" class="relative z-10 flex flex-col md:flex-row items-center cursor-pointer group">
                        <div class="w-full md:w-1/2 md:pr-8 text-center md:text-right order-1 md:order-1 text-xs text-slate-500">
                            Berdirinya Sarekat Islam, Indische Partij, dan Muhammadiyah.
                        </div>
                        <div class="w-10 h-10 rounded-full bg-brand-gold border-4 border-white shadow text-white flex items-center justify-center font-bold text-sm my-2 md:my-0 group-hover:bg-brand-red transition order-2">
                            <i class="fa-solid fa-flag"></i>
                        </div>
                        <div class="w-full md:w-1/2 md:pl-8 text-center md:text-left order-3 md:order-3 mb-2 md:mb-0">
                            <span class="text-2xl font-black text-brand-red font-serif group-hover:scale-110 transition inline-block">1912</span>
                            <h4 class="font-bold text-slate-800">Masa Organisasi Politik</h4>
                        </div>
                    </div>

                    <!-- Timeline Node 1918 -->
                    <div onclick="openTimelineModal('1918')" class="relative z-10 flex flex-col md:flex-row items-center cursor-pointer group">
                        <div class="w-full md:w-1/2 md:pr-8 text-center md:text-right mb-2 md:mb-0">
                            <span class="text-2xl font-black text-brand-red font-serif group-hover:scale-110 transition inline-block">1918</span>
                            <h4 class="font-bold text-slate-800">Pembentukan Volksraad</h4>
                        </div>
                        <div class="w-10 h-10 rounded-full bg-brand-gold border-4 border-white shadow text-white flex items-center justify-center font-bold text-sm my-2 md:my-0 group-hover:bg-brand-red transition">
                            <i class="fa-solid fa-building-columns"></i>
                        </div>
                        <div class="w-full md:w-1/2 md:pl-8 text-center md:text-left text-xs text-slate-500">
                            Dewan Rakyat bentukan Belanda sebagai sarana perjuangan diplomasi.
                        </div>
                    </div>

                    <!-- Timeline Node 1927 -->
                    <div onclick="openTimelineModal('1927')" class="relative z-10 flex flex-col md:flex-row items-center cursor-pointer group">
                        <div class="w-full md:w-1/2 md:pr-8 text-center md:text-right text-xs text-slate-500">
                            Ir. Soekarno mendirikan PNI di Bandung berazas Radikal Non-Kooperasi.
                        </div>
                        <div class="w-10 h-10 rounded-full bg-brand-gold border-4 border-white shadow text-white flex items-center justify-center font-bold text-sm my-2 md:my-0 group-hover:bg-brand-red transition">
                            <i class="fa-solid fa-bullhorn"></i>
                        </div>
                        <div class="w-full md:w-1/2 md:pl-8 text-center md:text-left mb-2 md:mb-0">
                            <span class="text-2xl font-black text-brand-red font-serif group-hover:scale-110 transition inline-block">1927</span>
                            <h4 class="font-bold text-slate-800">Pendirian PNI</h4>
                        </div>
                    </div>

                    <!-- Timeline Node 1928 -->
                    <div onclick="openTimelineModal('1928')" class="relative z-10 flex flex-col md:flex-row items-center cursor-pointer group">
                        <div class="w-full md:w-1/2 md:pr-8 text-center md:text-right mb-2 md:mb-0">
                            <span class="text-2xl font-black text-brand-red font-serif group-hover:scale-110 transition inline-block">1928</span>
                            <h4 class="font-bold text-slate-800">Sumpah Pemuda</h4>
                        </div>
                        <div class="w-10 h-10 rounded-full bg-brand-red border-4 border-white shadow text-white flex items-center justify-center font-bold text-sm my-2 md:my-0 group-hover:scale-125 transition">
                            <i class="fa-solid fa-star"></i>
                        </div>
                        <div class="w-full md:w-1/2 md:pl-8 text-center md:text-left text-xs text-slate-500">
                            Kongres Pemuda II menyatukan tekad Satu Nusa, Satu Bangsa, Satu Bahasa.
                        </div>
                    </div>

                    <!-- Timeline Node 1942 -->
                    <div onclick="openTimelineModal('1942')" class="relative z-10 flex flex-col md:flex-row items-center cursor-pointer group">
                        <div class="w-full md:w-1/2 md:pr-8 text-center md:text-right text-xs text-slate-500">
                            Belanda menyerah tanpa syarat di Kalijati kepada Kekaisaran Jepang.
                        </div>
                        <div class="w-10 h-10 rounded-full bg-brand-gold border-4 border-white shadow text-white flex items-center justify-center font-bold text-sm my-2 md:my-0 group-hover:bg-brand-red transition">
                            <i class="fa-solid fa-shield-halved"></i>
                        </div>
                        <div class="w-full md:w-1/2 md:pl-8 text-center md:text-left mb-2 md:mb-0">
                            <span class="text-2xl font-black text-brand-red font-serif group-hover:scale-110 transition inline-block">1942</span>
                            <h4 class="font-bold text-slate-800">Pendudukan Jepang</h4>
                        </div>
                    </div>

                </div>
            </div>
        </section>

        <!-- ==================== 3. ORGANISASI VIEW ==================== -->
        <section id="view-organisasi" class="view-section">
            <div class="mb-8">
                <div class="flex flex-col md:flex-row md:items-center justify-between gap-4 bg-white p-6 rounded-2xl border border-amber-200 shadow-sm mb-6">
                    <div>
                        <h2 class="text-3xl font-extrabold text-brand-darkred font-serif">Organisasi Pergerakan</h2>
                        <p class="text-slate-600 text-sm mt-1">Eksplorasi rekam jejak, lambang, tokoh, dan peran sejarah 10 organisasi utama.</p>
                    </div>
                    <!-- Live Search -->
                    <div class="relative w-full md:w-72">
                        <input type="text" id="org-search-input" oninput="filterOrganizations()" placeholder="Cari organisasi atau tokoh..." class="w-full pl-10 pr-4 py-2.5 rounded-xl border border-amber-300 focus:outline-none focus:ring-2 focus:ring-brand-gold text-sm bg-white">
                        <i class="fa-solid fa-magnifying-glass absolute left-3.5 top-3.5 text-amber-600"></i>
                    </div>
                </div>

                <!-- Category Filters -->
                <div class="flex flex-wrap gap-2 mb-6">
                    <button onclick="setOrgFilter('all')" class="org-filter-btn px-4 py-2 rounded-xl text-xs font-bold bg-brand-red text-white shadow-sm" data-filter="all">Semua Organisasi</button>
                    <button onclick="setOrgFilter('Awal')" class="org-filter-btn px-4 py-2 rounded-xl text-xs font-bold bg-white text-slate-700 hover:bg-amber-100 border border-amber-200" data-filter="Awal">Masa Pelopor (1908-1912)</button>
                    <button onclick="setOrgFilter('Keagamaan')" class="org-filter-btn px-4 py-2 rounded-xl text-xs font-bold bg-white text-slate-700 hover:bg-amber-100 border border-amber-200" data-filter="Keagamaan">Masa Keagamaan</button>
                    <button onclick="setOrgFilter('Radikal')" class="org-filter-btn px-4 py-2 rounded-xl text-xs font-bold bg-white text-slate-700 hover:bg-amber-100 border border-amber-200" data-filter="Radikal">Masa Radikal / Non-Kooperasi</button>
                    <button onclick="setOrgFilter('Moderat')" class="org-filter-btn px-4 py-2 rounded-xl text-xs font-bold bg-white text-slate-700 hover:bg-amber-100 border border-amber-200" data-filter="Moderat">Masa Moderat / Kooperasi</button>
                </div>
            </div>

            <!-- Organization Cards Grid -->
            <div id="org-grid-container" class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
                <!-- Populated via JS -->
            </div>
        </section>

        <!-- ==================== 4. VIDEO EDUKASI VIEW ==================== -->
        <section id="view-video" class="view-section">
            <div class="flex flex-col md:flex-row md:items-center justify-between gap-4 bg-white p-6 rounded-2xl border border-amber-200 shadow-sm mb-8">
                <div>
                    <h2 class="text-3xl font-extrabold text-brand-darkred font-serif">Video Edukasi</h2>
                    <p class="text-slate-600 text-sm mt-1">Saksikan video rangkuman audiovisual pergerakan nasional Indonesia.</p>
                </div>
                <div class="text-xs text-amber-800 bg-amber-100 px-3 py-1.5 rounded-lg border border-amber-300 font-semibold flex items-center gap-2">
                    <i class="fa-solid fa-circle-info"></i> Klik video untuk memutar tayangan
                </div>
            </div>

            <!-- Video Grid Container -->
            <div id="video-grid-container" class="grid grid-cols-1 md:grid-cols-3 gap-6">
                <!-- Populated via JS -->
            </div>
        </section>

        <!-- ==================== 5. GAME VIEW ==================== -->
        <section id="view-game" class="view-section">
            <div class="bg-white p-6 rounded-2xl border border-amber-200 shadow-sm mb-6 flex flex-col md:flex-row justify-between items-center gap-4">
                <div>
                    <h2 class="text-3xl font-extrabold text-brand-darkred font-serif">Game: Samakan Dua Gambar</h2>
                    <p class="text-slate-600 text-sm mt-1">Buka kartu dan cari 8 pasangan lambang organisasi pergerakan nasional yang cocok!</p>
                </div>
                <div class="flex items-center gap-4">
                    <div class="text-center bg-amber-50 px-4 py-2 rounded-xl border border-amber-200">
                        <span class="text-[10px] text-amber-800 uppercase font-bold block">Percobaan</span>
                        <span id="game-attempts" class="text-lg font-black text-brand-darkred">0</span>
                    </div>
                    <div class="text-center bg-amber-50 px-4 py-2 rounded-xl border border-amber-200">
                        <span class="text-[10px] text-amber-800 uppercase font-bold block">Pasangan</span>
                        <span id="game-matches" class="text-lg font-black text-brand-darkred">0 / 8</span>
                    </div>
                    <div class="text-center bg-amber-50 px-4 py-2 rounded-xl border border-amber-200">
                        <span class="text-[10px] text-amber-800 uppercase font-bold block">Waktu</span>
                        <span id="game-timer" class="text-lg font-black text-amber-700">00:00</span>
                    </div>
                    <button onclick="initGame()" class="px-4 py-2.5 bg-brand-red hover:bg-brand-darkred text-white font-bold rounded-xl text-sm transition shadow flex items-center gap-2">
                        <i class="fa-solid fa-rotate-right"></i> Reset Game
                    </button>
                </div>
            </div>

            <!-- Game Board Container -->
            <div id="game-board" class="grid grid-cols-2 sm:grid-cols-4 gap-4 max-w-4xl mx-auto">
                <!-- Cards generated via JS -->
            </div>

            <!-- Game Win Banner Modal -->
            <div id="game-win-banner" class="hidden fixed inset-0 bg-slate-900/70 backdrop-blur-sm z-50 flex items-center justify-center p-4">
                <div class="bg-white rounded-3xl p-8 max-w-md w-full text-center border-2 border-amber-400 shadow-2xl space-y-4">
                    <div class="w-20 h-20 bg-amber-100 text-amber-600 rounded-full flex items-center justify-center text-4xl mx-auto">
                        <i class="fa-solid fa-trophy"></i>
                    </div>
                    <h3 class="text-2xl font-extrabold text-slate-900 font-serif">Selamat! Perjuangan Selesai!</h3>
                    <p class="text-slate-600 text-sm">Kamu berhasil menemukan seluruh pasangan lambang organisasi pergerakan nasional.</p>
                    <div class="bg-amber-50 p-4 rounded-xl border border-amber-200 text-xs text-slate-700 space-y-1">
                        <p>Total Percobaan: <strong id="win-attempts" class="text-brand-darkred text-sm">0</strong></p>
                        <p>Waktu Selesai: <strong id="win-time" class="text-brand-darkred text-sm">00:00</strong></p>
                    </div>
                    <button onclick="initGame(); document.getElementById('game-win-banner').classList.add('hidden')" class="w-full py-3 bg-brand-red hover:bg-brand-darkred text-white font-bold rounded-xl shadow transition">
                        Main Lagi
                    </button>
                </div>
            </div>
        </section>

        <!-- ==================== 6. EVALUASI VIEW ==================== -->
        <section id="view-evaluasi" class="view-section">
            <div id="quiz-container" class="bg-white p-6 sm:p-8 rounded-2xl border border-amber-200 shadow-sm max-w-3xl mx-auto">
                <!-- Quiz Progress Bar -->
                <div class="flex items-center justify-between mb-6 border-b border-amber-200 pb-4">
                    <div>
                        <span id="quiz-question-number" class="text-xs font-extrabold uppercase text-amber-800 bg-amber-100 px-3 py-1 rounded-full border border-amber-300">Soal 1 dari 20</span>
                        <h3 class="text-xl font-bold text-slate-900 font-serif mt-2">Evaluasi Pemahaman Sejarah</h3>
                    </div>
                    <span id="quiz-timer-text" class="text-xs font-semibold text-slate-500">Pilih Jawaban Terbaik</span>
                </div>

                <!-- Question Text -->
                <div id="quiz-question-text" class="text-base sm:text-lg font-medium text-slate-800 mb-6 leading-relaxed">
                    <!-- Text inserted by JS -->
                </div>

                <!-- Choices Container -->
                <div id="quiz-options-container" class="space-y-3 mb-8">
                    <!-- Radio/Buttons inserted by JS -->
                </div>

                <!-- Navigation Controls -->
                <div class="flex justify-between items-center border-t border-amber-200 pt-4">
                    <button id="quiz-prev-btn" onclick="prevQuestion()" class="px-5 py-2.5 bg-slate-100 hover:bg-slate-200 text-slate-700 font-bold rounded-xl text-sm transition disabled:opacity-40 flex items-center gap-2">
                        <i class="fa-solid fa-arrow-left"></i> Sebelumnya
                    </button>
                    <button id="quiz-next-btn" onclick="nextQuestion()" class="px-6 py-2.5 bg-brand-red hover:bg-brand-darkred text-white font-bold rounded-xl text-sm transition flex items-center gap-2">
                        Berikutnya <i class="fa-solid fa-arrow-right"></i>
                    </button>
                </div>
            </div>

            <!-- Quiz Result Container -->
            <div id="quiz-result-container" class="hidden bg-white p-8 rounded-2xl border border-amber-200 shadow-md max-w-2xl mx-auto text-center space-y-6">
                <div class="w-24 h-24 bg-gradient-to-br from-amber-400 to-amber-600 rounded-full flex items-center justify-center text-white text-4xl mx-auto shadow-lg shadow-amber-500/30">
                    <i class="fa-solid fa-award"></i>
                </div>
                <div>
                    <h3 class="text-3xl font-extrabold text-slate-900 font-serif">Hasil Evaluasi Pembelajaran</h3>
                    <p class="text-slate-600 text-sm mt-1">Ulasan pencapaian materi Pergerakan Nasional Indonesia</p>
                </div>

                <div class="bg-amber-50 p-6 rounded-2xl border border-amber-200 grid grid-cols-3 gap-4">
                    <div>
                        <span class="text-xs text-slate-500 block">Benar</span>
                        <span id="result-correct" class="text-2xl font-black text-emerald-600">0</span>
                    </div>
                    <div>
                        <span class="text-xs text-slate-500 block">Salah</span>
                        <span id="result-incorrect" class="text-2xl font-black text-rose-600">0</span>
                    </div>
                    <div>
                        <span class="text-xs text-slate-500 block">Nilai Akhir</span>
                        <span id="result-score" class="text-3xl font-black text-brand-darkred">0</span>
                    </div>
                </div>

                <div id="result-message-box" class="p-4 rounded-xl text-sm font-medium leading-relaxed bg-amber-100 text-amber-900 border border-amber-300">
                    <!-- Result feedback message -->
                </div>

                <div class="flex flex-col sm:flex-row justify-center gap-4 pt-2">
                    <button onclick="switchTab('materi')" class="px-6 py-3 bg-slate-100 hover:bg-slate-200 text-slate-800 font-bold rounded-xl text-sm transition flex items-center justify-center gap-2">
                        <i class="fa-solid fa-book-open"></i> Pelajari Kembali Materi
                    </button>
                    <button onclick="resetQuiz()" class="px-6 py-3 bg-brand-red hover:bg-brand-darkred text-white font-bold rounded-xl text-sm transition flex items-center justify-center gap-2">
                        <i class="fa-solid fa-rotate-right"></i> Ulangi Evaluasi
                    </button>
                </div>
            </div>
        </section>

    </main>

    <!-- GENERAL MODAL POPUP -->
    <div id="app-modal" class="hidden fixed inset-0 bg-slate-900/70 backdrop-blur-sm z-50 flex items-center justify-center p-4">
        <div class="bg-white rounded-3xl max-w-2xl w-full max-h-[90vh] overflow-y-auto custom-scrollbar border border-amber-300 shadow-2xl p-6 sm:p-8 relative">
            <button onclick="closeAppModal()" class="absolute top-5 right-5 text-slate-400 hover:text-slate-700 w-9 h-9 bg-slate-100 rounded-full flex items-center justify-center text-lg transition">
                <i class="fa-solid fa-xmark"></i>
            </button>
            <div id="app-modal-body">
                <!-- Modal content dynamically injected -->
            </div>
        </div>
    </div>

    <!-- FOOTER -->
    <footer class="bg-brand-dark font-sans text-amber-200/80 border-t border-amber-900/50 py-8 mt-12 text-xs">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 text-center space-y-2">
            <p class="font-semibold text-amber-100">EsHist — Exploring History: Pergerakan Nasional Indonesia</p>
            <p class="text-amber-300/60">Media Pembelajaran Interaktif Sejarah Indonesia SMA/MA Kelas XI</p>
        </div>
    </footer>

    <script>
        /* ==================== DATA STRUCTURES ==================== */

        // 1. ORGANIZATIONS DATA (10 Required Organizations)
        const organizations = [
            {
                id: "bu",
                name: "Budi Utomo",
                year: 1908,
                category: "Awal",
                badgeSvg: `<svg class="w-12 h-12 text-amber-700" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><circle cx="12" cy="12" r="10"/><path d="M12 8v8M8 12h8"/></svg>`,
                founders: "Dr. Soetomo, Dr. Wahidin Sudirohusodo, mahasiswa STOVIA",
                goals: "Memajukan pendidikan, kebudayaan, serta pertanian di wilayah Jawa dan Madura.",
                role: "Sebagai organisasi modern pertama yang memicu lahirnya Kebangkitan Nasional (20 Mei 1908).",
                summary: "Pelopor organisasi modern di Indonesia berbasis kebudayaan Jawa dan kemajuan pendidikan kaum pribumi."
            },
            {
                id: "si",
                name: "Sarekat Islam",
                year: 1912,
                category: "Awal",
                badgeSvg: `<svg class="w-12 h-12 text-emerald-700" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M12 2L2 7l10 5 10-5-10-5zM2 17l10 5 10-5M2 12l10 5 10-5"/></svg>`,
                founders: "H. Samanhudi (SDI 1911), H.O.S. Cokroaminoto",
                goals: "Membela pedagang pribumi Muslim, memajukan perdagangan dan agama Islam, serta memperjuangkan kesetaraan.",
                role: "Organisasi massa terbesar pertama di Indonesia yang berhasil menghimpun jutaan rakyat secara terbuka.",
                summary: "Beralih dari Sarekat Dagang Islam menjadi Sarekat Islam untuk memperluas jangkauan perjuangan ekonomi & sosial."
            },
            {
                id: "ip",
                name: "Indische Partij",
                year: 1912,
                category: "Radikal",
                badgeSvg: `<svg class="w-12 h-12 text-brand-red" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M4 15s1-1 4-1 5 2 8 2 4-1 4-1V3s-1 1-4 1-5-2-8-2-4 1-4 1zM4 22v-7"/></svg>`,
                founders: "Tiga Serangkai: E.F.E. Douwes Dekker, Dr. Cipto Mangunkusumo, Suwardi Suryaningrat",
                goals: "Membangun rasa patriotisme seluruh 'Indier' dan menuntut kemerdekaan penuh Hindia Belanda.",
                role: "Organisasi politik pertama di Indonesia yang secara terang-terangan menyuarakan paham nasionalisme radikal.",
                summary: "Dikenal dengan semboyan 'Indie voor Indiers' dan majalah 'Het Tijdschrift' sebelum akhirnya dilarang Belanda."
            },
            {
                id: "pi",
                name: "Perhimpunan Indonesia",
                year: 1908,
                category: "Radikal",
                badgeSvg: `<svg class="w-12 h-12 text-amber-800" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><circle cx="12" cy="12" r="10"/><path d="M2 12h20M12 2a15.3 15.3 0 014 10 15.3 15.3 0 01-4 10 15.3 15.3 0 01-4-10 15.3 15.3 0 014-10z"/></svg>`,
                founders: "Sultan Kasayangan, Noto Suroto, Mohammad Hatta, Ahmad Subardjo",
                goals: "Memperjuangkan kemerdekaan Indonesia dari Negeri Belanda menggunakan prinsip Self-Help & Non-Kooperasi.",
                role: "Menjadi pelopor penggunaan kata 'Indonesia' di kancah internasional dan mempromosikan ideologi anti-kolonial.",
                summary: "Dandani diplomasi pelajar Indonesia di Belanda (Indische Vereeniging yang berubah menjadi Perhimpunan Indonesia)."
            },
            {
                id: "pni",
                name: "Partai Nasional Indonesia",
                year: 1927,
                category: "Radikal",
                badgeSvg: `<svg class="w-12 h-12 text-brand-red" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><polygon points="12 2 15.09 8.26 22 9.27 17 14.14 18.18 21.02 12 17.77 5.82 21.02 7 14.14 2 9.27 8.91 8.26 12 2"/></svg>`,
                founders: "Ir. Soekarno, Tjipto Mangoenkoesoemo, Mr. Sartono, Sunario",
                goals: "Mencapai Kemerdekaan Indonesia secara utuh berlandaskan asas Marhaenisme dan Non-Kooperasi.",
                role: "Mampu menyatukan semangat rakyat dan membangkitkan nasionalisme massa hingga penangkapan Soekarno.",
                summary: "Pelopor utama pergerakan radikal non-kooperasi di tanah air dengan pidato terkenal 'Indonesia Menggugat'."
            },
            {
                id: "muh",
                name: "Muhammadiyah",
                year: 1912,
                category: "Keagamaan",
                badgeSvg: `<svg class="w-12 h-12 text-amber-600" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><circle cx="12" cy="12" r="9"/><path d="M12 3v18M3 12h18"/></svg>`,
                founders: "K.H. Ahmad Dahlan (Yogyakarta)",
                goals: "Pemurnian ajaran Islam berdasarkan Al-Qur'an & Hadis serta memajukan pendidikan sosial kesehatan modern.",
                role: "Mendirikan ribuan sekolah, rumah sakit, dan panti asuhan untuk meningkatkan taraf hidup rakyat pribumi.",
                summary: "Organisasi kemasyarakatan berazas Islam yang berfokus pada reformasi pendidikan modern dan pemuliaan sosial."
            },
            {
                id: "nu",
                name: "Nahdlatul Ulama",
                year: 1926,
                category: "Keagamaan",
                badgeSvg: `<svg class="w-12 h-12 text-emerald-800" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M12 2a10 10 0 100 20 10 10 0 000-20zM12 6v12M6 12h12"/></svg>`,
                founders: "K.H. Hasyim Asy'ari, K.H. Wahab Hasbullah (Jombang)",
                goals: "Menjaga tradisi Islam Ahlussunnah wal Jama'ah serta membela kepentingan ummat dan tanah air.",
                role: "Menjadi benteng keberagamaan tradisionalis, menguatkan sistem pesantren, serta menolak dominasi asing.",
                summary: "Wadah persatuan para ulama dan santri dalam membela ajaran keislaman dan perjuangan kebangsaan Indonesia."
            },
            {
                id: "parindra",
                name: "Partai Indonesia Raya (Parindra)",
                year: 1935,
                category: "Moderat",
                badgeSvg: `<svg class="w-12 h-12 text-amber-900" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><rect x="3" y="3" width="18" height="18" rx="2"/><path d="M8 12h8M12 8v8"/></svg>`,
                founders: "Dr. Soetomo (Penggabungan Budi Utomo & PBI)",
                goals: "Mencapai Indonesia Raya yang merdeka melalui perjuangan moderat kooperasi dan Volksraad.",
                role: "Memperjuangkan perbaikan ekonomi, mendirikan bank rakyat, serta memperkuat keterwakilan di dewan rakyat.",
                summary: "Organisasi penganut taktik moderat terbesar pada periode 1930-an menjelang Perang Dunia II."
            },
            {
                id: "gerindo",
                name: "Gerakan Rakyat Indonesia (Gerindo)",
                year: 1937,
                category: "Moderat",
                badgeSvg: `<svg class="w-12 h-12 text-rose-800" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M17 21v-2a4 4 0 00-4-4H5a4 4 0 00-4 4v2"/><circle cx="9" cy="7" r="4"/><path d="M23 21v-2a4 4 0 00-3-3.87M16 3.13a4 4 0 010 7.75"/></svg>`,
                founders: "A.K. Gani, Amir Sjarifuddin, Yamin, Sartono",
                goals: "Membentuk pemerintahan demokratis dan melawan ancaman fasisme dunia (Jepang & Jerman).",
                role: "Pelopor kesadaran anti-fasisme dan pendukung gerakan gabungan GAPI (Gabungan Politik Indonesia).",
                summary: "Organisasi kiri-moderat yang sangat kritis terhadap ancaman ideologi militerisme imperial fasis."
            },
            {
                id: "partindo",
                name: "Partai Indonesia (Partindo)",
                year: 1931,
                category: "Radikal",
                badgeSvg: `<svg class="w-12 h-12 text-amber-700" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M12 22s8-4 8-10V5l-8-3-8 3v7c0 6 8 10 8 10z"/></svg>`,
                founders: "Mr. Sartono, Ir. Soekarno (bergabung 1932)",
                goals: "Mencapai Indonesia merdeka dengan azas non-kooperasi setelah PNI dibubarkan.",
                role: "Wadah kelanjutan perjuangan massa Marhaenisme hingga represivitas kolonial mengetat.",
                summary: "Didirikan oleh Mr. Sartono sebagai pecahan dari PNI lama yang dibubarkan akibat pembatasan Belanda."
            }
        ];

        // 2. EDUCATIONAL VIDEOS DATA
        const videos = [
            {
                title: "Latar Belakang Pergerakan Nasional",
                desc: "Ulasan penyebab internal dan eksternal pemicu lahirnya kesadaran kebangsaan di Indonesia awal abad ke-20.",
                embedUrl: "https://youtu.be/-WdlE8EjR80?si=X4I2aG7GoyM9XHZW",
                badge: "Dasar Sejarah"
            },
            {
                title: "Peran Organisasi Pergerakan Nasional",
                desc: "Penjelasan transformasi strategi dari Budi Utomo, Sarekat Islam, hingga PNI radikal non-kooperasi.",
                embedUrl: "https://youtu.be/BGMCaCwEdTE?si=v6Nu3PvJnvqxlHpK",
                badge: "Organisasi"
            },
            {
                title: "Sumpah Pemuda 1928 & Perjuangan Bangsa",
                desc: "Peristiwa penting Kongres Pemuda II yang melahirkan kesepakatan Tunggal Nusa, Bangsa, dan Bahasa.",
                embedUrl: "https://youtu.be/DKbAb08tB30?si=kmPt2hfeSaECaFys",
                badge: "Nasionalisme"
            }
        ];

        // 3. 20 MULTIPLE CHOICE EVALUATION QUESTIONS
        const quizQuestions = [
            {
                q: "1. Siapakah tokoh Belanda yang mencetuskan gagasan Politik Etis (Ethische Politiek) pada akhir abad ke-19 yang mendorong pendidikan modern di Indonesia?",
                options: ["C. Th. van Deventer", "E.F.E. Douwes Dekker", "J.P. Coen", "Van den Bosch"],
                answer: 0
            },
            {
                q: "2. Faktor internal utama yang memicu lahirnya Pergerakan Nasional Indonesia pada awal abad ke-20 adalah...",
                options: [
                    "Kemenangan Jepang atas Rusia tahun 1905",
                    "Lahirnya golongan terpelajar hasil dari Politik Etis",
                    "Revolusi Tiongkok yang dipimpin Dr. Sun Yat Sen",
                    "Gerakan Ahimsa dan Satyagraha di India"
                ],
                answer: 1
            },
            {
                q: "3. Organisasi Budi Utomo didirikan pada tanggal 20 Mei 1908 oleh para mahasiswa STOVIA di bawah dorongan gagasan...",
                options: ["Dr. Wahidin Sudirohusodo", "H.O.S. Cokroaminoto", "Ir. Soekarno", "K.H. Ahmad Dahlan"],
                answer: 0
            },
            {
                q: "4. Peristiwa luar negeri tahun 1905 yang membakar rasa percaya diri bangsa-bangsa Asia bahwa bangsa kulit putih dapat dikalahkan adalah...",
                options: [
                    "Kemenangan Jepang atas Rusia",
                    "Revolusi Industri di Inggris",
                    "Perang Dunia Pertama",
                    "Kemerdekaan Filipina dari Spanyol"
                ],
                answer: 0
            },
            {
                q: "5. Organisasi politik pertama di Indonesia yang secara berani mengusung slogan radikal 'Indie voor Indiers' adalah...",
                options: ["Budi Utomo", "Sarekat Islam", "Indische Partij", "Parindra"],
                answer: 2
            },
            {
                q: "6. Asas perjuangan Mahatma Gandhi di India yang menginspirasi pejuang Indonesia untuk menolak bekerja sama dengan pemerintah kolonial dinamakan...",
                options: ["Ahimsa & Satyagraha", "San Min Chu I", "Swadeshi & Ahimsa", "Non-Kooperasi"],
                answer: 2
            },
            {
                q: "7. Tiga Serangkai pendiri Indische Partij terdiri dari tokoh-tokoh berikut, KECUALI...",
                options: ["E.F.E. Douwes Dekker", "Dr. Cipto Mangunkusumo", "Suwardi Suryaningrat", "H.O.S. Cokroaminoto"],
                answer: 3
            },
            {
                q: "8. Perbedaan mendasar perjuangan rakyat Indonesia sebelum dan sesudah tahun 1908 terletak pada...",
                options: [
                    "Sebelum 1908 bersifat kedaerahan fisik, sesudah 1908 bersifat nasional dan terorganisir",
                    "Sebelum 1908 dipimpin kaum terpelajar, sesudah 1908 dipimpin oleh raja",
                    "Sebelum 1908 menggunakan pers, sesudah 1908 menggunakan perang gerilya",
                    "Sebelum 1908 berazaskan diplomasi, sesudah 1908 bersifat pasif"
                ],
                answer: 0
            },
            {
                q: "9. Kongres Pemuda II tanggal 28 Oktober 1928 menghasilkan ikrar bersejarah Sumpah Pemuda yang menegaskan kesatuan dalam hal...",
                options: [
                    "Tanah air, Bangsa, dan Bahasa",
                    "Agama, Suku, dan Kebudayaan",
                    "Partai, Pemimpin, dan Wilayah",
                    "Pendidikan, Ekonomi, dan Hukum"
                ],
                answer: 0
            },
            {
                q: "10. Tiga ajaran utama 'San Min Chu I' yang dicetuskan oleh Dr. Sun Yat Sen dalam Revolusi Tiongkok 1911 meliputi...",
                options: [
                    "Nasionalisme, Demokrasi, Kesejahteraan Rakyat",
                    "Sosialisme, Kapitalisme, Liberalisme",
                    "Kemerdekaan, Kesetaraan, Persaudaraan",
                    "Monarki, Militerisme, Feodalisme"
                ],
                answer: 0
            },
            {
                q: "11. Organisasi Muhammadiyah didirikan di Yogyakarta pada tahun 1912 oleh K.H. Ahmad Dahlan dengan fokus utama di bidang...",
                options: [
                    "Pendidikan, sosial kemasyarakatan, dan pemurnian Islam",
                    "Perjuangan politik radikal dan pemberontakan fisik",
                    "Perdagangan rempah-rempah di kawasan pesisir",
                    "Pengiriman perwakilan ke Volksraad"
                ],
                answer: 0
            },
            {
                q: "12. Tokoh ulama besar yang memelopori berdirinya Nahdlatul Ulama (NU) di Jombang pada tahun 1926 adalah...",
                options: ["K.H. Hasyim Asy'ari", "K.H. Ahmad Dahlan", "H. Samanhudi", "H.O.S. Cokroaminoto"],
                answer: 0
            },
            {
                q: "13. Tujuan utama pendirian Partai Nasional Indonesia (PNI) oleh Ir. Soekarno pada tahun 1927 adalah...",
                options: [
                    "Mencapai Indonesia Merdeka penuh melalui perjuangan non-kooperasi",
                    "Membantu pemerintah Belanda mengumpulkan pajak rakyat",
                    "Mengirimkan utusan sebanyak-banyaknya ke dewan Volksraad",
                    "Membatasi hak-hak buruh dan petani pribumi"
                ],
                answer: 0
            },
            {
                q: "14. Taktik 'Non-Kooperasi' yang diterapkan oleh organisasi radikal seperti PNI dan Perhimpunan Indonesia berarti...",
                options: [
                    "Menolak bekerja sama dalam bentuk apapun dengan pemerintah kolonial Belanda",
                    "Selalu menuruti aturan dewan Volksraad Belanda",
                    "Melakukan negosiasi rahasia dengan Ratu Belanda",
                    "Membantu tentara kolonial dalam peperangan luar negeri"
                ],
                answer: 0
            },
            {
                q: "15. Sarekat Dagang Islam (SDI) awalnya didirikan di Surakarta pada tahun 1911 oleh H. Samanhudi dengan tujuan...",
                options: [
                    "Melindungi pedagang batik pribumi Muslim dari persaingan pedagang monopoli",
                    "Mendirikan sekolah kedokteran untuk anak-anak bangsawan",
                    "Menerbitkan surat kabar berbahasa Belanda",
                    "Menggalang kekuatan militer bersenjata"
                ],
                answer: 0
            },
            {
                q: "16. Alasan H.O.S. Cokroaminoto mengubah Sarekat Dagang Islam (SDI) menjadi Sarekat Islam (SI) pada tahun 1912 adalah...",
                options: [
                    "Agar keanggotaan organisasi tidak terbatas pada pedagang dan menjadi lebih luas",
                    "Karena dilarang keras oleh pemerintah kolonial Belanda",
                    "Agar dapat bergabung menjadi tentara cadangan Belanda",
                    "Karena seluruh pedagang batik mengalami bangkrut"
                ],
                answer: 0
            },
            {
                q: "17. Organisasi mahasiswa Indonesia di Negeri Belanda yang memelopori penggunan istilah 'Indonesia' secara internasional adalah...",
                options: ["Perhimpunan Indonesia", "Budi Utomo", "Gerindo", "Partindo"],
                answer: 0
            },
            {
                q: "18. Karakteristik perjuangan organisasi pergerakan pada periode moderat (tahun 1930-an) ditandai oleh...",
                options: [
                    "Penggunaan taktik kooperasi dan memanfaatkan dewan Volksraad",
                    "Pemberontakan persenjataan secara massal",
                    "Penolakan terhadap semua bentuk pendidikan sekolah",
                    "Pembubaran seluruh partai politik keagamaan"
                ],
                answer: 0
            },
            {
                q: "19. Gabungan Politik Indonesia (GAPI) yang dibentuk tahun 1939 menuntut pemerintah Belanda dengan semboyan utama...",
                options: ["Indonesia Berparlemen", "Indonesia Menggugat", "Indie voor Indiers", "Merdeka Atau Mati"],
                answer: 0
            },
            {
                q: "20. Akhir dari periode kekuasaan kolonial Belanda di Indonesia ditandai dengan penyerahan tanpa syarat kepada militer Jepang di Kalijati pada tanggal...",
                options: ["8 Maret 1942", "17 Agustus 1945", "20 Mei 1908", "28 Oktober 1928"],
                answer: 0
            }
        ];

        /* ==================== GLOBAL APP STATE ==================== */
        let visitedModules = new Set(['beranda']);
        let currentQuizIndex = 0;
        let userQuizAnswers = new Array(quizQuestions.length).fill(null);
        let gameTimerInterval = null;
        let gameSeconds = 0;
        let gameAttempts = 0;
        let gameMatches = 0;
        let flippedCards = [];
        let isGameProcessing = false;

        /* ==================== NAVIGATION LOGIC ==================== */
        function switchTab(tabId) {
            // Hide all views
            const views = document.querySelectorAll('.view-section');
            views.forEach(v => v.classList.remove('active'));

            // Show selected view
            const target = document.getElementById(`view-${tabId}`);
            if (target) {
                target.classList.add('active');
            }

            // Update Nav Styling
            const navBtns = document.querySelectorAll('.nav-btn');
            navBtns.forEach(btn => {
                btn.classList.remove('bg-amber-200/80', 'text-brand-darkred', 'font-bold');
            });
            const activeNav = document.getElementById(`nav-${tabId}`);
            if (activeNav) {
                activeNav.classList.add('bg-amber-200/80', 'text-brand-darkred', 'font-bold');
            }

            // Track Progress
            visitedModules.add(tabId);
            updateProgressTracker();

            // Lazy Load Game or Quiz setup if needed
            if (tabId === 'game' && gameMatches === 0) {
                initGame();
            } else if (tabId === 'organisasi') {
                renderOrganizations(organizations);
            } else if (tabId === 'video') {
                renderVideos();
            } else if (tabId === 'evaluasi') {
                renderQuestion();
            }

            window.scrollTo({ top: 0, behavior: 'smooth' });
        }

        function toggleMobileMenu() {
            const menu = document.getElementById('mobile-menu');
            menu.classList.toggle('hidden');
        }

        function updateProgressTracker() {
            const count = visitedModules.size;
            const pct = Math.min((count / 6) * 100, 100);
            document.getElementById('progress-text').textContent = `${count} / 6 Modul Dikunjungi`;
            document.getElementById('progress-bar-inner').style.width = `${pct}%`;
        }

        /* ==================== MATERI LOGIC ==================== */
        function switchMateriSub(subId) {
            const contents = document.querySelectorAll('.materi-content');
            contents.forEach(c => c.classList.add('hidden'));

            const selected = document.getElementById(subId);
            if (selected) selected.classList.remove('hidden');

            const subBtns = document.querySelectorAll('.subtab-btn');
            subBtns.forEach(b => {
                b.classList.remove('bg-brand-red', 'text-white', 'shadow-sm');
                b.classList.add('bg-white', 'text-slate-700');
            });

            const activeBtn = document.getElementById(`subtab-${subId}`);
            if (activeBtn) {
                activeBtn.classList.remove('bg-white', 'text-slate-700');
                activeBtn.classList.add('bg-brand-red', 'text-white', 'shadow-sm');
            }
        }

        const timelineDetails = {
            '1908': {
                title: "1908: Berdirinya Budi Utomo",
                desc: "Diinisiasi oleh para mahasiswa STOVIA seperti Soetomo dan Gunawan Mangunkusumo di bawah arahan Dr. Wahidin Sudirohusodo. Tanggal 20 Mei kini diperingati sebagai Hari Kebangkitan Nasional."
            },
            '1912': {
                title: "1912: Kemunculan SI, IP, dan Muhammadiyah",
                desc: "Sarekat Dagang Islam berubah menjadi Sarekat Islam (SI), Indische Partij didirikan oleh Tiga Serangkai, dan K.H. Ahmad Dahlan mendirikan Muhammadiyah di Yogyakarta."
            },
            '1918': {
                title: "1918: Pembentukan Volksraad",
                desc: "Pemerintah Hindia Belanda meresmikan dewan perwakilan Volksraad (Dewan Rakyat). Meskipun memiliki kekuasaan terbatas, Volksraad dimanfaatkan para tokoh untuk diplomasi politik."
            },
            '1927': {
                title: "1927: Pendirian PNI oleh Ir. Soekarno",
                desc: "Partai Nasional Indonesia (PNI) berdiri di Bandung dengan asas Marhaenisme dan taktik non-kooperasi radikal menuntut Indonesia Merdeka penuh."
            },
            '1928': {
                title: "1928: Kongres Pemuda II (Sumpah Pemuda)",
                desc: "Pertemuan bersejarah para pemuda seluruh Nusantara pada 28 Oktober 1928 yang mengikrarkan Sumpah Pemuda serta dikumandangkannya lagu Indonesia Raya."
            },
            '1942': {
                title: "1942: Pendudukan Militer Jepang",
                desc: "Belanda menyerah tanpa syarat di Kalijati pada 8 Maret 1942. Kekuasaan kolonial Hindia Belanda berakhir dan digantikan oleh masa pendudukan militer Jepang."
            }
        };

        function openTimelineModal(year) {
            const data = timelineDetails[year];
            if (!data) return;

            const modalBody = document.getElementById('app-modal-body');
            modalBody.innerHTML = `
                <div class="space-y-4">
                    <span class="text-xs font-black bg-amber-100 text-amber-800 px-3 py-1 rounded-full border border-amber-300 uppercase">Peristiwa Sejarah</span>
                    <h3 class="text-2xl font-bold text-brand-darkred font-serif">${data.title}</h3>
                    <p class="text-slate-700 leading-relaxed text-sm sm:text-base">${data.desc}</p>
                    <div class="pt-4 flex justify-end">
                        <button onclick="closeAppModal()" class="px-5 py-2.5 bg-brand-red text-white font-bold rounded-xl text-sm hover:bg-brand-darkred transition">
                            Tutup
                        </button>
                    </div>
                </div>
            `;
            document.getElementById('app-modal').classList.remove('hidden');
        }

        /* ==================== ORGANISASI LOGIC ==================== */
        function renderOrganizations(data) {
            const container = document.getElementById('org-grid-container');
            if (!container) return;

            if (data.length === 0) {
                container.innerHTML = `
                    <div class="col-span-full text-center py-12 text-slate-500 bg-white rounded-2xl border border-amber-200">
                        <i class="fa-solid fa-magnifying-glass text-4xl text-amber-300 mb-3"></i>
                        <p class="font-bold">Organisasi tidak ditemukan</p>
                        <p class="text-xs">Coba kata kunci pencarian atau filter lain.</p>
                    </div>
                `;
                return;
            }

            container.innerHTML = data.map(org => `
                <div onclick="openOrgModal('${org.id}')" class="bg-white rounded-2xl p-6 border border-amber-200 shadow-sm hover:shadow-xl transition transform hover:-translate-y-1 cursor-pointer flex flex-col justify-between group">
                    <div>
                        <div class="flex items-center justify-between mb-4">
                            <div class="w-14 h-14 rounded-2xl bg-amber-50 border border-amber-200 flex items-center justify-center group-hover:scale-105 transition">
                                ${org.badgeSvg}
                            </div>
                            <span class="text-xs font-black bg-amber-100 text-amber-900 px-3 py-1 rounded-full border border-amber-300">
                                ${org.year}
                            </span>
                        </div>
                        <h3 class="text-xl font-bold text-slate-900 group-hover:text-brand-red transition mb-1 font-serif">${org.name}</h3>
                        <p class="text-xs text-amber-800 font-medium mb-3">Kategori: Masa ${org.category}</p>
                        <p class="text-slate-600 text-xs line-clamp-3 leading-relaxed mb-4">${org.summary}</p>
                    </div>
                    <div class="pt-3 border-t border-amber-100 flex items-center justify-between text-xs font-bold text-brand-darkred">
                        <span>Lihat Detail</span>
                        <i class="fa-solid fa-arrow-right group-hover:translate-x-1 transition"></i>
                    </div>
                </div>
            `).join('');
        }

        function filterOrganizations() {
            const query = document.getElementById('org-search-input').value.toLowerCase().trim();
            const activeFilterBtn = document.querySelector('.org-filter-btn.bg-brand-red');
            const category = activeFilterBtn ? activeFilterBtn.dataset.filter : 'all';

            const filtered = organizations.filter(org => {
                const matchesQuery = org.name.toLowerCase().includes(query) ||
                                     org.founders.toLowerCase().includes(query) ||
                                     org.goals.toLowerCase().includes(query);
                const matchesCategory = (category === 'all') || (org.category === category);
                return matchesQuery && matchesCategory;
            });

            renderOrganizations(filtered);
        }

        function setOrgFilter(cat) {
            const filterBtns = document.querySelectorAll('.org-filter-btn');
            filterBtns.forEach(btn => {
                btn.classList.remove('bg-brand-red', 'text-white', 'shadow-sm');
                btn.classList.add('bg-white', 'text-slate-700');
            });

            const targetBtn = document.querySelector(`.org-filter-btn[data-filter="${cat}"]`);
            if (targetBtn) {
                targetBtn.classList.remove('bg-white', 'text-slate-700');
                targetBtn.classList.add('bg-brand-red', 'text-white', 'shadow-sm');
            }

            filterOrganizations();
        }

        function openOrgModal(orgId) {
            const org = organizations.find(o => o.id === orgId);
            if (!org) return;

            const modalBody = document.getElementById('app-modal-body');
            modalBody.innerHTML = `
                <div class="space-y-6">
                    <div class="flex items-center gap-4 border-b border-amber-200 pb-4">
                        <div class="w-16 h-16 rounded-2xl bg-amber-50 border border-amber-300 flex items-center justify-center">
                            ${org.badgeSvg}
                        </div>
                        <div>
                            <span class="text-xs font-bold text-amber-800 uppercase tracking-widest bg-amber-100 px-2.5 py-0.5 rounded-full border border-amber-300">Tahun Berdiri: ${org.year}</span>
                            <h3 class="text-2xl font-bold text-brand-darkred font-serif mt-1">${org.name}</h3>
                        </div>
                    </div>

                    <div class="space-y-4 text-xs sm:text-sm text-slate-700">
                        <div>
                            <strong class="text-slate-900 block font-bold text-base mb-1"><i class="fa-solid fa-users text-amber-600 mr-2"></i>Tokoh Penting & Pendiri:</strong>
                            <p class="bg-amber-50/70 p-3 rounded-xl border border-amber-200 leading-relaxed">${org.founders}</p>
                        </div>

                        <div>
                            <strong class="text-slate-900 block font-bold text-base mb-1"><i class="fa-solid fa-bullseye text-amber-600 mr-2"></i>Tujuan Utama:</strong>
                            <p class="bg-amber-50/70 p-3 rounded-xl border border-amber-200 leading-relaxed">${org.goals}</p>
                        </div>

                        <div>
                            <strong class="text-slate-900 block font-bold text-base mb-1"><i class="fa-solid fa-star text-amber-600 mr-2"></i>Peran dalam Pergerakan Nasional:</strong>
                            <p class="bg-amber-50/70 p-3 rounded-xl border border-amber-200 leading-relaxed">${org.role}</p>
                        </div>
                    </div>

                    <div class="pt-2 flex justify-end">
                        <button onclick="closeAppModal()" class="px-6 py-2.5 bg-brand-red text-white font-bold rounded-xl text-sm hover:bg-brand-darkred transition">
                            Tutup
                        </button>
                    </div>
                </div>
            `;
            document.getElementById('app-modal').classList.remove('hidden');
        }

        /* ==================== VIDEO LOGIC ==================== */
        function renderVideos() {
            const container = document.getElementById('video-grid-container');
            if (!container) return;

            container.innerHTML = videos.map((v, i) => `
                <div class="bg-white rounded-2xl border border-amber-200 shadow-sm overflow-hidden flex flex-col justify-between hover:shadow-lg transition group">
                    <div class="relative bg-slate-900 aspect-video flex items-center justify-center cursor-pointer overflow-hidden" onclick="playVideoModal('${v.embedUrl}', '${v.title}')">
                        <div class="absolute inset-0 bg-gradient-to-t from-slate-950/80 via-transparent to-transparent z-10"></div>
                        <i class="fa-solid fa-circle-play text-5xl text-amber-400 group-hover:scale-110 transition z-20 shadow-lg"></i>
                        <span class="absolute top-3 left-3 z-20 text-[10px] font-bold uppercase bg-amber-500 text-slate-950 px-2.5 py-1 rounded-md shadow">
                            ${v.badge}
                        </span>
                    </div>
                    <div class="p-5 flex-grow flex flex-col justify-between">
                        <div>
                            <h3 class="font-bold text-slate-900 text-base mb-2 group-hover:text-brand-red transition font-serif">${v.title}</h3>
                            <p class="text-slate-600 text-xs leading-relaxed mb-4">${v.desc}</p>
                        </div>
                        <button onclick="playVideoModal('${v.embedUrl}', '${v.title}')" class="w-full py-2.5 bg-amber-100 hover:bg-brand-red hover:text-white text-brand-darkred font-bold rounded-xl text-xs transition flex items-center justify-center gap-2">
                            <i class="fa-solid fa-play"></i> Tonton Video
                        </button>
                    </div>
                </div>
            `).join('');
        }

        function playVideoModal(url, title) {
            const modalBody = document.getElementById('app-modal-body');
            modalBody.innerHTML = `
                <div class="space-y-4">
                    <h3 class="text-xl font-bold text-brand-darkred font-serif">${title}</h3>
                    <div class="aspect-video w-full rounded-2xl overflow-hidden bg-black border border-amber-300 shadow">
                        <iframe class="w-full h-full" src="${url}" title="${title}" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
                    </div>
                    <div class="flex justify-end pt-2">
                        <button onclick="closeAppModal()" class="px-5 py-2 bg-brand-red text-white font-bold rounded-xl text-sm hover:bg-brand-darkred transition">
                            Tutup
                        </button>
                    </div>
                </div>
            `;
            document.getElementById('app-modal').classList.remove('hidden');
        }

        /* ==================== GAME LOGIC ==================== */
        function initGame() {
            clearInterval(gameTimerInterval);
            gameSeconds = 0;
            gameAttempts = 0;
            gameMatches = 0;
            flippedCards = [];
            isGameProcessing = false;

            document.getElementById('game-attempts').textContent = '0';
            document.getElementById('game-matches').textContent = '0 / 8';
            document.getElementById('game-timer').textContent = '00:00';

            // Select 8 organizations for memory pairs
            const selectedOrgs = organizations.slice(0, 8);
            let deck = [];
            selectedOrgs.forEach(org => {
                deck.push({ id: org.id, name: org.name, svg: org.badgeSvg });
                deck.push({ id: org.id, name: org.name, svg: org.badgeSvg });
            });

            // Shuffle Deck
            deck.sort(() => Math.random() - 0.5);

            const board = document.getElementById('game-board');
            board.innerHTML = deck.map((item, idx) => `
                <div class="game-card perspective-1000 h-32 cursor-pointer" onclick="flipGameCard(this, '${item.id}')" data-card-id="${item.id}">
                    <div class="card-inner relative w-full h-full transform-style-3d rounded-2xl shadow-md">
                        <!-- Front (Covered) -->
                        <div class="absolute inset-0 bg-gradient-to-br from-amber-700 to-brand-darkred rounded-2xl border-2 border-amber-400 flex items-center justify-center text-amber-200 backface-hidden">
                            <i class="fa-solid fa-shield-halved text-3xl opacity-80"></i>
                        </div>
                        <!-- Back (Revealed) -->
                        <div class="absolute inset-0 bg-white rounded-2xl border-2 border-amber-400 flex flex-col items-center justify-center p-2 text-center rotate-y-180 backface-hidden">
                            <div class="w-10 h-10 flex items-center justify-center mb-1">
                                ${item.svg}
                            </div>
                            <span class="text-[11px] font-extrabold text-slate-800 leading-tight font-serif">${item.name}</span>
                        </div>
                    </div>
                </div>
            `).join('');

            // Start Timer
            gameTimerInterval = setInterval(() => {
                gameSeconds++;
                const mins = String(Math.floor(gameSeconds / 60)).padStart(2, '0');
                const secs = String(gameSeconds % 60).padStart(2, '0');
                document.getElementById('game-timer').textContent = `${mins}:${secs}`;
            }, 1000);
        }

        function flipGameCard(cardEl, id) {
            if (isGameProcessing) return;
            const inner = cardEl.querySelector('.card-inner');
            if (inner.classList.contains('rotate-y-180') || cardEl.classList.contains('matched')) return;

            inner.classList.add('rotate-y-180');
            flippedCards.push({ element: cardEl, id: id });

            if (flippedCards.length === 2) {
                gameAttempts++;
                document.getElementById('game-attempts').textContent = gameAttempts;
                isGameProcessing = true;

                const [c1, c2] = flippedCards;
                if (c1.id === c2.id) {
                    // Match found
                    c1.element.classList.add('matched');
                    c2.element.classList.add('matched');
                    gameMatches++;
                    document.getElementById('game-matches').textContent = `${gameMatches} / 8`;
                    flippedCards = [];
                    isGameProcessing = false;

                    if (gameMatches === 8) {
                        clearInterval(gameTimerInterval);
                        setTimeout(() => {
                            document.getElementById('win-attempts').textContent = gameAttempts;
                            document.getElementById('win-time').textContent = document.getElementById('game-timer').textContent;
                            document.getElementById('game-win-banner').classList.remove('hidden');
                        }, 500);
                    }
                } else {
                    // Not a match
                    setTimeout(() => {
                        c1.element.querySelector('.card-inner').classList.remove('rotate-y-180');
                        c2.element.querySelector('.card-inner').classList.remove('rotate-y-180');
                        flippedCards = [];
                        isGameProcessing = false;
                    }, 900);
                }
            }
        }

        /* ==================== EVALUASI (QUIZ) LOGIC ==================== */
        function renderQuestion() {
            const q = quizQuestions[currentQuizIndex];
            document.getElementById('quiz-question-number').textContent = `Soal ${currentQuizIndex + 1} dari ${quizQuestions.length}`;
            document.getElementById('quiz-question-text').textContent = q.q;

            const optionsContainer = document.getElementById('quiz-options-container');
            const selectedAnswer = userQuizAnswers[currentQuizIndex];

            optionsContainer.innerHTML = q.options.map((opt, i) => {
                const isSelected = selectedAnswer === i;
                return `
                    <label onclick="selectQuizOption(${i})" class="flex items-center gap-3 p-4 rounded-xl border transition cursor-pointer ${
                        isSelected 
                        ? 'bg-amber-100 border-amber-500 font-bold text-amber-950 shadow-sm' 
                        : 'bg-slate-50 border-slate-200 hover:bg-amber-50 text-slate-700'
                    }">
                        <input type="radio" name="quiz-opt" value="${i}" ${isSelected ? 'checked' : ''} class="w-4 h-4 text-brand-red focus:ring-brand-gold">
                        <span class="text-xs sm:text-sm">${String.fromCharCode(65 + i)}. ${opt}</span>
                    </label>
                `;
            }).join('');

            // Controls state
            document.getElementById('quiz-prev-btn').disabled = (currentQuizIndex === 0);

            const nextBtn = document.getElementById('quiz-next-btn');
            if (currentQuizIndex === quizQuestions.length - 1) {
                nextBtn.innerHTML = `Selesai <i class="fa-solid fa-check ml-1"></i>`;
                nextBtn.className = "px-6 py-2.5 bg-emerald-600 hover:bg-emerald-700 text-white font-bold rounded-xl text-sm transition flex items-center gap-2";
            } else {
                nextBtn.innerHTML = `Berikutnya <i class="fa-solid fa-arrow-right ml-1"></i>`;
                nextBtn.className = "px-6 py-2.5 bg-brand-red hover:bg-brand-darkred text-white font-bold rounded-xl text-sm transition flex items-center gap-2";
            }
        }

        function selectQuizOption(optIdx) {
            userQuizAnswers[currentQuizIndex] = optIdx;
            renderQuestion();
        }

        function nextQuestion() {
            if (currentQuizIndex < quizQuestions.length - 1) {
                currentQuizIndex++;
                renderQuestion();
            } else {
                finishQuiz();
            }
        }

        function prevQuestion() {
            if (currentQuizIndex > 0) {
                currentQuizIndex--;
                renderQuestion();
            }
        }

        function finishQuiz() {
            let correctCount = 0;
            quizQuestions.forEach((q, idx) => {
                if (userQuizAnswers[idx] === q.answer) {
                    correctCount++;
                }
            });

            const incorrectCount = quizQuestions.length - correctCount;
            const finalScore = Math.round((correctCount / quizQuestions.length) * 100);

            document.getElementById('quiz-container').classList.add('hidden');
            document.getElementById('quiz-result-container').classList.remove('hidden');

            document.getElementById('result-correct').textContent = correctCount;
            document.getElementById('result-incorrect').textContent = incorrectCount;
            document.getElementById('result-score').textContent = finalScore;

            const msgBox = document.getElementById('result-message-box');
            if (finalScore >= 90) {
                msgBox.className = "p-4 rounded-xl text-xs sm:text-sm font-medium bg-emerald-100 text-emerald-900 border border-emerald-300";
                msgBox.innerHTML = `<strong>Luar Biasa! (Nilai: ${finalScore})</strong><br>Pemahamanmu terhadap materi Pergerakan Nasional Indonesia sangat unggul dan komprehensif.`;
            } else if (finalScore >= 75) {
                msgBox.className = "p-4 rounded-xl text-xs sm:text-sm font-medium bg-amber-100 text-amber-900 border border-amber-300";
                msgBox.innerHTML = `<strong>Sangat Baik! (Nilai: ${finalScore})</strong><br>Pemahamanmu sudah memadai. Beberapa bagian kecil masih dapat ditingkatkan lagi melalui ulasan materi.`;
            } else if (finalScore >= 60) {
                msgBox.className = "p-4 rounded-xl text-xs sm:text-sm font-medium bg-orange-100 text-orange-900 border border-orange-300";
                msgBox.innerHTML = `<strong>Cukup Baik (Nilai: ${finalScore})</strong><br>Kamu sudah memahami beberapa konsep dasar. Pelajari kembali halaman organisasi dan timeline sejarah.`;
            } else {
                msgBox.className = "p-4 rounded-xl text-xs sm:text-sm font-medium bg-rose-100 text-rose-900 border border-rose-300";
                msgBox.innerHTML = `<strong>Perlu Ditingkatkan (Nilai: ${finalScore})</strong><br>Jangan berkecil hati. Luangkan waktu untuk membaca ulang materi pembelajaran dan ulangi evaluasi ini.`;
            }
        }

        function resetQuiz() {
            currentQuizIndex = 0;
            userQuizAnswers = new Array(quizQuestions.length).fill(null);
            document.getElementById('quiz-result-container').classList.add('hidden');
            document.getElementById('quiz-container').classList.remove('hidden');
            renderQuestion();
        }

        function closeAppModal() {
            document.getElementById('app-modal').classList.add('hidden');
        }

        window.onload = function() {
            renderOrganizations(organizations);
            renderVideos();
            renderQuestion();
            updateProgressTracker();
        };
    </script>
</body>
</html>
