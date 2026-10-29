index.html
<!DOCTYPE html>
<html lang="fr" class="dark">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no, viewport-fit=cover">
    <title>SYSTEM_CORE v5.0 - Xianxia OS</title>

    <meta name="mobile-web-app-capable" content="yes">
    <meta name="apple-mobile-web-app-capable" content="yes">
    <meta name="apple-mobile-web-app-status-bar-style" content="black-translucent">
    <meta name="theme-color" content="#05070a">

    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Cinzel:wght@600;800;900&family=JetBrains+Mono:wght@400;600;700&family=Plus+Jakarta+Sans:wght@300;400;500;600;700&display=swap" rel="stylesheet">

    <script>
        tailwind.config = {
            darkMode: 'class',
            theme: {
                extend: {
                    colors: {
                        darkBg: '#040609',
                        darkCard: '#0a0e17',
                        darkBorder: '#162032',
                        goldAccent: '#e5b869',
                        goldLight: '#fdf0d5',
                        jadeGreen: '#10b981',
                        cyanGlow: '#00f0ff',
                        cyanDark: '#005f73',
                        systemRed: '#ef4444',
                        purpleDao: '#a855f7'
                    },
                    fontFamily: {
                        cinzel: ['Cinzel', 'serif'],
                        mono: ['JetBrains Mono', 'monospace'],
                        sans: ['Plus Jakarta Sans', 'sans-serif']
                    }
                }
            }
        }
    </script>

    <style>
        body {
            background-color: #040609;
            color: #c9d1d9;
            font-family: 'Plus Jakarta Sans', sans-serif;
            -webkit-tap-highlight-color: transparent;
            user-select: none;
            padding-bottom: env(safe-area-inset-bottom);
        }

        .pb-safe { padding-bottom: calc(5rem + env(safe-area-inset-bottom)); }
        .pt-safe { padding-top: max(1rem, env(safe-area-inset-top)); }

        ::-webkit-scrollbar { width: 3px; }
        ::-webkit-scrollbar-track { background: #040609; }
        ::-webkit-scrollbar-thumb { background: #162032; border-radius: 4px; }

        #particle-canvas {
            position: fixed;
            top: 0; left: 0; width: 100%; height: 100%;
            pointer-events: none; z-index: 0;
        }

        @keyframes scanline {
            0% { transform: translateY(-100%); }
            100% { transform: translateY(1000%); }
        }
        .scanline-effect {
            position: absolute;
            top: 0; left: 0; right: 0; height: 2px;
            background: linear-gradient(to right, transparent, #00f0ff, transparent);
            animation: scanline 8s linear infinite;
            opacity: 0.5;
            pointer-events: none;
        }
    </style>
</head>
<body class="min-h-screen flex flex-col relative overflow-x-hidden bg-darkBg pb-safe">

    <!-- Canvas de particules spirituelles -->
    <canvas id="particle-canvas"></canvas>

    <!-- MAIN APP CONTAINER -->
    <div class="relative z-10 flex-1 flex flex-col max-w-md mx-auto w-full px-4 pt-safe">

        <!-- HEADER SYSTEM_CORE -->
        <header class="flex justify-between items-center py-3 mb-4 border-b border-darkBorder/80 bg-darkCard/60 backdrop-blur-md px-3.5 rounded-2xl border shadow-xl">
            <div class="flex items-center gap-3">
                <div class="w-10 h-10 rounded-xl bg-cyanGlow/10 border border-cyanGlow/40 flex items-center justify-center shadow-[0_0_15px_rgba(0,240,255,0.2)]">
                    <i class="fa-solid fa-atom text-cyanGlow text-lg animate-spin" style="animation-duration: 12s;"></i>
                </div>
                <div>
                    <h1 class="font-mono text-sm font-bold text-transparent bg-clip-text bg-gradient-to-r from-cyanGlow via-slate-100 to-goldAccent tracking-wider">
                        SYSTEM_CORE v5.0
                    </h1>
                    <p class="text-[9px] text-slate-400 font-mono tracking-widest uppercase" id="header-root-badge">RACINE: MORTEL</p>
                </div>
            </div>

            <div class="flex items-center gap-2">
                <button id="secte-badge-btn" class="px-2.5 py-1.5 rounded-xl bg-purpleDao/10 border border-purpleDao/30 text-purpleDao text-[10px] font-mono font-bold flex items-center gap-1 active:scale-95">
                    <i class="fa-solid fa-synagogue"></i>
                    <span id="secte-level-indicator">Secte Nv.1</span>
                </button>
                <button id="export-import-btn" title="Sauvegarde" class="p-2 rounded-xl bg-goldAccent/10 border border-goldAccent/30 text-goldAccent text-xs active:scale-95">
                    <i class="fa-solid fa-file-arrow-down"></i>
                </button>
            </div>
        </header>

        <!-- ALERTE D'INSTABILITÉ DU QI -->
        <div id="instability-alert" class="hidden mb-4 p-3 bg-systemRed/10 border border-systemRed/40 rounded-2xl flex items-center gap-3 text-systemRed text-xs font-mono shadow-[0_0_20px_rgba(239,68,68,0.15)]">
            <i class="fa-solid fa-triangle-exclamation text-base animate-bounce shrink-0"></i>
            <div>
                <strong class="block font-bold">DÉVIATION DU QI DÉTECTÉE</strong>
                <span>Plus de 24h d'inactivité. Rendement des quêtes réduit de 50%.</span>
            </div>
        </div>

        <!-- TAB 1: SYSTEM CULTIVATION DASHBOARD -->
        <section id="tab-cultivation" class="tab-view flex flex-col gap-4">
            
            <!-- PALIER PRINCIPAL & BARRE DE DENSITÉ -->
            <div class="bg-darkCard border border-darkBorder rounded-2xl p-5 shadow-2xl relative overflow-hidden flex flex-col gap-4">
                <div class="scanline-effect"></div>

                <div class="flex justify-between items-start">
                    <div>
                        <div class="flex items-center gap-2">
                            <span class="inline-block w-2 h-2 rounded-full bg-cyanGlow animate-ping"></span>
                            <span id="active-realm-badge" class="text-[10px] font-mono font-bold text-cyanGlow uppercase tracking-wider">
                                PALIER 01 // BODY_FORGING
                            </span>
                        </div>
                        <h2 id="active-realm-title" class="font-cinzel text-xl font-black text-slate-100 mt-1">
                            Forge du Corps
                        </h2>
                    </div>
                    <div class="text-right font-mono">
                        <span class="text-[9px] text-slate-400 block">DENSITÉ DU QI</span>
                        <span id="circle-percent" class="text-lg font-bold text-goldAccent">0.0%</span>
                    </div>
                </div>

                <!-- Barre de progression -->
                <div class="space-y-1.5">
                    <div class="flex justify-between text-[11px] font-mono text-slate-400">
                        <span>Ancrage Spirituel</span>
                        <span id="circle-qi-text">0 / 100 Units</span>
                    </div>
                    <div class="w-full h-3 bg-darkBg rounded-full border border-darkBorder p-0.5 overflow-hidden">
                        <div id="foundation-bar" class="h-full bg-gradient-to-r from-cyanDark via-cyanGlow to-goldAccent rounded-full transition-all duration-500 w-0"></div>
                    </div>
                </div>

                <!-- METRIQUES STREAK & RANG -->
                <div class="grid grid-cols-2 gap-2 pt-1 font-mono">
                    <div class="bg-darkBg/80 border border-darkBorder rounded-xl p-2.5 flex items-center gap-2.5">
                        <div class="w-8 h-8 rounded-lg bg-goldAccent/10 text-goldAccent flex items-center justify-center text-xs">
                            <i class="fa-solid fa-fire"></i>
                        </div>
                        <div>
                            <span class="text-[9px] text-slate-400 block">RÉGULARITÉ</span>
                            <span id="streak-counter" class="text-xs font-bold text-slate-100">0 Jours</span>
                        </div>
                    </div>
                    <div class="bg-darkBg/80 border border-darkBorder rounded-xl p-2.5 flex items-center gap-2.5">
                        <div class="w-8 h-8 rounded-lg bg-purpleDao/10 text-purpleDao flex items-center justify-center text-xs">
                            <i class="fa-solid fa-crown"></i>
                        </div>
                        <div>
                            <span class="text-[9px] text-slate-400 block">TITRE ACTIF</span>
                            <span id="active-title-label" class="text-[10px] font-bold text-purpleDao truncate max-w-[100px] block">Novice</span>
                        </div>
                    </div>
                </div>

                <p id="active-realm-subtitle" class="text-xs text-slate-400 leading-relaxed font-sans border-l-2 border-cyanGlow/40 pl-2.5 py-0.5">
                    Optimisation biologique initiale. Ancrage d'une structure physique et spatiale sans faille.
                </p>

                <!-- Bouton Tribulation -->
                <button id="breakthrough-btn" disabled class="w-full py-3 rounded-xl font-mono font-bold text-xs uppercase tracking-wider transition-all duration-300 opacity-50 cursor-not-allowed bg-slate-900 text-slate-500 border border-slate-800 flex items-center justify-center gap-2">
                    <i class="fa-solid fa-bolt-lightning"></i>
                    <span>Exécuter la Tribulation Céleste</span>
                </button>
            </div>

            <!-- HUD ATTRIBUTS DU CULTIVATEUR -->
            <div class="bg-darkCard border border-darkBorder rounded-2xl p-4 shadow-xl flex flex-col gap-3">
                <div class="flex justify-between items-center">
                    <h3 class="font-mono text-xs font-bold text-slate-300 flex items-center gap-2 uppercase tracking-wider">
                        <i class="fa-solid fa-chart-pie text-cyanGlow"></i>
                        Attributs du Cultivateur
                    </h3>
                    <span id="total-attributes-pts" class="text-[10px] font-mono text-cyanGlow">Total: 0 XP</span>
                </div>

                <div class="grid grid-cols-2 gap-2.5 font-mono text-xs">
                    <div class="bg-darkBg p-2.5 rounded-xl border border-darkBorder flex flex-col gap-1">
                        <div class="flex justify-between text-[11px]">
                            <span class="text-slate-400"><i class="fa-solid fa-dumbbell text-systemRed mr-1"></i> Vigueur</span>
                            <span id="stat-vigueur-val" class="text-slate-200 font-bold">0</span>
                        </div>
                        <div class="w-full h-1.5 bg-darkCard rounded-full overflow-hidden">
                            <div id="bar-vigueur" class="bg-systemRed h-full transition-all duration-300" style="width: 0%"></div>
                        </div>
                    </div>
                    <div class="bg-darkBg p-2.5 rounded-xl border border-darkBorder flex flex-col gap-1">
                        <div class="flex justify-between text-[11px]">
                            <span class="text-slate-400"><i class="fa-solid fa-brain text-cyanGlow mr-1"></i> Esprit</span>
                            <span id="stat-esprit-val" class="text-slate-200 font-bold">0</span>
                        </div>
                        <div class="w-full h-1.5 bg-darkCard rounded-full overflow-hidden">
                            <div id="bar-esprit" class="bg-cyanGlow h-full transition-all duration-300" style="width: 0%"></div>
                        </div>
                    </div>
                    <div class="bg-darkBg p-2.5 rounded-xl border border-darkBorder flex flex-col gap-1">
                        <div class="flex justify-between text-[11px]">
                            <span class="text-slate-400"><i class="fa-solid fa-anchor text-goldAccent mr-1"></i> Ancrage</span>
                            <span id="stat-ancrage-val" class="text-slate-200 font-bold">0</span>
                        </div>
                        <div class="w-full h-1.5 bg-darkCard rounded-full overflow-hidden">
                            <div id="bar-ancrage" class="bg-goldAccent h-full transition-all duration-300" style="width: 0%"></div>
                        </div>
                    </div>
                    <div class="bg-darkBg p-2.5 rounded-xl border border-darkBorder flex flex-col gap-1">
                        <div class="flex justify-between text-[11px]">
                            <span class="text-slate-400"><i class="fa-solid fa-bolt text-jadeGreen mr-1"></i> Agilité</span>
                            <span id="stat-agilite-val" class="text-slate-200 font-bold">0</span>
                        </div>
                        <div class="w-full h-1.5 bg-darkCard rounded-full overflow-hidden">
                            <div id="bar-agilite" class="bg-jadeGreen h-full transition-all duration-300" style="width: 0%"></div>
                        </div>
                    </div>
                </div>
            </div>

            <!-- DIRECTIVES DU PALIER -->
            <div class="flex flex-col gap-3">
                <div class="flex justify-between items-center px-1">
                    <h3 class="font-mono text-xs font-bold text-slate-300 flex items-center gap-2 uppercase tracking-wider">
                        <i class="fa-solid fa-bars-staggered text-cyanGlow"></i>
                        Directives d'Optimisation
                    </h3>
                    
                    <button id="add-quest-modal-btn" class="px-2.5 py-1 rounded-lg bg-cyanGlow/10 border border-cyanGlow/30 text-cyanGlow text-xs font-mono font-semibold flex items-center gap-1 active:scale-95">
                        <i class="fa-solid fa-plus"></i>
                        <span>Directive</span>
                    </button>
                </div>

                <div id="quests-container" class="flex flex-col gap-2.5">
                </div>
            </div>

        </section>

        <!-- TAB 2: TECHNIQUES DIVINES & ARTS MARTIAUX -->
        <section id="tab-skills" class="tab-view hidden flex-col gap-4">
            <div class="px-1">
                <h2 class="font-mono text-base font-bold text-slate-100 uppercase">Techniques Divines</h2>
                <p class="text-xs text-slate-400">Progression par répétition et maîtrise des arts martiaux.</p>
            </div>

            <div id="skills-container" class="flex flex-col gap-3">
            </div>
        </section>

        <!-- TAB 3: DOMAINE DE SECTE (IDLE / PASSIVE) -->
        <section id="tab-secte" class="tab-view hidden flex-col gap-4">
            <div class="bg-darkCard border border-purpleDao/40 rounded-2xl p-5 shadow-2xl relative overflow-hidden flex flex-col gap-3">
                <div class="flex justify-between items-center">
                    <div>
                        <span class="text-[9px] font-mono text-purpleDao uppercase tracking-wider block">DOMAINE SPIRITUEL</span>
                        <h2 class="font-cinzel text-lg font-bold text-slate-100">Secte de la Voie Céleste</h2>
                    </div>
                    <div class="w-10 h-10 rounded-xl bg-purpleDao/20 border border-purpleDao text-purpleDao flex items-center justify-center text-lg">
                        <i class="fa-solid fa-synagogue"></i>
                    </div>
                </div>

                <p class="text-xs text-slate-400 font-sans leading-relaxed">
                    Vos disciples fantômes absorbent le Qi environnant en arrière-plan grâce à votre série d'assiduité (<span id="secte-streak-display" class="text-purpleDao font-bold">0 Jours</span>).
                </p>

                <div class="bg-darkBg p-3 rounded-xl border border-darkBorder flex justify-between items-center font-mono text-xs">
                    <div>
                        <span class="text-[10px] text-slate-500 block">QI EN ATTENTE</span>
                        <span id="pending-idle-qi" class="text-goldAccent font-bold text-sm">0.0 Units</span>
                    </div>
                    <button id="claim-idle-qi-btn" class="px-3 py-2 rounded-xl bg-purpleDao text-darkBg font-bold text-xs active:scale-95 shadow-lg">
                        Récolter le Qi
                    </button>
                </div>
            </div>

            <!-- RUINES ANTIQUES ET CARTES AU TRÉSOR -->
            <div class="bg-darkCard border border-goldAccent/30 rounded-2xl p-4 shadow-xl space-y-3">
                <div class="flex items-center gap-2.5">
                    <i class="fa-solid fa-map text-goldAccent text-base"></i>
                    <h3 class="font-mono text-xs font-bold text-slate-200 uppercase">Ruines Antiques & Cartes au Trésor</h3>
                </div>
                <p class="text-xs text-slate-400 font-sans">Résolvez une énigme logique ou mathématique antique pour débloquer un trésor de Qi.</p>
                <button id="open-ruins-btn" class="w-full py-2.5 rounded-xl bg-goldAccent/10 border border-goldAccent/40 text-goldAccent text-xs font-mono font-bold active:scale-95 flex items-center justify-center gap-2">
                    <i class="fa-solid fa-compass"></i>
                    <span>Explorer une Ruine Antique</span>
                </button>
            </div>
        </section>

        <!-- TAB 4: L'ŒIL DE VÉRIFICATION & AUDIT CHAT -->
        <section id="tab-master" class="tab-view hidden flex-col gap-4">
            <div class="bg-darkCard border border-cyanGlow/30 rounded-2xl p-4 flex items-center gap-3.5 shadow-xl">
                <div class="w-11 h-11 rounded-xl bg-cyanGlow/10 border border-cyanGlow text-cyanGlow flex items-center justify-center text-lg shrink-0">
                    <i class="fa-solid fa-eye"></i>
                </div>
                <div class="flex-1">
                    <h2 class="font-mono font-bold text-xs text-slate-100 uppercase">ŒIL DE VÉRIFICATION & AUDIT</h2>
                    <p class="text-[11px] text-slate-400 mt-0.5 leading-snug font-sans">Analyse automatique des failles de discipline et conseils du Système.</p>
                </div>
            </div>

            <button id="run-appraisal-scan-btn" class="w-full py-2.5 rounded-xl bg-cyanGlow/10 border border-cyanGlow/40 text-cyanGlow font-mono font-bold text-xs flex items-center justify-center gap-2 active:scale-95">
                <i class="fa-solid fa-microchip"></i>
                <span>Scanner les Failles de Discipline</span>
            </button>

            <!-- CHAT TERMINAL LOGS -->
            <div class="bg-darkCard border border-darkBorder rounded-2xl flex flex-col h-[340px] shadow-2xl overflow-hidden">
                <div class="px-3.5 py-2 border-b border-darkBorder bg-darkBg/80 flex justify-between items-center text-[11px] font-mono">
                    <span class="text-slate-400 font-semibold flex items-center gap-2">
                        <i class="fa-solid fa-terminal text-cyanGlow"></i>
                        COMMUNICATION SYSTEM_CORE
                    </span>
                    <button id="clear-chat-btn" class="text-[10px] text-slate-500 hover:text-systemRed">Effacer</button>
                </div>

                <div id="master-chat-messages" class="flex-1 p-3 overflow-y-auto space-y-3 text-xs font-sans">
                </div>

                <form id="master-chat-form" class="p-2 border-t border-darkBorder bg-darkBg/90 flex items-center gap-2">
                    <input type="text" id="master-chat-input" placeholder="Consigner votre rapport du jour..." class="flex-1 bg-darkCard border border-darkBorder rounded-xl px-3 py-2 text-slate-200 text-xs outline-none focus:border-cyanGlow font-mono">
                    <button type="submit" class="w-9 h-9 rounded-xl bg-cyanGlow text-darkBg flex items-center justify-center font-bold text-xs active:scale-95 shrink-0">
                        <i class="fa-solid fa-chevron-right"></i>
                    </button>
                </form>
            </div>
        </section>

        <!-- TAB 5: PANTHÉON DES ANCÊTRES & TITRES -->
        <section id="tab-pantheon" class="tab-view hidden flex-col gap-4">
            <div class="px-1">
                <h2 class="font-mono text-base font-bold text-slate-100 uppercase">Panthéon & Titres Honorifiques</h2>
                <p class="text-xs text-slate-400">Équipement des titres et passifs d'ancêtres.</p>
            </div>

            <div id="titles-container" class="flex flex-col gap-2.5">
            </div>
        </section>

    </div>

    <!-- NAVBAR MOBIL -->
    <nav class="fixed bottom-0 left-0 right-0 bg-darkCard/95 backdrop-blur-lg border-t border-darkBorder z-40 py-2 px-3 flex justify-around items-center max-w-md mx-auto font-mono">
        <button class="nav-tab active flex flex-col items-center gap-1 text-cyanGlow transition-colors" data-target="tab-cultivation">
            <i class="fa-solid fa-microchip text-base"></i>
            <span class="text-[8px] font-semibold">Système</span>
        </button>
        <button class="nav-tab flex flex-col items-center gap-1 text-slate-500 transition-colors" data-target="tab-skills">
            <i class="fa-solid fa-hand-fist text-base"></i>
            <span class="text-[8px] font-semibold">Arts</span>
        </button>
        <button class="nav-tab flex flex-col items-center gap-1 text-slate-500 transition-colors" data-target="tab-secte">
            <i class="fa-solid fa-synagogue text-base"></i>
            <span class="text-[8px] font-semibold">Secte</span>
        </button>
        <button class="nav-tab flex flex-col items-center gap-1 text-slate-500 transition-colors" data-target="tab-master">
            <i class="fa-solid fa-eye text-base"></i>
            <span class="text-[8px] font-semibold">Œil</span>
        </button>
        <button class="nav-tab flex flex-col items-center gap-1 text-slate-500 transition-colors" data-target="tab-pantheon">
            <i class="fa-solid fa-crown text-base"></i>
            <span class="text-[8px] font-semibold">Titres</span>
        </button>
    </nav>

    <!-- MODAL: AUDIT STRICT CHRONO-INTELLIGENT -->
    <div id="verification-modal" class="fixed inset-0 z-50 flex items-center justify-center p-4 bg-darkBg/95 backdrop-blur-md opacity-0 pointer-events-none transition-all duration-300">
        <div class="bg-darkCard border-2 border-cyanGlow rounded-2xl p-5 max-w-sm w-full text-left relative shadow-[0_0_40px_rgba(0,240,255,0.25)] space-y-4">
            <div class="flex items-center gap-3">
                <div class="w-10 h-10 rounded-xl bg-cyanGlow/20 border border-cyanGlow text-cyanGlow flex items-center justify-center text-base">
                    <i class="fa-solid fa-stopwatch"></i>
                </div>
                <div>
                    <h3 class="font-mono text-xs font-black text-cyanGlow uppercase">AUDIT CHRONO-INTELLIGENT</h3>
                    <p class="text-[10px] text-slate-400 font-mono">Contrôle d'intégrité & Temps Réel</p>
                </div>
            </div>

            <div class="space-y-3 font-sans text-xs">
                <p id="verification-quest-title" class="font-bold text-slate-200">Intitulé de la directive</p>
                
                <div>
                    <label class="block text-slate-400 text-[10px] font-mono mb-1">Durée réelle consacrée (en minutes) :</label>
                    <input type="number" id="verification-time-input" min="1" value="20" class="w-full bg-darkBg border border-darkBorder rounded-xl p-2.5 text-slate-200 font-mono text-xs outline-none focus:border-cyanGlow">
                </div>

                <div>
                    <label class="block text-slate-400 text-[10px] font-mono mb-1">Rapport de cohérence logique :</label>
                    <textarea id="verification-proof-input" rows="3" placeholder="Description détaillée du travail effectué..." class="w-full bg-darkBg border border-darkBorder rounded-xl p-2.5 text-slate-200 text-xs outline-none focus:border-cyanGlow"></textarea>
                </div>
            </div>

            <div id="audit-status" class="hidden text-xs font-mono p-2.5 rounded-xl text-center"></div>

            <div class="flex gap-2 pt-1 font-mono">
                <button id="cancel-verification-btn" class="flex-1 py-2.5 rounded-xl border border-darkBorder text-slate-400 text-xs font-semibold">Annuler</button>
                <button id="confirm-verification-btn" class="flex-1 py-2.5 rounded-xl bg-cyanGlow text-darkBg text-xs font-bold">Soumettre l'Audit</button>
            </div>
        </div>
    </div>

    <!-- MODAL: TRIBULATION CÉLESTE MULTIMODALE (BREAKTHROUGH) -->
    <div id="breakthrough-modal" class="fixed inset-0 z-50 flex items-center justify-center p-4 bg-darkBg/95 backdrop-blur-md opacity-0 pointer-events-none transition-all duration-300">
        <div class="bg-darkCard border-2 border-goldAccent rounded-2xl p-5 max-w-sm w-full text-left relative shadow-[0_0_50px_rgba(229,184,105,0.3)] space-y-4">
            <div class="flex items-center gap-3">
                <div class="w-12 h-12 rounded-2xl bg-goldAccent/20 border-2 border-goldAccent flex items-center justify-center text-goldAccent text-xl animate-pulse">
                    <i class="fa-solid fa-bolt-lightning"></i>
                </div>
                <div>
                    <h3 class="font-mono text-xs font-black text-goldAccent uppercase">TRIBULATION CÉLESTE</h3>
                    <p class="text-[10px] text-slate-400 font-mono">Évaluation Multimodale par l'IA</p>
                </div>
            </div>

            <div id="tribulation-body" class="space-y-3 font-sans text-xs">
                <!-- Contenu généré dynamiquement -->
            </div>

            <div id="tribulation-status" class="hidden text-xs font-mono p-2.5 rounded-xl text-center"></div>

            <div class="flex gap-2 pt-2 font-mono">
                <button id="close-breakthrough-btn" class="flex-1 py-2.5 rounded-xl border border-darkBorder text-slate-400 text-xs font-semibold">Abandonner</button>
                <button id="submit-tribulation-btn" class="flex-1 py-2.5 rounded-xl bg-goldAccent text-darkBg text-xs font-bold">Valider l'Épreuve</button>
            </div>
        </div>
    </div>

    <!-- MODAL: RUINES ANTIQUES (ÉMIGME) -->
    <div id="ruins-modal" class="fixed inset-0 z-50 flex items-center justify-center p-4 bg-darkBg/95 backdrop-blur-md opacity-0 pointer-events-none transition-all duration-300">
        <div class="bg-darkCard border border-goldAccent rounded-2xl p-5 max-w-sm w-full space-y-4">
            <h3 class="font-mono text-xs font-bold text-goldAccent uppercase flex items-center gap-2">
                <i class="fa-solid fa-landmark"></i>
                Énigme de la Ruine Antique
            </h3>
            <p id="ruins-riddle-text" class="text-xs text-slate-300 font-sans leading-relaxed"></p>
            <input type="text" id="ruins-answer-input" placeholder="Votre réponse..." class="w-full bg-darkBg border border-darkBorder rounded-xl p-3 text-slate-200 outline-none focus:border-goldAccent font-mono text-xs">
            <div id="ruins-status" class="hidden text-xs font-mono p-2 rounded-xl text-center"></div>
            <div class="flex gap-2 font-mono">
                <button id="close-ruins-btn" class="flex-1 py-2 rounded-xl border border-darkBorder text-slate-400 text-xs">Quitter</button>
                <button id="submit-ruins-btn" class="flex-1 py-2 rounded-xl bg-goldAccent text-darkBg text-xs font-bold">Résoudre</button>
            </div>
        </div>
    </div>

    <!-- MODAL: NOUVELLE DIRECTIVE -->
    <div id="quest-modal" class="fixed inset-0 z-50 flex items-center justify-center p-4 bg-darkBg/90 backdrop-blur-sm opacity-0 pointer-events-none transition-opacity duration-300">
        <div class="bg-darkCard border border-goldAccent/40 rounded-2xl p-5 w-full max-w-sm shadow-2xl space-y-4">
            <h3 class="font-mono text-sm font-bold text-goldAccent flex items-center gap-2">
                <i class="fa-solid fa-plus-circle"></i>
                Nouvelle Directive Personnalisée
            </h3>

            <div class="space-y-3 text-xs font-sans">
                <div>
                    <label class="block text-slate-400 mb-1 font-mono">Objectif de la Directive</label>
                    <input type="text" id="custom-quest-title" placeholder="Ex: Résoudre 5 exercices de thermo" class="w-full bg-darkBg border border-darkBorder rounded-xl p-3 text-slate-200 outline-none focus:border-goldAccent">
                </div>

                <div>
                    <label class="block text-slate-400 mb-1 font-mono">Catégorie d'Attribut</label>
                    <select id="custom-quest-cat" class="w-full bg-darkBg border border-darkBorder rounded-xl p-3 text-slate-200 outline-none focus:border-goldAccent font-mono">
                        <option value="vigueur">Vigueur (Physique)</option>
                        <option value="esprit" selected>Esprit (Physique / Maths)</option>
                        <option value="ancrage">Ancrage (Routine)</option>
                        <option value="agilite">Agilité (Focus)</option>
                    </select>
                </div>

                <div>
                    <label class="block text-slate-400 mb-1 font-mono">Type</label>
                    <select id="custom-quest-req" class="w-full bg-darkBg border border-darkBorder rounded-xl p-3 text-slate-200 outline-none focus:border-goldAccent font-mono">
                        <option value="mandatory">Obligatoire (Palier)</option>
                        <option value="optional">Optionnel (Bonus)</option>
                    </select>
                </div>

                <div>
                    <label class="block text-slate-400 mb-1 font-mono">Valeur (Units)</label>
                    <input type="number" id="custom-quest-qi" value="30" min="10" max="100" class="w-full bg-darkBg border border-darkBorder rounded-xl p-3 text-slate-200 outline-none focus:border-goldAccent font-mono">
                </div>
            </div>

            <div class="flex gap-2 pt-2 font-mono">
                <button id="cancel-quest-btn" class="flex-1 py-2.5 rounded-xl border border-darkBorder text-slate-400 text-xs font-semibold">Annuler</button>
                <button id="save-quest-btn" class="flex-1 py-2.5 rounded-xl bg-goldAccent text-darkBg text-xs font-bold">Consigner</button>
            </div>
        </div>
    </div>

    <!-- MODAL EXPORT/IMPORT -->
    <div id="export-import-modal" class="fixed inset-0 z-50 flex items-center justify-center p-4 bg-darkBg/90 backdrop-blur-sm opacity-0 pointer-events-none transition-opacity duration-300">
        <div class="bg-darkCard border border-goldAccent/40 rounded-2xl p-5 w-full max-w-sm space-y-4">
            <h3 class="font-mono text-sm font-bold text-goldAccent">Sauvegarde JSON</h3>
            <div class="flex flex-col gap-2.5 font-mono">
                <button id="export-json-btn" class="w-full py-2.5 rounded-xl bg-goldAccent/20 border border-goldAccent/40 text-goldAccent text-xs font-bold">Exporter (.json)</button>
                <label class="w-full py-2.5 rounded-xl bg-cyanGlow/10 border border-cyanGlow/30 text-cyanGlow text-xs font-bold text-center cursor-pointer">
                    Importer (.json)
                    <input type="file" id="import-json-input" accept=".json" class="hidden">
                </label>
            </div>
            <button id="close-export-modal-btn" class="w-full py-2 rounded-xl border border-darkBorder text-slate-400 text-xs">Fermer</button>
        </div>
    </div>

    <!-- JAVASCRIPT APP LOGIC v5.0 -->
    <script>
        // DATA DES 10 PALIERS THÉMATIQUES AVEC EXPONANITIEL DENSITÉ
        const MASTER_REALMS = [
            { id: 1, title: "BODY_FORGING", nameFr: "Forge du Corps", badge: "PALIER 01", icon: "fa-dumbbell", targetQi: 100, desc: "Ancrage d'une structure physique et spatiale sans faille.", quests: [
                { id: "bf_1", title: "Santé du Vaisseau Biologique", desc: "45 min de musculation ou cardio intense.", qi: 30, cat: "vigueur", difficulty: "Facile", mandatory: true, minTime: 30, completed: false },
                { id: "bf_2", title: "Sanctuaire de Travail", desc: "Rangement complet et purification de l'espace de travail.", qi: 25, cat: "ancrage", difficulty: "Facile", mandatory: true, minTime: 15, completed: false },
                { id: "bf_3", title: "Mobilité Articulaire", desc: "Routine d'étirements de 20 min.", qi: 20, cat: "vigueur", difficulty: "Facile", mandatory: false, minTime: 10, completed: false }
            ]},
            { id: 2, title: "QI_REFINING", nameFr: "Raffinage des Données", badge: "PALIER 02", icon: "fa-brain", targetQi: 180, desc: "Assimilation d'informations théoriques brutes et purge des distractions.", quests: [
                { id: "qr_1", title: "Concentration Ciblée (Licence)", desc: "1h d'étude active en physique/mathématiques.", qi: 40, cat: "esprit", difficulty: "Moyenne", mandatory: true, minTime: 40, completed: false },
                { id: "qr_2", title: "Purge des Flux Parasites", desc: "Zéro réseaux sociaux pendant toute la journée.", qi: 35, cat: "agilite", difficulty: "Moyenne", mandatory: true, minTime: 60, completed: false }
            ]},
            { id: 3, title: "FOUNDATION_ESTABLISHMENT", nameFr: "Fondation Inébranlable", badge: "PALIER 03", icon: "fa-cubes-stacked", targetQi: 280, desc: "Ancrage des structures de pensée permanentes.", quests: [
                { id: "fe_1", title: "Feynman Technique Session", desc: "Expliquer un concept d'électrostatique ou d'algèbre de A à Z.", qi: 50, cat: "esprit", difficulty: "Difficile", mandatory: true, minTime: 45, completed: false }
            ]},
            { id: 4, title: "GOLDEN_CORE", nameFr: "Noyau Cristallisé", badge: "PALIER 04", icon: "fa-atom", targetQi: 400, desc: "Cristallisation de l'autonomie intellectuelle.", quests: [
                { id: "gc_1", title: "Résolution de Problème Complexe", desc: "3 exercices complets d'analyse ou de thermodynamique.", qi: 60, cat: "esprit", difficulty: "Difficile", mandatory: true, minTime: 50, completed: false }
            ]},
            { id: 5, title: "NASCENT_SOUL", nameFr: "Expansion Stratégique", badge: "PALIER 05", icon: "fa-network-wired", targetQi: 550, desc: "Émergence d'une vision long terme sans biais.", quests: []},
            { id: 6, title: "SOUL_FORMATION", nameFr: "Harmonisation Cognition", badge: "PALIER 06", icon: "fa-eye", targetQi: 720, desc: "Suppression des frictions entre décision et exécution.", quests: []},
            { id: 7, title: "VOID_REFINEMENT", nameFr: "Silence Mental Absolu", badge: "PALIER 07", icon: "fa-wind", targetQi: 900, desc: "Contrôle parfait de l'agitation interne.", quests: []},
            { id: 8, title: "BODY_INTEGRATION", nameFr: "Intégration Totale", badge: "PALIER 08", icon: "fa-dna", targetQi: 1100, desc: "Harmonie absolue entre physique et mental.", quests: []},
            { id: 9, title: "MAHAYANA", nameFr: "Grande Synthèse", badge: "PALIER 09", icon: "fa-sun", targetQi: 1350, desc: "Création de structures de valeur durable.", quests: []},
            { id: 10, title: "TRANSCENDENCE", nameFr: "Transcendance Suprême", badge: "PALIER 10", icon: "fa-infinity", targetQi: 1600, desc: "Accomplissement complet de la voie de cultivation.", quests: []}
        ];

        // PANTHEON DES TITRES
        const PANTHEON_TITLES = [
            { id: "t1", name: "Novice du Qi", desc: "Aucun bonus actif.", req: "Palier 1 atteint", unlocked: true, passive: "Rien" },
            { id: "t2", name: "Seigneur de la Discipline", desc: "+10% de Qi sur les quêtes d'Ancrage.", req: "Streak de 5 jours", unlocked: false, passive: "+10% Qi Ancrage" },
            { id: "t3", name: "Érudit du Dao Mathématique", desc: "+15% XP Esprit sur les calculs.", req: "Palier 3 atteint", unlocked: false, passive: "+15% XP Esprit" },
            { id: "t4", name: "Briseur de Limites Biologiques", desc: "+15% XP Vigueur.", req: "3 Arts Martiaux Maîtrisés", unlocked: false, passive: "+15% XP Vigueur" }
        ];

        // TECHNIQUES DIVINES & ARTS MARTIAUX
        const INITIAL_SKILLS = [
            { id: "s1", name: "L'Épée de Concentration Céleste", type: "Esprit", level: 1, maxLvl: 5, reps: 0, targetReps: 5, bonus: "+5% XP Esprit" },
            { id: "s2", name: "Posture du Palmier d'Acier (Handstand)", type: "Vigueur", level: 1, maxLvl: 5, reps: 0, targetReps: 5, bonus: "+5% XP Vigueur" },
            { id: "s3", name: "Respiration du Vide Mental", type: "Ancrage", level: 1, maxLvl: 5, reps: 0, targetReps: 5, bonus: "+5% Qi Passif" }
        ];

        let appData = {
            qi: 0,
            maxQi: 100,
            currentRealmIdx: 0,
            attributes: { vigueur: 0, esprit: 0, ancrage: 0, agilite: 0 },
            streak: 0,
            lastCompletedDate: null,
            lastActivityTimestamp: Date.now(),
            quests: [],
            skills: INITIAL_SKILLS,
            titles: PANTHEON_TITLES,
            activeTitleId: "t1",
            idleQi: 0.0,
            journal: [{ id: "j1", date: new Date().toLocaleDateString(), text: "SYSTEM_CORE v5.0 initialisé." }],
            chatHistory: [{ sender: "system", text: "Salutations, Hôte. Le moteur d'audit chrono-intelligent v5.0 est en ligne." }]
        };

        let pendingQuestIndex = null;
        let currentTribulationType = null; // 'physical' ou 'mental'
        let currentMentalAnswer = 0;

        function loadState() {
            const saved = localStorage.getItem("system_cultivation_mobile_v50");
            if (saved) {
                try { appData = { ...appData, ...JSON.parse(saved) }; } catch(e){}
            }
            if (!appData.quests || appData.quests.length === 0) {
                loadRealmQuests(appData.currentRealmIdx);
            }
            checkDailyReset();
            checkInstability();
            calculateIdleQi();
        }

        function saveState() {
            localStorage.setItem("system_cultivation_mobile_v50", JSON.stringify(appData));
        }

        function loadRealmQuests(idx) {
            const r = MASTER_REALMS[idx] || MASTER_REALMS[0];
            appData.maxQi = r.targetQi;
            appData.quests = JSON.parse(JSON.stringify(r.quests));
        }

        function checkDailyReset() {
            const today = new Date().toDateString();
            if (appData.lastResetDate !== today) {
                appData.quests.forEach(q => { q.completed = false; q.proof = ""; });
                appData.lastResetDate = today;
                saveState();
            }
        }

        function checkInstability() {
            const diffHours = (Date.now() - (appData.lastActivityTimestamp || Date.now())) / (1000 * 3600);
            const alertEl = document.getElementById("instability-alert");
            if (diffHours >= 24) alertEl.classList.remove("hidden");
            else alertEl.classList.add("hidden");
        }

        function calculateIdleQi() {
            const now = Date.now();
            const elapsedHours = (now - (appData.lastActivityTimestamp || now)) / (1000 * 3600);
            const ratePerHour = 1.5 + (appData.streak * 0.5);
            const gained = Math.min(100, elapsedHours * ratePerHour);
            appData.idleQi = Math.round(gained * 10) / 10;
        }

        // Particle Canvas
        const canvas = document.getElementById("particle-canvas");
        const ctx = canvas.getContext("2d");
        let particles = [];
        function resizeCanvas() { canvas.width = window.innerWidth; canvas.height = window.innerHeight; }
        window.addEventListener("resize", resizeCanvas);
        resizeCanvas();

        for (let i = 0; i < 40; i++) {
            particles.push({
                x: Math.random() * canvas.width, y: Math.random() * canvas.height,
                radius: Math.random() * 1.8 + 0.4,
                color: Math.random() > 0.4 ? '#00f0ff' : '#e5b869',
                vx: (Math.random() - 0.5) * 0.3, vy: (Math.random() - 0.5) * 0.3,
                alpha: Math.random() * 0.5 + 0.2
            });
        }

        function animateParticles() {
            ctx.clearRect(0, 0, canvas.width, canvas.height);
            particles.forEach(p => {
                p.x += p.vx; p.y += p.vy;
                if (p.x < 0) p.x = canvas.width; if (p.x > canvas.width) p.x = 0;
                if (p.y < 0) p.y = canvas.height; if (p.y > canvas.height) p.y = 0;
                ctx.beginPath(); ctx.arc(p.x, p.y, p.radius, 0, Math.PI * 2);
                ctx.fillStyle = p.color; ctx.globalAlpha = p.alpha; ctx.fill();
            });
            requestAnimationFrame(animateParticles);
        }
        animateParticles();

        // Navigation Tabs
        document.querySelectorAll(".nav-tab").forEach(btn => {
            btn.addEventListener("click", () => {
                const target = btn.getAttribute("data-target");
                document.querySelectorAll(".tab-view").forEach(v => v.classList.add("hidden"));
                document.getElementById(target).classList.remove("hidden");
                document.querySelectorAll(".nav-tab").forEach(b => { b.classList.remove("text-cyanGlow"); b.classList.add("text-slate-500"); });
                btn.classList.remove("text-slate-500"); btn.classList.add("text-cyanGlow");
            });
        });

        function renderUI() {
            const realm = MASTER_REALMS[appData.currentRealmIdx] || MASTER_REALMS[0];
            document.getElementById("active-realm-badge").innerText = `${realm.badge} // ${realm.title}`;
            document.getElementById("active-realm-title").innerText = realm.nameFr;
            document.getElementById("active-realm-subtitle").innerText = realm.desc;

            const percent = Math.min(100, (appData.qi / appData.maxQi) * 100).toFixed(1);
            document.getElementById("circle-percent").innerText = `${percent}%`;
            document.getElementById("circle-qi-text").innerText = `${appData.qi} / ${appData.maxQi} Units`;
            document.getElementById("foundation-bar").style.width = `${percent}%`;

            document.getElementById("streak-counter").innerText = `${appData.streak} Jours`;
            document.getElementById("secte-streak-display").innerText = `${appData.streak} Jours`;
            document.getElementById("pending-idle-qi").innerText = `${appData.idleQi} Units`;

            const activeTitle = appData.titles.find(t => t.id === appData.activeTitleId) || appData.titles[0];
            document.getElementById("active-title-label").innerText = activeTitle.name;

            document.getElementById("stat-vigueur-val").innerText = appData.attributes.vigueur;
            document.getElementById("bar-vigueur").style.width = `${Math.min(100, (appData.attributes.vigueur / 250) * 100)}%`;

            document.getElementById("stat-esprit-val").innerText = appData.attributes.esprit;
            document.getElementById("bar-esprit").style.width = `${Math.min(100, (appData.attributes.esprit / 250) * 100)}%`;

            document.getElementById("stat-ancrage-val").innerText = appData.attributes.ancrage;
            document.getElementById("bar-ancrage").style.width = `${Math.min(100, (appData.attributes.ancrage / 250) * 100)}%`;

            document.getElementById("stat-agilite-val").innerText = appData.attributes.agilite;
            document.getElementById("bar-agilite").style.width = `${Math.min(100, (appData.attributes.agilite / 250) * 100)}%`;

            const totalAttr = appData.attributes.vigueur + appData.attributes.esprit + appData.attributes.ancrage + appData.attributes.agilite;
            document.getElementById("total-attributes-pts").innerText = `Total XP: ${totalAttr}`;

            // Check breakthrough condition
            const mandatoryQuests = appData.quests.filter(q => q.mandatory);
            const allMandatoryDone = mandatoryQuests.length > 0 && mandatoryQuests.every(q => q.completed);
            const bBtn = document.getElementById("breakthrough-btn");

            if (appData.qi >= appData.maxQi && allMandatoryDone) {
                bBtn.removeAttribute("disabled");
                bBtn.className = "w-full py-3 rounded-xl font-mono font-bold text-xs uppercase tracking-wider transition-all duration-300 bg-gradient-to-r from-cyanGlow to-goldAccent text-darkBg cursor-pointer shadow-[0_0_20px_rgba(0,240,255,0.4)] flex items-center justify-center gap-2";
            } else {
                bBtn.setAttribute("disabled", "true");
                bBtn.className = "w-full py-3 rounded-xl font-mono font-bold text-xs uppercase tracking-wider transition-all duration-300 opacity-50 cursor-not-allowed bg-slate-900 text-slate-500 border border-slate-800 flex items-center justify-center gap-2";
            }

            renderQuests();
            renderSkills();
            renderTitles();
            renderChat();
        }

        function renderQuests() {
            const container = document.getElementById("quests-container");
            container.innerHTML = "";

            if (appData.quests.length === 0) {
                container.innerHTML = `<p class="text-xs text-slate-500 text-center py-4 font-mono">Aucune directive pour ce palier.</p>`;
                return;
            }

            appData.quests.forEach((q, index) => {
                const card = document.createElement("div");
                card.className = `p-3.5 rounded-2xl border transition-all flex items-center justify-between gap-3 ${q.completed ? 'bg-darkCard/40 border-darkBorder opacity-70' : 'bg-darkCard border-darkBorder hover:border-cyanGlow/40 shadow-lg'}`;
                
                card.innerHTML = `
                    <div class="flex items-center gap-3 min-w-0 flex-1">
                        <button onclick="requestVerification(${index})" ${q.completed ? 'disabled' : ''} class="w-7 h-7 rounded-xl border flex items-center justify-center shrink-0 ${q.completed ? 'bg-jadeGreen/20 border-jadeGreen text-jadeGreen' : 'bg-darkBg border-darkBorder text-slate-600 hover:border-cyanGlow'}">
                            <i class="fa-solid ${q.completed ? 'fa-check text-xs' : 'fa-circle text-[6px]' }"></i>
                        </button>
                        <div class="min-w-0 flex-1">
                            <div class="flex items-center gap-2">
                                <h4 class="text-xs font-bold font-mono text-slate-200 truncate ${q.completed ? 'line-through text-slate-500' : ''}">${q.title}</h4>
                                ${q.mandatory ? '<span class="text-[8px] px-1.5 py-0.5 rounded bg-systemRed/20 text-systemRed border border-systemRed/30 font-mono">REQUIS</span>' : ''}
                            </div>
                            <p class="text-[11px] text-slate-400 truncate font-sans">${q.proof ? 'Audit: ' + q.proof : (q.desc || '')}</p>
                            <div class="flex items-center gap-2 mt-1 font-mono text-[9px] text-slate-500">
                                <span><i class="fa-solid fa-clock mr-1"></i>Min: ${q.minTime || 15}m</span>
                                <span>•</span>
                                <span class="text-goldAccent">+${q.qi} Units</span>
                            </div>
                        </div>
                    </div>
                    <button onclick="deleteQuest(${index})" class="text-slate-600 hover:text-systemRed p-1 text-xs"><i class="fa-solid fa-trash"></i></button>
                `;
                container.appendChild(card);
            });
        }

        window.requestVerification = function(index) {
            const q = appData.quests[index];
            if (q.completed) return;
            pendingQuestIndex = index;
            document.getElementById("verification-quest-title").innerText = `Directive : ${q.title}`;
            document.getElementById("verification-time-input").value = q.minTime || 20;
            document.getElementById("verification-proof-input").value = "";
            document.getElementById("audit-status").className = "hidden text-xs font-mono p-2.5 rounded-xl text-center";
            document.getElementById("verification-modal").classList.remove("opacity-0", "pointer-events-none");
        }

        document.getElementById("cancel-verification-btn").addEventListener("click", () => {
            document.getElementById("verification-modal").classList.add("opacity-0", "pointer-events-none");
            pendingQuestIndex = null;
        });

        // AUDIT CHRONO-INTELLIGENT AVEC ENTROPIE ET TEMPS RÉEL
        document.getElementById("confirm-verification-btn").addEventListener("click", () => {
            if (pendingQuestIndex === null) return;
            const q = appData.quests[pendingQuestIndex];
            const proofText = document.getElementById("verification-proof-input").value.trim();
            const declaredTime = parseInt(document.getElementById("verification-time-input").value) || 0;
            const statusEl = document.getElementById("audit-status");
            statusEl.classList.remove("hidden");

            // 1. Audit Temps Réel
            if (declaredTime < (q.minTime || 10)) {
                statusEl.className = "text-xs font-mono p-2.5 rounded-xl text-center bg-systemRed/20 text-systemRed border border-systemRed/40";
                statusEl.innerText = `⛔ TEMPS INSUFFISANT : Minimum ${q.minTime || 10} minutes requises par le Système.`;
                return;
            }

            // 2. Audit de Cohérence & Entropie
            const auditResult = performLocalStrictAudit(proofText);
            if (!auditResult.approved) {
                statusEl.className = "text-xs font-mono p-2.5 rounded-xl text-center bg-systemRed/20 text-systemRed border border-systemRed/40";
                statusEl.innerText = "⛔ REJET : " + auditResult.reason;
                return;
            }

            // Validation Accordée
            q.completed = true;
            q.proof = proofText + ` (${declaredTime} min)`;

            const earned = q.qi;
            appData.qi += earned;
            const cat = q.cat || 'esprit';
            appData.attributes[cat] = (appData.attributes[cat] || 0) + Math.round(earned * 0.8);

            // Progression des Arts Martiaux
            appData.skills.forEach(s => {
                if (s.type.toLowerCase() === cat.toLowerCase()) {
                    s.reps += 1;
                    if (s.reps >= s.targetReps && s.level < s.maxLvl) {
                        s.level += 1; s.reps = 0; s.targetReps += 5;
                    }
                }
            });

            statusEl.className = "text-xs font-mono p-2.5 rounded-xl text-center bg-jadeGreen/20 text-jadeGreen border border-jadeGreen/40";
            statusEl.innerText = "✅ AUDIT VALIDÉ : Rapport certifié conforme.";

            appData.lastActivityTimestamp = Date.now();
            saveState();

            setTimeout(() => {
                document.getElementById("verification-modal").classList.add("opacity-0", "pointer-events-none");
                pendingQuestIndex = null;
                renderUI();
            }, 700);
        });

        function performLocalStrictAudit(text) {
            if (!text || text.length < 20) return { approved: false, reason: "Rapport trop court (min 20 caractères)." };
            if (/(.)\1{3,}/i.test(text) || /(azerty|qwerty|asdf|zxcv|1234)/i.test(text)) return { approved: false, reason: "Spam clavier détecté." };
            const words = text.toLowerCase().split(/\s+/).filter(w => w.length > 0);
            if (words.length < 4) return { approved: false, reason: "Structure de phrase invalide." };
            return { approved: true, reason: "Cohérence validée." };
        }

        window.deleteQuest = function(index) {
            appData.quests.splice(index, 1);
            saveState(); renderUI();
        }

        function renderSkills() {
            const container = document.getElementById("skills-container");
            container.innerHTML = "";
            appData.skills.forEach(s => {
                const card = document.createElement("div");
                card.className = "bg-darkCard border border-darkBorder p-3.5 rounded-2xl flex justify-between items-center font-mono";
                card.innerHTML = `
                    <div>
                        <span class="text-[9px] text-cyanGlow uppercase">Nv.${s.level} / ${s.maxLvl} // ${s.type}</span>
                        <h4 class="text-xs font-bold text-slate-200">${s.name}</h4>
                        <p class="text-[10px] text-goldAccent font-sans mt-0.5">${s.bonus}</p>
                    </div>
                    <div class="text-right">
                        <span class="text-[10px] text-slate-400 block">${s.reps} / ${s.targetReps} Reps</span>
                        <div class="w-16 h-1.5 bg-darkBg rounded-full border border-darkBorder mt-1 overflow-hidden">
                            <div class="bg-cyanGlow h-full" style="width: ${(s.reps / s.targetReps) * 100}%"></div>
                        </div>
                    </div>
                `;
                container.appendChild(card);
            });
        }

        function renderTitles() {
            const container = document.getElementById("titles-container");
            container.innerHTML = "";
            appData.titles.forEach(t => {
                const isActive = t.id === appData.activeTitleId;
                const card = document.createElement("div");
                card.className = `p-3.5 rounded-2xl border font-mono flex justify-between items-center ${isActive ? 'bg-purpleDao/10 border-purpleDao' : 'bg-darkCard border-darkBorder'}`;
                card.innerHTML = `
                    <div>
                        <span class="text-[9px] text-purpleDao uppercase font-bold">${t.req}</span>
                        <h4 class="text-xs font-bold text-slate-200">${t.name}</h4>
                        <p class="text-[10px] text-slate-400 font-sans">${t.passive}</p>
                    </div>
                    <button onclick="equipTitle('${t.id}')" ${!t.unlocked ? 'disabled' : ''} class="px-3 py-1.5 rounded-xl text-xs font-bold ${isActive ? 'bg-purpleDao text-darkBg' : 'bg-darkBg border border-darkBorder text-slate-400'}">
                        ${isActive ? 'Équipé' : (t.unlocked ? 'Équiper' : 'Verrouillé')}
                    </button>
                `;
                container.appendChild(card);
            });
        }

        window.equipTitle = function(id) {
            appData.activeTitleId = id;
            saveState(); renderUI();
        }

        // TRIBULATION CÉLESTE MULTIMODALE (SIMULATION VIDÉO & PHOTO PROBLÈME)
        document.getElementById("breakthrough-btn").addEventListener("click", () => {
            const modal = document.getElementById("breakthrough-modal");
            const body = document.getElementById("tribulation-body");
            
            // Alternance Épreuve Physique / Épreuve Math/Physique
            currentTribulationType = Math.random() > 0.5 ? 'physical' : 'mental';

            if (currentTribulationType === 'physical') {
                body.innerHTML = `
                    <div class="p-3 bg-darkBg rounded-xl border border-darkBorder space-y-2">
                        <span class="text-[10px] text-goldAccent font-mono block">ÉPREUVE PHYSIQUE // HANDSTAND / POSTURE</span>
                        <p class="text-slate-300 text-xs">Exécutez un <strong>Handstand (équilibre sur les mains)</strong> ou du gainage strict pendant 30s. Téléversez la vidéo d'analyse pour l'IA.</p>
                        <input type="file" id="tribulation-video-input" accept="video/*" class="w-full text-xs text-slate-400 bg-darkCard p-2 rounded-xl border border-darkBorder">
                    </div>
                `;
            } else {
                const n1 = Math.floor(Math.random() * 20) + 10;
                const n2 = Math.floor(Math.random() * 15) + 5;
                currentMentalAnswer = n1 * n2;

                body.innerHTML = `
                    <div class="p-3 bg-darkBg rounded-xl border border-darkBorder space-y-2">
                        <span class="text-[10px] text-cyanGlow font-mono block">ÉPREUVE ACADÉMIQUE // PHYSIQUE & MATHS</span>
                        <p class="text-slate-300 text-xs">Calculez le produit de la matrice d'onde : <strong>${n1} × ${n2}</strong>.</p>
                        <input type="number" id="tribulation-math-input" placeholder="Résultat du calcul..." class="w-full bg-darkCard border border-darkBorder rounded-xl p-2.5 text-slate-200 font-mono text-xs outline-none">
                        <label class="block text-[10px] text-slate-400 mt-2">Photo de la feuille de brouillon (IA Scan) :</label>
                        <input type="file" id="tribulation-photo-input" accept="image/*" class="w-full text-xs text-slate-400 bg-darkCard p-2 rounded-xl border border-darkBorder">
                    </div>
                `;
            }

            modal.classList.remove("opacity-0", "pointer-events-none");
        });

        document.getElementById("submit-tribulation-btn").addEventListener("click", () => {
            const statusEl = document.getElementById("tribulation-status");
            statusEl.classList.remove("hidden");

            if (currentTribulationType === 'physical') {
                const videoInput = document.getElementById("tribulation-video-input");
                if (!videoInput.files || videoInput.files.length === 0) {
                    statusEl.className = "text-xs font-mono p-2.5 rounded-xl text-center bg-systemRed/20 text-systemRed border border-systemRed/40";
                    statusEl.innerText = "⛔ ERREUR : Veuillez joindre la vidéo de la performance.";
                    return;
                }
            } else {
                const ans = parseInt(document.getElementById("tribulation-math-input").value);
                if (ans !== currentMentalAnswer) {
                    statusEl.className = "text-xs font-mono p-2.5 rounded-xl text-center bg-systemRed/20 text-systemRed border border-systemRed/40";
                    statusEl.innerText = "⛔ CALCUL INCORRECT : Revoir le brouillon.";
                    return;
                }
            }

            // ÉCRAN DE RÉUSSITE D'ÉLEVATION
            statusEl.className = "text-xs font-mono p-2.5 rounded-xl text-center bg-jadeGreen/20 text-jadeGreen border border-jadeGreen/40";
            statusEl.innerText = "✅ TRIBULATION SURMONTÉE ! ÉLEVATION EN COURS...";

            setTimeout(() => {
                appData.qi = 0;
                appData.currentRealmIdx = Math.min(MASTER_REALMS.length - 1, appData.currentRealmIdx + 1);
                loadRealmQuests(appData.currentRealmIdx);
                saveState();
                renderUI();
                document.getElementById("breakthrough-modal").classList.add("opacity-0", "pointer-events-none");
            }, 1000);
        });

        document.getElementById("close-breakthrough-btn").addEventListener("click", () => {
            document.getElementById("breakthrough-modal").classList.add("opacity-0", "pointer-events-none");
        });

        // RECOLTER QI SECTE IDLE
        document.getElementById("claim-idle-qi-btn").addEventListener("click", () => {
            if (appData.idleQi <= 0) return;
            appData.qi += Math.round(appData.idleQi);
            appData.idleQi = 0;
            saveState(); renderUI();
        });

        // RUINES ANTIQUES (ÉMIGMES LOGIQUES)
        document.getElementById("open-ruins-btn").addEventListener("click", () => {
            document.getElementById("ruins-riddle-text").innerText = "« Plus je suis présent, moins on me voit. Que suis-je ? »";
            document.getElementById("ruins-answer-input").value = "";
            document.getElementById("ruins-status").className = "hidden text-xs font-mono p-2 rounded-xl text-center";
            document.getElementById("ruins-modal").classList.remove("opacity-0", "pointer-events-none");
        });

        document.getElementById("submit-ruins-btn").addEventListener("click", () => {
            const ans = document.getElementById("ruins-answer-input").value.trim().toLowerCase();
            const statusEl = document.getElementById("ruins-status");
            statusEl.classList.remove("hidden");

            if (ans.includes("obscurité") || ans.includes("ombre") || ans.includes("noir")) {
                statusEl.className = "text-xs font-mono p-2 rounded-xl text-center bg-jadeGreen/20 text-jadeGreen";
                statusEl.innerText = "✅ TRÉSOR DÉBLOQUÉ : +40 Units de Qi !";
                appData.qi += 40;
                saveState();
                setTimeout(() => {
                    document.getElementById("ruins-modal").classList.add("opacity-0", "pointer-events-none");
                    renderUI();
                }, 800);
            } else {
                statusEl.className = "text-xs font-mono p-2 rounded-xl text-center bg-systemRed/20 text-systemRed";
                statusEl.innerText = "⛔ RÉPONSE INCORRECTE.";
            }
        });

        document.getElementById("close-ruins-btn").addEventListener("click", () => {
            document.getElementById("ruins-modal").classList.add("opacity-0", "pointer-events-none");
        });

        // CHAT TERMINAL & SCAN FAILLES
        function renderChat() {
            const container = document.getElementById("master-chat-messages");
            container.innerHTML = "";
            appData.chatHistory.forEach(msg => {
                const isUser = msg.sender === 'user';
                const bubble = document.createElement("div");
                bubble.className = `flex gap-2.5 ${isUser ? 'justify-end' : 'justify-start'}`;
                bubble.innerHTML = `
                    <div class="max-w-[85%] p-3 rounded-2xl text-xs font-sans ${isUser ? 'bg-cyanGlow text-darkBg font-semibold' : 'bg-darkBg border border-darkBorder text-slate-200'}">
                        ${msg.text}
                    </div>
                `;
                container.appendChild(bubble);
            });
            container.scrollTop = container.scrollHeight;
        }

        document.getElementById("run-appraisal-scan-btn").addEventListener("click", () => {
            appData.chatHistory.push({ sender: "system", text: "🔍 [ANALYSE SYSTEME] Faible volume de quêtes d'Esprit aujourd'hui. Risque de stagnation cognitive." });
            saveState(); renderUI();
        });

        document.getElementById("master-chat-form").addEventListener("submit", (e) => {
            e.preventDefault();
            const input = document.getElementById("master-chat-input");
            const val = input.value.trim();
            if (!val) return;
            input.value = "";
            appData.chatHistory.push({ sender: "user", text: val });
            appData.chatHistory.push({ sender: "system", text: "Rapport consigné dans le Journal d'Analyse." });
            saveState(); renderUI();
        });

        document.getElementById("clear-chat-btn").addEventListener("click", () => {
            appData.chatHistory = [{ sender: "system", text: "Terminal réinitialisé." }];
            saveState(); renderUI();
        });

        // ADD CUSTOM QUEST
        const questModal = document.getElementById("quest-modal");
        document.getElementById("add-quest-modal-btn").addEventListener("click", () => questModal.classList.remove("opacity-0", "pointer-events-none"));
        document.getElementById("cancel-quest-btn").addEventListener("click", () => questModal.classList.add("opacity-0", "pointer-events-none"));

        document.getElementById("save-quest-btn").addEventListener("click", () => {
            const title = document.getElementById("custom-quest-title").value.trim();
            const cat = document.getElementById("custom-quest-cat").value;
            const isMandatory = document.getElementById("custom-quest-req").value === 'mandatory';
            const qiVal = parseInt(document.getElementById("custom-quest-qi").value) || 30;

            if (!title) return;

            appData.quests.push({
                id: 'q_' + Date.now(),
                title: title,
                desc: "Directive personnalisée.",
                qi: qiVal,
                cat: cat,
                mandatory: isMandatory,
                minTime: 20,
                completed: false,
                proof: ""
            });

            document.getElementById("custom-quest-title").value = "";
            questModal.classList.add("opacity-0", "pointer-events-none");
            saveState(); renderUI();
        });

        // EXPORT IMPORT JSON
        const exportModal = document.getElementById("export-import-modal");
        document.getElementById("export-import-btn").addEventListener("click", () => exportModal.classList.remove("opacity-0", "pointer-events-none"));
        document.getElementById("close-export-modal-btn").addEventListener("click", () => exportModal.classList.add("opacity-0", "pointer-events-none"));

        document.getElementById("export-json-btn").addEventListener("click", () => {
            const dataStr = "data:text/json;charset=utf-8," + encodeURIComponent(JSON.stringify(appData, null, 2));
            const a = document.createElement('a');
            a.setAttribute("href", dataStr);
            a.setAttribute("download", `system_core_v5_${new Date().toISOString().slice(0,10)}.json`);
            a.click();
        });

        document.getElementById("import-json-input").addEventListener("change", (e) => {
            const file = e.target.files[0];
            if (!file) return;
            const reader = new FileReader();
            reader.onload = function(evt) {
                try {
                    appData = { ...appData, ...JSON.parse(evt.target.result) };
                    saveState(); renderUI();
                    exportModal.classList.add("opacity-0", "pointer-events-none");
                } catch(err) { alert("JSON Invalide."); }
            };
            reader.readAsText(file);
        });

        loadState();
        renderUI();
    </script>
</body>
</html>
