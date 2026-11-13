<!DOCTYPE html>
<html lang="en" class="dark scroll-smooth">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta name="description" content="ODONO AI — One AI. Unlimited Possibilities. Create, edit, generate, develop and explore everything with ODONO AI.">
    <title>ODONO AI | One AI. Unlimited Possibilities.</title>

    <!-- Google Fonts: Plus Jakarta Sans & Space Grotesk & JetBrains Mono -->
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=JetBrains+Mono:wght@400;500;600&family=Plus+Jakarta+Sans:wght@400;500;600;700&family=Space+Grotesk:wght@600;700&display=swap" rel="stylesheet">

    <!-- Font Awesome 6 -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.1/css/all.min.css">

    <!-- Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    <script>
        tailwind.config = {
            darkMode: 'class',
            theme: {
                extend: {
                    fontFamily: {
                        sans: ['Plus Jakarta Sans', 'sans-serif'],
                        display: ['Space Grotesk', 'sans-serif'],
                        mono: ['JetBrains Mono', 'monospace'],
                    },
                    colors: {
                        pureBlack: '#000000',
                        deepNavy: '#030816',
                        panelNavy: '#060F24',
                        electricBlue: '#0088FF',
                        cyberBlue: '#00D4FF',
                    }
                }
            }
        }
    </script>

    <!-- Three.js for 3D Interactive Neural Core -->
    <script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js"></script>

    <style>
        :root {
            --accent-primary: #0088FF;
            --accent-secondary: #00D4FF;
            --bg-main: #000000;
            --bg-navy: #040B1A;
        }

        body {
            background-color: var(--bg-main);
            color: #F8FAFC;
            overflow-x: hidden;
        }

        /* Custom Scrollbar */
        ::-webkit-scrollbar {
            width: 7px;
            height: 7px;
        }
        ::-webkit-scrollbar-track {
            background: #000000;
        }
        ::-webkit-scrollbar-thumb {
            background: linear-gradient(180deg, var(--accent-primary), var(--accent-secondary));
            border-radius: 9999px;
        }

        /* Glassmorphism Panels - Pure Black & Deep Navy Blue */
        .odono-glass {
            background: linear-gradient(145deg, rgba(6, 15, 36, 0.78) 0%, rgba(1, 4, 12, 0.9) 100%);
            backdrop-filter: blur(18px);
            -webkit-backdrop-filter: blur(18px);
            border: 1px solid rgba(0, 136, 255, 0.22);
            box-shadow: 0 10px 40px rgba(0, 0, 0, 0.85), inset 0 1px 0 rgba(0, 212, 255, 0.12);
        }

        .odono-card {
            background: linear-gradient(160deg, rgba(7, 19, 46, 0.65) 0%, rgba(2, 5, 14, 0.92) 100%);
            backdrop-filter: blur(14px);
            border: 1px solid rgba(0, 136, 255, 0.18);
            transition: all 0.35s cubic-bezier(0.22, 1, 0.36, 1);
        }

        .odono-card:hover {
            border-color: var(--accent-secondary);
            transform: translateY(-4px);
            box-shadow: 0 14px 36px -6px rgba(0, 136, 255, 0.32), 0 0 22px rgba(0, 212, 255, 0.15);
        }

        /* Electric Blue Gradients & Glowing Buttons */
        .text-electric {
            background: linear-gradient(135deg, #FFFFFF 0%, var(--accent-secondary) 48%, var(--accent-primary) 100%);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
        }

        .btn-electric {
            background: linear-gradient(135deg, var(--accent-primary) 0%, #0055CC 100%);
            box-shadow: 0 0 22px rgba(0, 136, 255, 0.45), inset 0 1px 0 rgba(255, 255, 255, 0.25);
            transition: all 0.25s ease;
        }

        .btn-electric:hover:not(:disabled) {
            background: linear-gradient(135deg, var(--accent-secondary) 0%, var(--accent-primary) 100%);
            box-shadow: 0 0 32px rgba(0, 212, 255, 0.7);
            transform: translateY(-1px);
        }

        .btn-electric:disabled {
            opacity: 0.5;
            cursor: not-allowed;
        }

        /* Futuristic Loader Ring */
        .neural-loader {
            width: 36px;
            height: 36px;
            border: 3px solid rgba(0, 136, 255, 0.2);
            border-top-color: var(--accent-secondary);
            border-right-color: var(--accent-primary);
            border-radius: 50%;
            animation: spin 0.8s linear infinite;
        }

        @keyframes spin {
            to { transform: rotate(360deg); }
        }

        /* Grid Background Pattern */
        .cyber-grid {
            background-size: 48px 48px;
            background-image: 
                linear-gradient(to right, rgba(0, 136, 255, 0.06) 1px, transparent 1px),
                linear-gradient(to bottom, rgba(0, 136, 255, 0.06) 1px, transparent 1px);
        }

        #hero-3d-canvas {
            position: fixed;
            inset: 0;
            width: 100%;
            height: 100%;
            z-index: -1;
            pointer-events: none;
        }

        /* Markdown-like code block formatting */
        .ai-output pre {
            background: #020612;
            border: 1px solid rgba(0, 136, 255, 0.3);
            border-radius: 0.75rem;
            padding: 1rem;
            overflow-x: auto;
            font-family: 'JetBrains Mono', monospace;
            font-size: 0.82rem;
            margin: 0.75rem 0;
            color: #93C5FD;
        }
    </style>
</head>
<body class="antialiased selection:bg-blue-500/30 selection:text-cyan-200 cyber-grid">

    <!-- 3D Neural Core Canvas -->
    <canvas id="hero-3d-canvas"></canvas>

    <!-- Ambient Deep Navy & Electric Blue Glows -->
    <div class="fixed top-[-15%] left-[10%] w-[42vw] h-[42vw] rounded-full bg-blue-600/15 blur-[140px] pointer-events-none z-[-1]"></div>
    <div class="fixed bottom-[-15%] right-[5%] w-[38vw] h-[38vw] rounded-full bg-cyan-500/10 blur-[140px] pointer-events-none z-[-1]"></div>

    <!-- Notification Toast (Non-blocking UI feedback) -->
    <div id="toast-container" class="fixed bottom-5 right-5 z-50 flex flex-col gap-2 pointer-events-none"></div>

    <!-- ========================================== -->
    <!-- TOP NAVIGATION BAR                         -->
    <!-- ========================================== -->
    <header class="sticky top-0 z-40 border-b border-blue-500/20 bg-black/85 backdrop-blur-xl">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 h-16 flex items-center justify-between gap-4">
            <!-- Dynamic Brand Logo & Name -->
            <button onclick="switchView('home')" class="flex items-center gap-3 text-left group">
                <div id="brand-logo-box" class="w-10 h-10 rounded-xl btn-electric flex items-center justify-center text-white font-display font-bold text-lg">
                    <i class="fa-solid fa-atom"></i>
                </div>
                <div>
                    <span id="brand-name-header" class="font-display font-bold text-xl tracking-wide text-white block leading-none">
                        ODONO <span class="text-cyan-400">AI</span>
                    </span>
                    <span id="brand-tagline-header" class="text-[10px] tracking-widest uppercase text-blue-400/90 font-medium">
                        One AI. Unlimited Possibilities.
                    </span>
                </div>
            </button>

            <!-- Primary Nav Links -->
            <nav class="hidden lg:flex items-center gap-1.5 bg-[#040B1A] p-1.5 rounded-xl border border-blue-500/20">
                <button onclick="switchView('home')" data-nav="home" class="nav-tab px-3.5 py-1.5 rounded-lg text-xs font-semibold text-white bg-blue-600/30 border border-blue-400/40 transition-all">
                    Home
                </button>
                <button onclick="switchView('studio')" data-nav="studio" class="nav-tab px-3.5 py-1.5 rounded-lg text-xs font-semibold text-slate-300 hover:text-white transition-all">
                    AI Studios (7)
                </button>
                <button onclick="switchView('dashboard')" data-nav="dashboard" class="nav-tab px-3.5 py-1.5 rounded-lg text-xs font-semibold text-slate-300 hover:text-white transition-all">
                    Dashboard
                </button>
                <button onclick="switchView('pricing')" data-nav="pricing" class="nav-tab px-3.5 py-1.5 rounded-lg text-xs font-semibold text-slate-300 hover:text-white transition-all">
                    Pricing
                </button>
                <button onclick="switchView('about')" data-nav="about" class="nav-tab px-3.5 py-1.5 rounded-lg text-xs font-semibold text-slate-300 hover:text-white transition-all">
                    About Us
                </button>
                <button onclick="switchView('admin')" data-nav="admin" class="nav-tab px-3.5 py-1.5 rounded-lg text-xs font-semibold text-cyan-300 hover:text-white transition-all flex items-center gap-1.5">
                    <i class="fa-solid fa-shield-halved text-[11px]"></i> Admin
                </button>
            </nav>

            <!-- Credits Pill & Quick Launch -->
            <div class="flex items-center gap-3">
                <div onclick="switchView('pricing')" title="Available AI Credits" class="cursor-pointer px-3.5 py-1.5 rounded-xl bg-[#051026] border border-blue-500/35 flex items-center gap-2 hover:border-cyan-400 transition-colors">
                    <i class="fa-solid fa-bolt text-cyan-400 text-xs"></i>
                    <span id="header-credits" class="font-mono text-xs font-bold text-white">250</span>
                    <span class="text-[11px] text-blue-300 hidden sm:inline">Credits</span>
                </div>

                <button onclick="switchView('studio')" class="hidden sm:inline-flex items-center gap-2 px-4 py-2 rounded-xl btn-electric text-white text-xs font-bold">
                    <span>Launch Studio</span>
                    <i class="fa-solid fa-arrow-right"></i>
                </button>

                <!-- Mobile Menu Button -->
                <button id="mobile-nav-toggle" class="lg:hidden w-10 h-10 rounded-xl odono-glass flex items-center justify-center text-blue-300">
                    <i class="fa-solid fa-bars"></i>
                </button>
            </div>
        </div>

        <!-- Mobile Dropdown Drawer -->
        <div id="mobile-nav-drawer" class="hidden lg:hidden border-t border-blue-500/20 bg-black/95 px-4 py-4 space-y-2">
            <button onclick="switchView('home'); toggleMobileNav()" class="w-full text-left px-4 py-2.5 rounded-xl text-sm font-semibold text-white hover:bg-blue-600/20">Home</button>
            <button onclick="switchView('studio'); toggleMobileNav()" class="w-full text-left px-4 py-2.5 rounded-xl text-sm font-semibold text-slate-300 hover:bg-blue-600/20">All 7 AI Studios</button>
            <button onclick="switchView('dashboard'); toggleMobileNav()" class="w-full text-left px-4 py-2.5 rounded-xl text-sm font-semibold text-slate-300 hover:bg-blue-600/20">User Dashboard</button>
            <button onclick="switchView('pricing'); toggleMobileNav()" class="w-full text-left px-4 py-2.5 rounded-xl text-sm font-semibold text-slate-300 hover:bg-blue-600/20">Pricing ($1 Starter)</button>
            <button onclick="switchView('about'); toggleMobileNav()" class="w-full text-left px-4 py-2.5 rounded-xl text-sm font-semibold text-slate-300 hover:bg-blue-600/20">About ODONO AI</button>
            <button onclick="switchView('admin'); toggleMobileNav()" class="w-full text-left px-4 py-2.5 rounded-xl text-sm font-semibold text-cyan-400 hover:bg-blue-600/20">Private Admin Panel</button>
        </div>
    </header>

    <!-- ========================================== -->
    <!-- VIEW 1: HOMEPAGE                           -->
    <!-- ========================================== -->
    <main id="view-home" class="view-section">
        <!-- Hero Section -->
        <section class="relative pt-16 pb-20 sm:pt-24 sm:pb-28 px-4 sm:px-6 lg:px-8 max-w-7xl mx-auto text-center">
            <div class="inline-flex items-center gap-2.5 px-4 py-1.5 rounded-full bg-blue-950/70 border border-blue-400/35 text-cyan-300 text-xs font-semibold mb-8 shadow-lg shadow-blue-500/10">
                <span class="w-2 h-2 rounded-full bg-cyan-400 animate-ping"></span>
                <span>NEXT-GEN MULTI-MODAL NEURAL ENGINE</span>
            </div>

            <h1 id="hero-heading" class="font-display text-4xl sm:text-6xl lg:text-7xl font-bold tracking-tight text-white max-w-5xl mx-auto leading-[1.08]">
                WELCOME TO <span class="text-electric">ODONO AI</span>
            </h1>

            <p id="hero-subtitle" class="font-display text-xl sm:text-2xl font-semibold text-cyan-300 mt-5">
                Your World. Your Creativity. Powered by AI.
            </p>

            <p id="hero-description" class="text-slate-300 text-base sm:text-lg max-w-2xl mx-auto mt-4 leading-relaxed">
                Experience the future of artificial intelligence. Create, edit, generate, develop and explore everything with ODONO AI.
            </p>

            <!-- Hero Buttons -->
            <div class="flex flex-col sm:flex-row items-center justify-center gap-4 mt-10">
                <button onclick="switchView('studio')" class="w-full sm:w-auto px-8 py-4 rounded-2xl btn-electric text-white font-bold text-sm sm:text-base flex items-center justify-center gap-3">
                    <i class="fa-solid fa-grid-2"></i>
                    <span>Explore AI Tools</span>
                </button>
                <button onclick="openToolDirect('chat')" class="w-full sm:w-auto px-8 py-4 rounded-2xl odono-glass border border-blue-400/40 hover:border-cyan-300 text-white font-bold text-sm sm:text-base flex items-center justify-center gap-3 transition-all">
                    <i class="fa-solid fa-sparkles text-cyan-400"></i>
                    <span>Start Creating</span>
                </button>
            </div>

            <!-- Live Platform Telemetry Bar -->
            <div class="grid grid-cols-2 md:grid-cols-4 gap-4 max-w-4xl mx-auto mt-16">
                <div class="odono-glass rounded-2xl p-4 text-center">
                    <div class="font-display text-2xl sm:text-3xl font-bold text-white">7 Studios</div>
                    <div class="text-xs text-blue-300 mt-1">Unified AI Ecosystem</div>
                </div>
                <div class="odono-glass rounded-2xl p-4 text-center">
                    <div class="font-display text-2xl sm:text-3xl font-bold text-cyan-400">&lt; 1.2s</div>
                    <div class="text-xs text-blue-300 mt-1">Neural Inference Latency</div>
                </div>
                <div class="odono-glass rounded-2xl p-4 text-center">
                    <div class="font-display text-2xl sm:text-3xl font-bold text-white">4K / HD</div>
                    <div class="text-xs text-blue-300 mt-1">Visual & Audio Synthesis</div>
                </div>
                <div class="odono-glass rounded-2xl p-4 text-center">
                    <div class="font-display text-2xl sm:text-3xl font-bold text-cyan-400">$1.00</div>
                    <div class="text-xs text-blue-300 mt-1">Starter Access Plan</div>
                </div>
            </div>
        </section>

        <!-- All 7 AI Suites Overview Grid -->
        <section class="py-16 px-4 sm:px-6 lg:px-8 max-w-7xl mx-auto">
            <div class="flex flex-col sm:flex-row sm:items-end justify-between mb-12 gap-4">
                <div>
                    <span class="text-xs font-bold uppercase tracking-widest text-cyan-400">Modular Intelligence Suite</span>
                    <h2 class="font-display text-3xl sm:text-4xl font-bold text-white mt-1">
                        Every AI Superpower in <span class="text-electric">One Platform</span>
                    </h2>
                </div>
                <button onclick="switchView('studio')" class="text-sm font-semibold text-cyan-400 hover:text-white flex items-center gap-2">
                    Open Interactive Workspace <i class="fa-solid fa-arrow-right"></i>
                </button>
            </div>

            <div id="home-tools-grid" class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
                <!-- Dynamically populated from modular tool registry -->
            </div>
        </section>
    </main>

    <!-- ========================================== -->
    <!-- VIEW 2: ALL-IN-ONE AI STUDIO WORKSPACE     -->
    <!-- ========================================== -->
    <section id="view-studio" class="view-section hidden max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-8">
        <div class="grid grid-cols-1 lg:grid-cols-12 gap-6 min-h-[78vh]">
            
            <!-- Left Sidebar: Studio Switcher -->
            <aside class="lg:col-span-3 space-y-2">
                <div class="odono-glass rounded-2xl p-4">
                    <div class="flex items-center justify-between mb-3 px-2">
                        <span class="text-[11px] font-bold uppercase tracking-wider text-blue-300">ODONO AI Suites</span>
                        <span class="text-[10px] px-2 py-0.5 rounded-full bg-blue-500/20 text-cyan-300 border border-blue-400/30">LIVE API</span>
                    </div>
                    <div id="studio-sidebar-list" class="space-y-1.5">
                        <!-- Tool tabs rendered via JS -->
                    </div>
                </div>

                <!-- Security & API Status Card -->
                <div class="odono-glass rounded-2xl p-4 border border-blue-500/20">
                    <div class="flex items-center gap-2.5 text-xs font-semibold text-white mb-2">
                        <i class="fa-solid fa-lock text-cyan-400"></i>
                        <span>Enterprise Security Active</span>
                    </div>
                    <ul class="text-[11px] text-slate-400 space-y-1.5">
                        <li class="flex items-center justify-between">
                            <span>API Key Vault</span>
                            <span class="text-cyan-400 font-mono">ENCRYPTED</span>
                        </li>
                        <li class="flex items-center justify-between">
                            <span>Credit Validation</span>
                            <span class="text-cyan-400 font-mono">ACTIVE</span>
                        </li>
                        <li class="flex items-center justify-between">
                            <span>Rate Limiter</span>
                            <span class="text-blue-400 font-mono">60 RPM</span>
                        </li>
                    </ul>
                </div>
            </aside>

            <!-- Right Main Studio Canvas -->
            <div class="lg:col-span-9 odono-glass rounded-3xl p-5 sm:p-8 flex flex-col justify-between">
                
                <!-- 1. ODONO AI CHAT -->
                <div id="tool-panel-chat" class="tool-panel space-y-5">
                    <div class="flex flex-wrap items-center justify-between gap-3 border-b border-blue-500/20 pb-4">
                        <div>
                            <h2 class="font-display text-2xl font-bold text-white flex items-center gap-2.5">
                                <i class="fa-solid fa-comments text-cyan-400"></i> ODONO AI CHAT
                            </h2>
                            <p class="text-xs text-slate-400 mt-0.5">Ask anything • Math • Coding 
