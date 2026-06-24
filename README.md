<!DOCTYPE html>
<html lang="pt-BR" class="h-full bg-neutral-950">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Portal de Treinamento Ampernet Telecom</title>
    <!-- Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- FontAwesome Icons -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <!-- Google Fonts -->
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700;800&display=swap" rel="stylesheet">
    <style>
        body {
            font-family: 'Inter', sans-serif;
        }
        /* Custom scrollbar for simulated chats and general view */
        .chat-scrollbar::-webkit-scrollbar {
            width: 5px;
        }
        .chat-scrollbar::-webkit-scrollbar-track {
            background: rgba(255, 255, 255, 0.02);
        }
        .chat-scrollbar::-webkit-scrollbar-thumb {
            background: rgba(239, 68, 68, 0.3);
            border-radius: 3px;
        }
        .chat-scrollbar::-webkit-scrollbar-thumb:hover {
            background: rgba(239, 68, 68, 0.6);
        }
    </style>
</head>
<body class="h-full flex flex-col text-neutral-100 bg-neutral-950">

    <!-- TELA DE IDENTIFICAÇÃO OBRIGATÓRIA (LOGIN SCREEN) -->
    <div id="name-entry-modal" class="fixed inset-0 bg-neutral-950 z-[100] flex items-center justify-center p-4 transition-all duration-300">
        <div class="bg-neutral-900 border border-red-600/30 rounded-3xl p-8 max-w-md w-full text-center space-y-6 shadow-2xl relative">
            <div class="absolute top-0 left-1/2 -translate-x-1/2 -translate-y-1/2 bg-neutral-950 p-3 rounded-2xl border border-red-600/20 shadow-lg">
                <img src="image_bdffa5.png" alt="Ampernet Telecom" class="h-12 w-12 object-contain">
            </div>
            
            <div class="pt-6">
                <h2 class="text-xl font-extrabold tracking-tight text-white uppercase">Identificação do Técnico</h2>
                <p class="text-xs text-neutral-400 mt-2 leading-relaxed">Bem-vindo ao Portal de Capacitação Ampernet. Por favor, insira seu nome completo para iniciar o treinamento e vincular à sua certificação.</p>
            </div>

            <div class="space-y-3">
                <div class="relative">
                    <span class="absolute inset-y-0 left-0 flex items-center pl-3.5 text-neutral-500">
                        <i class="fas fa-user"></i>
                    </span>
                    <input type="text" id="tech-name-input" placeholder="Seu Nome Completo" class="w-full bg-neutral-950 border border-neutral-800 rounded-xl pl-10 pr-4 py-3.5 text-sm text-white focus:outline-none focus:border-red-600 transition">
                </div>
                <p id="name-error" class="text-[10px] text-red-500 hidden font-semibold text-left"><i class="fas fa-exclamation-triangle mr-1"></i> Por favor, digite seu nome completo para continuar.</p>
            </div>

            <button onclick="submitTechnicianName()" class="w-full bg-red-600 hover:bg-red-700 text-white font-bold py-3.5 rounded-xl shadow-md transition transform active:scale-95 flex items-center justify-center gap-2">
                <span>Acessar Treinamento</span>
                <i class="fas fa-arrow-right"></i>
            </button>
        </div>
    </div>

    <!-- HEADER DE NAVEGAÇÃO -->
    <header class="bg-neutral-900 border-b border-red-600/30 text-white shadow-lg shrink-0">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-4 flex flex-col sm:flex-row justify-between items-center gap-4">
            <!-- Brand & Logo -->
            <div class="flex items-center gap-3">
                <div class="bg-neutral-950 p-1.5 rounded-xl shadow-md border border-red-600/20 flex items-center justify-center">
                    <img src="image_bdffa5.png" alt="Ampernet Telecom Logo" class="h-10 w-10 object-contain rounded-lg" onerror="this.src='https://placehold.co/40x40/ef4444/ffffff?text=A'">
                </div>
                <div>
                    <h1 class="text-xl font-extrabold tracking-tight text-white flex items-center gap-1.5">
                        AMPERNET <span class="text-red-500 font-light">TELECOM</span>
                    </h1>
                    <p class="text-[10px] text-neutral-400 uppercase tracking-wider font-semibold">Portal de Treinamento de Comunicação & Processos</p>
                </div>
            </div>

            <!-- Gamificação / Estatísticas do Aluno -->
            <div class="flex items-center gap-6 bg-neutral-950 px-4 py-2 rounded-xl border border-red-600/20">
                <div class="text-center sm:text-right">
                    <span class="block text-[10px] uppercase text-neutral-400 font-bold tracking-wider">Pontuação Total</span>
                    <span id="user-points" class="text-lg font-extrabold text-red-500"><i class="fas fa-fire mr-1"></i> 0 XP</span>
                </div>
                <div class="h-8 w-[1px] bg-neutral-800"></div>
                <div>
                    <span class="block text-[10px] uppercase text-neutral-400 font-bold tracking-wider">Progresso Geral</span>
                    <div class="flex items-center gap-2 mt-1">
                        <div class="w-24 bg-neutral-800 rounded-full h-2">
                            <div id="progress-bar" class="bg-red-600 h-2 rounded-full transition-all duration-500 shadow-[0_0_8px_rgba(239,68,68,0.5)]" style="width: 0%"></div>
                        </div>
                        <span id="progress-text" class="text-xs font-bold text-red-400">0%</span>
                    </div>
                </div>
            </div>
        </div>
    </header>

    <!-- CONTAINER PRINCIPAL -->
    <div class="flex-1 max-w-7xl w-full mx-auto px-4 sm:px-6 lg:px-8 py-8 flex flex-col lg:flex-row gap-8 overflow-hidden">
        
        <!-- SIDEBAR DE SELEÇÃO DE MÓDULOS -->
        <aside class="w-full lg:w-72 shrink-0 flex flex-col gap-4">
            <div class="bg-neutral-900 rounded-2xl shadow-sm border border-neutral-800 p-5">
                <h3 class="text-xs uppercase font-extrabold text-neutral-400 tracking-wider mb-4">Módulos de Capacitação</h3>
                <nav class="space-y-2" aria-label="Sidebar">
                    <!-- Menu Item Dashboard -->
                    <button onclick="switchTab('dashboard')" id="btn-tab-dashboard" class="tab-btn w-full flex items-center justify-between px-4 py-3 rounded-xl text-left font-semibold transition-all bg-red-600/10 text-red-500 border border-red-500/20 shadow-sm">
                        <div class="flex items-center gap-3">
                            <i class="fas fa-chart-line text-lg"></i>
                            <span>Painel de Início</span>
                        </div>
                        <i class="fas fa-chevron-right text-xs opacity-50"></i>
                    </button>

                    <!-- Menu Item Módulo 1 -->
                    <button onclick="switchTab('modulo1')" id="btn-tab-modulo1" class="tab-btn w-full flex items-center justify-between px-4 py-3 rounded-xl text-left font-medium transition-all text-neutral-400 hover:bg-neutral-800 hover:text-neutral-100">
                        <div class="flex items-center gap-3">
                            <i class="fab fa-whatsapp text-lg text-emerald-500"></i>
                            <span>1. Canais & Links</span>
                        </div>
                        <span id="badge-m1" class="text-[10px] px-2.5 py-0.5 rounded-full bg-neutral-850 text-neutral-400 font-bold">Pendente</span>
                    </button>

                    <!-- Menu Item Módulo 2 -->
                    <button onclick="switchTab('modulo2')" id="btn-tab-modulo2" class="tab-btn w-full flex items-center justify-between px-4 py-3 rounded-xl text-left font-medium transition-all text-neutral-400 hover:bg-neutral-800 hover:text-neutral-100">
                        <div class="flex items-center gap-3">
                            <i class="fab fa-telegram text-lg text-sky-500"></i>
                            <span>2. Ampernet Interno Bot</span>
                        </div>
                        <span id="badge-m2" class="text-[10px] px-2.5 py-0.5 rounded-full bg-neutral-850 text-neutral-400 font-bold">Pendente</span>
                    </button>

                    <!-- Menu Item Módulo 3 -->
                    <button onclick="switchTab('modulo3')" id="btn-tab-modulo3" class="tab-btn w-full flex items-center justify-between px-4 py-3 rounded-xl text-left font-medium transition-all text-neutral-400 hover:bg-neutral-800 hover:text-neutral-100">
                        <div class="flex items-center gap-3">
                            <i class="fas fa-tools text-lg text-red-500"></i>
                            <span>3. SuperAmpbot</span>
                        </div>
                        <span id="badge-m3" class="text-[10px] px-2.5 py-0.5 rounded-full bg-neutral-850 text-neutral-400 font-bold">Pendente</span>
                    </button>

                    <!-- Menu Item Módulo 4 -->
                    <button onclick="switchTab('modulo4')" id="btn-tab-modulo4" class="tab-btn w-full flex items-center justify-between px-4 py-3 rounded-xl text-left font-medium transition-all text-neutral-400 hover:bg-neutral-800 hover:text-neutral-100">
                        <div class="flex items-center gap-3">
                            <i class="fas fa-network-wired text-lg text-red-400"></i>
                            <span>4. CST & Indicações</span>
                        </div>
                        <span id="badge-m4" class="text-[10px] px-2.5 py-0.5 rounded-full bg-neutral-850 text-neutral-400 font-bold">Pendente</span>
                    </button>

                    <!-- Menu Item Quiz -->
                    <button onclick="switchTab('quiz')" id="btn-tab-quiz" class="tab-btn w-full flex items-center justify-between px-4 py-3 rounded-xl text-left font-medium transition-all text-slate-500 hover:bg-neutral-800/50 border border-dashed border-neutral-800 mt-4 cursor-not-allowed">
                        <div class="flex items-center gap-3">
                            <i class="fas fa-graduation-cap text-lg text-red-400"></i>
                            <span class="font-bold">Avaliação Final</span>
                        </div>
                        <span id="badge-quiz" class="text-[10px] px-2.5 py-0.5 rounded-full bg-neutral-900 text-neutral-600 border border-neutral-800 font-bold">Trancado</span>
                    </button>
                </nav>
            </div>

            <!-- Card Técnico Rápido -->
            <div class="bg-gradient-to-br from-neutral-900 to-neutral-950 text-white rounded-2xl p-5 border border-neutral-800 shadow-sm">
                <h4 class="text-xs uppercase font-extrabold text-red-400 tracking-wider mb-3">Links Oficiais Ampernet</h4>
                <div class="space-y-3 text-xs text-neutral-300">
                    <a href="https://t.me/amper_opa_bot" target="_blank" class="flex items-center gap-2 hover:text-red-400 transition">
                        <i class="fab fa-telegram text-sky-400"></i> @amper_opa_bot
                    </a>
                    <a href="https://t.me/SuperAmpbot" target="_blank" class="flex items-center gap-2 hover:text-red-400 transition">
                        <i class="fab fa-telegram text-sky-400"></i> @SuperAmpbot
                    </a>
                    <a href="https://chat.whatsapp.com/DwPRHvP4BW9DDfzS0cwljL" target="_blank" class="flex items-center gap-2 hover:text-red-400 transition">
                        <i class="fab fa-whatsapp text-emerald-400"></i> Grupo de Indicações
                    </a>
                </div>
            </div>
        </aside>

        <!-- ÁREA PRINCIPAL DE CONTEÚDO -->
        <main class="flex-1 bg-neutral-900 rounded-3xl shadow-sm border border-neutral-800 p-6 sm:p-8 overflow-y-auto min-h-[500px]">

            <!-- TAB: DASHBOARD / BOAS-VINDAS -->
            <section id="tab-dashboard" class="tab-content block space-y-6">
                <div class="border-b border-neutral-800 pb-5">
                    <span class="text-xs uppercase tracking-wider font-extrabold text-red-500 bg-red-950/40 border border-red-500/20 px-2.5 py-1 rounded-md">Capacitação Inicial</span>
                    <h2 class="text-2xl sm:text-3xl font-extrabold text-white mt-2">Bem-vindo ao Portal de Treinamento Ampernet</h2>
                    <p class="text-neutral-400 mt-1">Este espaço foi desenhado exclusivamente para preparar nossa equipe de telecomunicações nos fluxos de comunicação intersetorial, requisições automatizadas e procedimentos operacionais.</p>
                </div>

                <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                    <div class="bg-gradient-to-r from-neutral-950 to-neutral-900 p-6 rounded-2xl border border-neutral-800 flex gap-4">
                        <div class="text-red-500 text-3xl"><i class="fas fa-info-circle"></i></div>
                        <div>
                            <h3 class="font-bold text-white">Como funciona o treinamento?</h3>
                            <p class="text-xs text-neutral-400 mt-1 leading-relaxed">Navegue sequencialmente pelos módulos na barra lateral. Complete as simulações interativas dos bots de Telegram para acumular XP e liberar sua avaliação final!</p>
                        </div>
                    </div>

                    <div class="bg-gradient-to-r from-neutral-950 to-neutral-900 p-6 rounded-2xl border border-neutral-800 flex gap-4">
                        <div class="text-red-500 text-3xl"><i class="fas fa-award"></i></div>
                        <div>
                            <h3 class="font-bold text-white">Certificado de Proficiência</h3>
                            <p class="text-xs text-neutral-400 mt-1 leading-relaxed">Ao finalizar todas as tarefas e alcançar no mínimo 80% de aproveitamento na Avaliação Final, você emitirá seu Certificado Oficial de Comunicação de Setores Ampernet.</p>
                        </div>
                    </div>
                </div>

                <div>
                    <h3 class="font-bold text-neutral-200 text-lg mb-4">Seu Progresso de Aprendizado</h3>
                    <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-4">
                        <!-- Módulo 1 Status -->
                        <div class="border border-neutral-800 bg-neutral-950/40 p-4 rounded-xl flex items-center justify-between">
                            <div>
                                <span class="text-xs text-neutral-500 block font-medium">Módulo 1</span>
                                <span class="font-bold text-neutral-300 text-sm">Canais & Links</span>
                            </div>
                            <span id="status-card-m1" class="text-xs px-2.5 py-1 rounded-full bg-neutral-900 text-red-500 font-semibold border border-red-500/10">Pendente</span>
                        </div>
                        <!-- Módulo 2 Status -->
                        <div class="border border-neutral-800 bg-neutral-950/40 p-4 rounded-xl flex items-center justify-between">
                            <div>
                                <span class="text-xs text-neutral-500 block font-medium">Módulo 2</span>
                                <span class="font-bold text-neutral-300 text-sm">Ampernet Bot</span>
                            </div>
                            <span id="status-card-m2" class="text-xs px-2.5 py-1 rounded-full bg-neutral-900 text-red-500 font-semibold border border-red-500/10">Pendente</span>
                        </div>
                        <!-- Módulo 3 Status -->
                        <div class="border border-neutral-800 bg-neutral-950/40 p-4 rounded-xl flex items-center justify-between">
                            <div>
                                <span class="text-xs text-neutral-500 block font-medium">Módulo 3</span>
                                <span class="font-bold text-neutral-300 text-sm">SuperAmpbot</span>
                            </div>
                            <span id="status-card-m3" class="text-xs px-2.5 py-1 rounded-full bg-neutral-900 text-red-500 font-semibold border border-red-500/10">Pendente</span>
                        </div>
                        <!-- Módulo 4 Status -->
                        <div class="border border-neutral-800 bg-neutral-950/40 p-4 rounded-xl flex items-center justify-between">
                            <div>
                                <span class="text-xs text-neutral-500 block font-medium">Módulo 4</span>
                                <span class="font-bold text-neutral-300 text-sm">CST & Indicações</span>
                            </div>
                            <span id="status-card-m4" class="text-xs px-2.5 py-1 rounded-full bg-neutral-900 text-red-500 font-semibold border border-red-500/10">Pendente</span>
                        </div>
                    </div>
                </div>

                <div class="pt-6 border-t border-neutral-800 flex justify-end">
                    <button onclick="switchTab('modulo1')" class="bg-red-600 hover:bg-red-700 text-white font-bold px-6 py-3 rounded-xl shadow-md hover:shadow-lg transform active:scale-95 transition flex items-center gap-2">
                        <span>Iniciar Treinamento</span>
                        <i class="fas fa-arrow-right"></i>
                    </button>
                </div>
            </section>

            <!-- TAB: MÓDULO 1: CANAIS & LINKS -->
            <section id="tab-modulo1" class="tab-content hidden space-y-6">
                <div class="border-b border-neutral-800 pb-5">
                    <span class="text-xs uppercase tracking-wider font-extrabold text-red-500 bg-red-950/40 border border-red-500/20 px-2.5 py-1 rounded-md">Módulo 1</span>
                    <h2 class="text-2xl font-extrabold text-white mt-2">Canais de Comunicação & Onde Encontrá-los</h2>
                    <p class="text-neutral-400 mt-1">A comunicação ágil começa no local correto. Todos os nossos técnicos e colaboradores operacionais estão incluídos no grupo de WhatsApp oficial de comunicação.</p>
                </div>

                <!-- Simulação Visual do Grupo de WhatsApp -->
                <div class="bg-neutral-950 p-4 rounded-2xl max-w-lg mx-auto border border-neutral-800">
                    <h4 class="text-xs text-neutral-400 font-bold mb-2 uppercase tracking-wide"><i class="fab fa-whatsapp text-emerald-500 mr-1"></i> Representação do Grupo Interno</h4>
                    <div class="bg-emerald-950 text-white rounded-xl overflow-hidden shadow-md">
                        <!-- Top Bar -->
                        <div class="bg-emerald-900 p-3 flex items-center justify-between border-b border-emerald-800">
                            <div class="flex items-center gap-3">
                                <!-- Logo Ampernet no WhatsApp Grupo -->
                                <img src="image_bdffa5.png" alt="Ampernet" class="h-9 w-9 object-contain rounded-full bg-white p-1">
                                <div>
                                    <h5 class="text-sm font-bold leading-none">INFORMATIVO SUP E SERVIÇO</h5>
                                    <span class="text-[10px] text-emerald-300">Grupo · 171 membros</span>
                                </div>
                            </div>
                            <i class="fas fa-ellipsis-v text-sm text-emerald-300 cursor-pointer"></i>
                        </div>
                        <!-- Grupo Descrição -->
                        <div class="p-4 bg-[#0e1111] text-slate-200 text-xs space-y-3">
                            <div class="bg-neutral-900 p-3 rounded-lg shadow-sm border border-neutral-800">
                                <p class="font-semibold text-neutral-400 text-[10px] uppercase mb-1">Descrição do Grupo (Informações Importantes)</p>
                                <p class="text-neutral-300 mb-2 leading-relaxed">Todos os colaboradores do nosso setor estão incluídos neste grupo, usado para avisos e comunicação direta.</p>
                                <div class="space-y-1 text-red-400 font-medium font-mono text-[11px] bg-neutral-950 p-2.5 rounded-md border border-neutral-800">
                                    <p class="text-neutral-400 text-[10px] uppercase mb-1 font-sans">LINKS CRUCIAIS DE SUPORTE:</p>
                                    <p>🤖 Link bot Telegram: <a href="https://t.me/amper_opa_bot" class="underline text-red-500 hover:text-red-400">https://t.me/amper_opa_bot</a></p>
                                    <p>⚙️ Bot pedido de ferramentas: <a href="https://t.me/SuperAmpbot" class="underline text-red-500 hover:text-red-400">https://t.me/SuperAmpbot</a></p>
                                    <p>📉 Bot cst sinal degradado: <a href="https://t.me/amper_opa_bot" class="underline text-red-500 hover:text-red-400">https://t.me/amper_opa_bot</a></p>
                                    <p>🔗 Link Grupo Indicações: <a href="https://chat.whatsapp.com/DwPRHvP4BW9DDfzS0cwljL" class="underline text-red-500 hover:text-red-400">https://chat.whatsapp.com/...</a></p>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>

                <div class="bg-red-950/20 border border-red-900/40 rounded-xl p-5 flex gap-4">
                    <div class="text-red-500 text-2xl"><i class="fas fa-exclamation-triangle"></i></div>
                    <div class="text-sm text-red-200 leading-relaxed">
                        <strong class="block mb-1 text-white">Regra de Ouro da Descrição:</strong>
                        Muitas dúvidas operacionais corriqueiras podem ser resolvidas de forma ágil simplesmente checando a <strong>descrição do grupo de WhatsApp do setor</strong>. Lá você tem acesso imediato e direto aos links dos bots de automação.
                    </div>
                </div>

                <div class="pt-6 border-t border-neutral-800 flex justify-between items-center">
                    <span class="text-sm text-neutral-400">Leia a descrição acima e avance.</span>
                    <button onclick="completarModulo1()" class="bg-red-600 hover:bg-red-700 text-white font-bold px-5 py-2.5 rounded-xl flex items-center gap-2 transition shadow-[0_0_12px_rgba(239,68,68,0.3)]">
                        <span>Concluir & Ir para Módulo 2</span>
                        <i class="fas fa-check"></i>
                    </button>
                </div>
            </section>

            <!-- TAB: MÓDULO 2: AMPERNET INTERNO BOT -->
            <section id="tab-modulo2" class="tab-content hidden space-y-6">
                <div class="border-b border-neutral-800 pb-5">
                    <span class="text-xs uppercase tracking-wider font-extrabold text-red-500 bg-red-950/40 border border-red-500/20 px-2.5 py-1 rounded-md">Módulo 2</span>
                    <h2 class="text-2xl font-extrabold text-white mt-2">Ampernet Interno Bot (@amper_opa_bot)</h2>
                    <p class="text-neutral-400 mt-1">Este bot do Telegram é a porta de entrada para a comunicação interna estruturada da Ampernet. Com ele, você encaminha suas dúvidas de forma direta para o setor correto sem perda de tempo ou ruídos de comunicação.</p>
                </div>

                <div class="grid grid-cols-1 lg:grid-cols-12 gap-8">
                    <!-- Instruções Teóricas -->
                    <div class="lg:col-span-5 space-y-4 text-sm text-neutral-300">
                        <h3 class="font-bold text-white text-base">Instruções de Fluxo</h3>
                        <p class="leading-relaxed">Ao acessar o bot no Telegram:</p>
                        <ul class="list-decimal pl-4 space-y-2 text-neutral-400">
                            <li>Envie o comando <code class="bg-neutral-950 text-red-400 px-1.5 py-0.5 rounded font-mono border border-neutral-800">/start</code> para iniciar seu atendimento.</li>
                            <li>O sistema gerará um número exclusivo de <strong>Protocolo de Atendimento</strong> (ex: <code class="bg-neutral-950 text-red-500 px-1 rounded font-mono border border-neutral-800">AMP20263488659</code>).</li>
                            <li>Em seguida, selecione o setor que você necessita contatar digitando o número correspondente à opção desejada.</li>
                        </ul>
                        <div class="bg-neutral-950 border border-neutral-800 rounded-xl p-4 mt-2">
                            <span class="block font-bold text-white mb-2 text-xs uppercase tracking-wider text-red-400">Setores Disponíveis (Pág. 3):</span>
                            <div class="grid grid-cols-2 gap-y-1.5 gap-x-2 text-xs text-neutral-300 font-medium">
                                <span>1. Financeiro</span>
                                <span>2. Suprimentos</span>
                                <span>3. Administrativo</span>
                                <span>4. Comercial</span>
                                <span class="text-red-400 font-bold">5. Suporte e Serviços</span>
                                <span>6. Recursos Humanos</span>
                                <span>7. Serviços e Tecnologia</span>
                                <span>8. NOC (Redes)</span>
                            </div>
                        </div>
                    </div>

                    <!-- Simulador Interativo Telegram -->
                    <div class="lg:col-span-7 flex flex-col">
                        <div class="bg-neutral-950 p-4 rounded-3xl border border-neutral-800">
                            <div class="bg-[#182533] text-white rounded-2xl shadow-xl overflow-hidden max-w-sm mx-auto flex flex-col h-[480px]">
                                <!-- Header Telegram -->
                                <div class="bg-[#202b36] p-3 flex items-center justify-between border-b border-[#141d26]">
                                    <div class="flex items-center gap-3">
                                        <!-- Logo do Telegram na imagem de contato -->
                                        <div class="h-9 w-9 rounded-full bg-[#5288c1] flex items-center justify-center text-white shrink-0 shadow-inner">
                                            <svg class="h-5 w-5 fill-current" viewBox="0 0 24 24">
                                                <path d="M12 .5C5.37.5 0 5.87 0 12.5S5.37 24.5 12 24.5 24 19.13 24 12.5 18.63.5 12 .5zm5.56 8.18l-1.89 8.9c-.14.63-.52.79-1.05.49l-2.88-2.12-1.39 1.34c-.15.15-.28.28-.58.28l.21-2.94 5.35-4.83c.23-.21-.05-.32-.36-.12L9.36 13.5l-2.85-.89c-.62-.19-.63-.62.13-.92l11.13-4.29c.52-.19.97.12.79.78z"/>
                                            </svg>
                                        </div>
                                        <div>
                                            <h4 class="text-xs font-bold leading-none text-white">Ampernet Interno Bot</h4>
                                            <span class="text-[9px] text-red-400">bot oficial de triagem</span>
                                        </div>
                                    </div>
                                    <div class="flex gap-3 text-slate-400 text-xs">
                                        <i class="fas fa-search"></i>
                                        <i class="fas fa-ellipsis-v"></i>
                                    </div>
                                </div>

                                <!-- Mensagens Chat -->
                                <div id="m2-chat-area" class="flex-1 p-3 overflow-y-auto space-y-3 chat-scrollbar bg-[#0e1621] text-xs">
                                    <div class="text-center my-2 text-slate-500 text-[10px]">Hoje</div>
                                    <!-- Bot start guide hint -->
                                    <div class="text-center my-1 bg-[#182533] text-slate-300 inline-block px-3 py-1.5 rounded-md mx-auto max-w-[85%] text-[10px] leading-relaxed">
                                        Toque no botão vermelho ou digite no campo abaixo para iniciar o simulador.
                                    </div>
                                </div>

                                <!-- Input e Controle Interativo de Simulação -->
                                <div class="p-3 bg-[#17212b] border-t border-[#101921] flex flex-col gap-2">
                                    <div id="m2-actions-container" class="flex flex-wrap gap-1.5 justify-center py-1">
                                        <button onclick="m2SendStart()" id="btn-m2-start" class="bg-red-600 hover:bg-red-500 text-white px-4 py-1.5 rounded-full font-bold text-[10px] tracking-wide transition shadow-md shadow-red-900/20">
                                            Enviar /start
                                        </button>
                                    </div>
                                    <div class="flex items-center gap-2 bg-[#24303f] px-3 py-2 rounded-xl text-slate-400">
                                        <input type="text" id="m2-text-input" disabled class="flex-1 bg-transparent border-none outline-none text-white text-[11px] placeholder-slate-500" placeholder="Aguardando ação...">
                                        <button onclick="m2SubmitText()" id="btn-m2-send" disabled class="text-slate-500 hover:text-red-400 transition">
                                            <i class="far fa-paper-plane"></i>
                                        </button>
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>

                <div class="pt-6 border-t border-neutral-800 flex justify-between items-center">
                    <span class="text-sm text-neutral-400">Conclua a simulação para destravar o progresso.</span>
                    <button id="btn-next-m2" disabled class="bg-neutral-850 text-neutral-600 border border-neutral-800 font-bold px-5 py-2.5 rounded-xl flex items-center gap-2 cursor-not-allowed transition">
                        <span>Complete a Simulação</span>
                        <i class="fas fa-lock"></i>
                    </button>
                </div>
            </section>

            <!-- TAB: MÓDULO 3: SUPERAMPBOT (PEDIDO DE FERRAMENTAS) -->
            <section id="tab-modulo3" class="tab-content hidden space-y-6">
                <div class="border-b border-neutral-800 pb-5">
                    <span class="text-xs uppercase tracking-wider font-extrabold text-red-500 bg-red-950/40 border border-red-500/20 px-2.5 py-1 rounded-md">Módulo 3</span>
                    <h2 class="text-2xl font-extrabold text-white mt-2">Bot Pedido de Ferramentas (@SuperAmpbot)</h2>
                    <p class="text-slate-500 mt-1">O pedido de insumos de trabalho e ferramentas deve seguir o fluxo digital centralizado do <strong>SuperAmpbot</strong>. Isso garante organização do estoque central e rastreamento de entregas.</p>
                </div>

                <div class="grid grid-cols-1 lg:grid-cols-12 gap-8">
                    <!-- Instruções e Sequência de Coleta -->
                    <div class="lg:col-span-5 space-y-4 text-sm text-neutral-300">
                        <h3 class="font-bold text-white text-base">Como Funciona a Requisição?</h3>
                        <p class="leading-relaxed text-neutral-400">O bot funciona coletando informações estruturadas passo a passo de acordo com o fluxo oficial:</p>
                        
                        <div class="space-y-2">
                            <div class="flex items-start gap-3 bg-neutral-950 p-2.5 rounded-lg border border-neutral-800">
                                <span class="bg-red-950 text-red-400 border border-red-800/30 font-bold text-xs h-5 w-5 rounded-full flex items-center justify-center shrink-0">1</span>
                                <p class="text-xs text-neutral-400">Nome completo e a cidade onde atua.</p>
                            </div>
                            <div class="flex items-start gap-3 bg-neutral-950 p-2.5 rounded-lg border border-neutral-800">
                                <span class="bg-red-950 text-red-400 border border-red-800/30 font-bold text-xs h-5 w-5 rounded-full flex items-center justify-center shrink-0">2</span>
                                <p class="text-xs text-neutral-400">Seleção de sua regional de atuação.</p>
                            </div>
                            <div class="flex items-start gap-3 bg-neutral-950 p-2.5 rounded-lg border border-neutral-800">
                                <span class="bg-red-950 text-red-400 border border-red-800/30 font-bold text-xs h-5 w-5 rounded-full flex items-center justify-center shrink-0">3</span>
                                <p class="text-xs text-neutral-400">Descrição dos itens e ferramentas desejados.</p>
                            </div>
                            <div class="flex items-start gap-3 bg-neutral-950 p-2.5 rounded-lg border border-neutral-800">
                                <span class="bg-red-950 text-red-400 border border-red-800/30 font-bold text-xs h-5 w-5 rounded-full flex items-center justify-center shrink-0">4</span>
                                <p class="text-xs text-neutral-400">Quantidade total de cada item solicitado.</p>
                            </div>
                            <div class="flex items-start gap-3 bg-neutral-950 p-2.5 rounded-lg border border-neutral-800">
                                <span class="bg-red-950 text-red-400 border border-red-800/30 font-bold text-xs h-5 w-5 rounded-full flex items-center justify-center shrink-0">5</span>
                                <p class="text-xs text-neutral-400">Motivo detalhado do pedido (ex: desgaste natural).</p>
                            </div>
                            <div class="flex items-start gap-3 bg-neutral-950 p-2.5 rounded-lg border border-neutral-800">
                                <span class="bg-red-950 text-red-400 border border-red-800/30 font-bold text-xs h-5 w-5 rounded-full flex items-center justify-center shrink-0">6</span>
                                <p class="text-xs text-neutral-400">Confirmação final com <strong>sim</strong> ou <strong>não</strong>.</p>
                            </div>
                        </div>
                    </div>

                    <!-- Simulador Interativo Telegram SuperAmpbot -->
                    <div class="lg:col-span-7 flex flex-col">
                        <div class="bg-neutral-950 p-4 rounded-3xl border border-neutral-800">
                            <div class="bg-[#182533] text-white rounded-2xl shadow-xl overflow-hidden max-w-sm mx-auto flex flex-col h-[520px]">
                                <!-- Header Telegram -->
                                <div class="bg-[#202b36] p-3 flex items-center justify-between border-b border-[#141d26]">
                                    <div class="flex items-center gap-3">
                                        <!-- Logo do Telegram na imagem de contato -->
                                        <div class="h-9 w-9 rounded-full bg-[#5288c1] flex items-center justify-center text-white shrink-0 shadow-inner">
                                            <svg class="h-5 w-5 fill-current" viewBox="0 0 24 24">
                                                <path d="M12 .5C5.37.5 0 5.87 0 12.5S5.37 24.5 12 24.5 24 19.13 24 12.5 18.63.5 12 .5zm5.56 8.18l-1.89 8.9c-.14.63-.52.79-1.05.49l-2.88-2.12-1.39 1.34c-.15.15-.28.28-.58.28l.21-2.94 5.35-4.83c.23-.21-.05-.32-.36-.12L9.36 13.5l-2.85-.89c-.62-.19-.63-.62.13-.92l11.13-4.29c.52-.19.97.12.79.78z"/>
                                            </svg>
                                        </div>
                                        <div>
                                            <h4 class="text-xs font-bold leading-none text-white">SuperAmpbot</h4>
                                            <span class="text-[9px] text-red-400">pedido de ferramentas</span>
                                        </div>
                                    </div>
                                    <div class="flex gap-3 text-slate-400 text-xs">
                                        <i class="fas fa-search"></i>
                                        <i class="fas fa-ellipsis-v"></i>
                                    </div>
                                </div>

                                <!-- Mensagens Chat -->
                                <div id="m3-chat-area" class="flex-1 p-3 overflow-y-auto space-y-3 chat-scrollbar bg-[#0e1621] text-xs">
                                    <div class="text-center my-2 text-slate-500 text-[10px]">Hoje</div>
                                    <div class="text-center my-1 bg-[#182533] text-slate-300 inline-block px-3 py-1.5 rounded-md mx-auto max-w-[85%] text-[10px] leading-relaxed">
                                        Clique no botão abaixo para começar a estruturar sua solicitação.
                                    </div>
                                </div>

                                <!-- Input e Controle Interativo de Simulação -->
                                <div class="p-3 bg-[#17212b] border-t border-[#101921] flex flex-col gap-2">
                                    <!-- Dynamic Action buttons for step guidance -->
                                    <div id="m3-actions-container" class="flex flex-wrap gap-1.5 justify-center py-1">
                                        <button onclick="m3StartFlow()" id="btn-m3-start" class="bg-red-600 hover:bg-red-500 text-white px-4 py-1.5 rounded-full font-bold text-[10px] tracking-wide transition shadow-md shadow-red-900/20">
                                            Iniciar Solicitação
                                        </button>
                                    </div>
                                    <!-- Text input for typing simulations -->
                                    <div class="flex items-center gap-2 bg-[#24303f] px-3 py-2 rounded-xl text-slate-400">
                                        <input type="text" id="m3-text-input" disabled class="flex-1 bg-transparent border-none outline-none text-white text-[11px] placeholder-slate-500" placeholder="Aguardando ação...">
                                        <button onclick="m3SubmitText()" id="btn-m3-send" disabled class="text-slate-500 hover:text-red-400 transition">
                                            <i class="far fa-paper-plane"></i>
                                        </button>
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>

                <div class="pt-6 border-t border-neutral-800 flex justify-between items-center">
                    <span class="text-sm text-neutral-400">Conclua o pedido de ferramenta simulado para avançar.</span>
                    <button id="btn-next-m3" disabled class="bg-neutral-850 text-neutral-600 border border-neutral-800 font-bold px-5 py-2.5 rounded-xl flex items-center gap-2 cursor-not-allowed transition">
                        <span>Complete a Simulação</span>
                        <i class="fas fa-lock"></i>
                    </button>
                </div>
            </section>

            <!-- TAB: MÓDULO 4: CST & INDICAÇÕES -->
            <section id="tab-modulo4" class="tab-content hidden space-y-6">
                <div class="border-b border-neutral-800 pb-5">
                    <span class="text-xs uppercase tracking-wider font-extrabold text-red-500 bg-red-950/40 border border-red-500/20 px-2.5 py-1 rounded-md">Módulo 4</span>
                    <h2 class="text-2xl font-extrabold text-white mt-2">CST Sinal Degradado & Grupo de Indicações</h2>
                    <p class="text-neutral-400 mt-1">Procedimentos cruciais de integridade técnica da rede de telecomunicação e incentivos ao crescimento de nossa rede comercial.</p>
                </div>

                <div class="grid grid-cols-1 md:grid-cols-2 gap-8">
                    <!-- Painel CST -->
                    <div class="bg-neutral-950 border border-neutral-800 rounded-2xl p-6 space-y-4">
                        <div class="flex items-center gap-3">
                            <div class="h-10 w-10 rounded-xl bg-red-950 border border-red-900/30 text-red-500 flex items-center justify-center text-lg">
                                <i class="fas fa-signal-cross"></i>
                            </div>
                            <h3 class="font-bold text-white text-base">CST - Sinal Degradado</h3>
                        </div>
                        <p class="text-xs text-neutral-400 leading-relaxed">
                            A degradação de sinal compromete diretamente a experiência de navegação do cliente e pode gerar quedas massivas. Ao identificar um sinal fora dos limites toleráveis:
                        </p>
                        <div class="bg-neutral-900 p-3.5 rounded-xl border border-neutral-800 text-xs text-neutral-300 space-y-2 font-medium">
                            <p class="text-neutral-400 text-[10px] uppercase font-bold text-red-400">Fluxo de Acionamento (Pág. 2):</p>
                            <div class="flex items-center gap-2">
                                <i class="fab fa-telegram text-sky-400"></i>
                                <span>Acessar o <strong>@amper_opa_bot</strong> no Telegram</span>
                            </div>
                            <div class="flex items-center gap-2">
                                <i class="fas fa-route text-red-500"></i>
                                <span>Selecionar a opção de <strong>CST/Atendimento de Sinal</strong></span>
                            </div>
                            <div class="flex items-center gap-2">
                                <i class="fas fa-file-invoice text-red-400"></i>
                                <span>Reportar os dados de fibra, CTO ou cliente afetado</span>
                            </div>
                        </div>
                    </div>

                    <!-- Painel Indicações -->
                    <div class="bg-neutral-950 border border-neutral-800 rounded-2xl p-6 space-y-4">
                        <div class="flex items-center gap-3">
                            <div class="h-10 w-10 rounded-xl bg-red-950 border border-red-900/30 text-red-500 flex items-center justify-center text-lg">
                                <i class="fas fa-users"></i>
                            </div>
                            <h3 class="font-bold text-white text-base">Grupo de Indicações Comerciais</h3>
                        </div>
                        <p class="text-xs text-neutral-400 leading-relaxed">
                            Crescemos em equipe! Sempre que você estiver em campo ou interagir com um potencial novo cliente interessado nos serviços de internet de alta velocidade da Ampernet:
                        </p>
                        <div class="bg-neutral-900 p-3.5 rounded-xl border border-neutral-800 text-xs text-neutral-300 space-y-2 font-medium">
                            <p class="text-neutral-400 text-[10px] uppercase font-bold text-red-400">Como Enviar?</p>
                            <div class="flex items-center gap-2">
                                <i class="fab fa-whatsapp text-emerald-400"></i>
                                <span>Acesse o <strong>Grupo de Indicações</strong> no WhatsApp</span>
                            </div>
                            <div class="flex items-center gap-2">
                                <i class="fas fa-map-marker-alt text-red-500"></i>
                                <span>Envie o Endereço com viabilidade técnica</span>
                            </div>
                            <div class="flex items-center gap-2">
                                <i class="fas fa-user-tag text-purple-400"></i>
                                <span>Nome e Contato do cliente para o comercial atuar</span>
                            </div>
                        </div>
                    </div>
                </div>

                <div class="pt-6 border-t border-neutral-800 flex justify-between items-center">
                    <span class="text-sm text-neutral-400">Estude os fluxos operacionais para liberar o Quiz de Avaliação.</span>
                    <button onclick="completarModulo4()" class="bg-red-600 hover:bg-red-700 text-white font-bold px-5 py-2.5 rounded-xl flex items-center gap-2 transition shadow-[0_0_12px_rgba(239,68,68,0.3)]">
                        <span>Concluir & Desbloquear Avaliação</span>
                        <i class="fas fa-unlock"></i>
                    </button>
                </div>
            </section>

            <!-- TAB: AVALIAÇÃO FINAL (QUIZ & CERTIFICADO) -->
            <section id="tab-quiz" class="tab-content hidden space-y-6">
                <!-- Tela Trancada -->
                <div id="quiz-locked" class="text-center py-12 space-y-4">
                    <div class="h-20 w-20 bg-neutral-950 text-neutral-600 rounded-full flex items-center justify-center text-3xl mx-auto border border-dashed border-neutral-800">
                        <i class="fas fa-lock"></i>
                    </div>
                    <div class="max-w-md mx-auto">
                        <h3 class="font-extrabold text-white text-xl">Avaliação Trancada</h3>
                        <p class="text-sm text-neutral-400 mt-2">Você precisa concluir todos os 4 módulos do portal de treinamento de comunicação para habilitar o teste de certificação.</p>
                    </div>
                </div>

                <!-- Tela Ativa do Quiz -->
                <div id="quiz-active" class="hidden space-y-6">
                    <div class="border-b border-neutral-800 pb-5">
                        <span class="text-xs uppercase tracking-wider font-extrabold text-red-500 bg-red-950/40 border border-red-500/20 px-2.5 py-1 rounded-md">Avaliação Final</span>
                        <h2 class="text-2xl font-extrabold text-white mt-2">Prova de Proficiência e Fluxos</h2>
                        <p class="text-neutral-400 mt-1">Responda às questões com atenção. Para ser aprovado e gerar o seu certificado, você deve acertar pelo menos <strong>4 das 5 perguntas</strong> (80% de aproveitamento).</p>
                    </div>

                    <!-- Corpo das Perguntas -->
                    <div id="quiz-questions-container" class="space-y-6">
                        <!-- Gerado via Javascript -->
                    </div>

                    <!-- Ação de Envio -->
                    <div class="pt-6 border-t border-neutral-800 flex justify-between items-center">
                        <span id="quiz-alert" class="text-xs font-semibold text-red-500 hidden">Por favor, responda a todas as questões antes de enviar.</span>
                        <div class="flex gap-3 ml-auto">
                            <button onclick="resetarQuiz()" class="px-5 py-2.5 rounded-xl border border-neutral-800 hover:bg-neutral-800 text-neutral-300 font-bold text-sm transition">Refazer Respostas</button>
                            <button onclick="corrigirQuiz()" class="bg-red-600 hover:bg-red-700 text-white font-bold px-6 py-2.5 rounded-xl text-sm transition flex items-center gap-2 shadow-[0_0_12px_rgba(239,68,68,0.3)]">
                                <span>Enviar Avaliação</span>
                                <i class="fas fa-paper-plane"></i>
                            </button>
                        </div>
                    </div>
                </div>

                <!-- Tela de Resultados do Quiz -->
                <div id="quiz-results" class="hidden text-center py-8 space-y-6 max-w-2xl mx-auto">
                    <div id="result-icon-container" class="h-20 w-20 rounded-full flex items-center justify-center text-4xl mx-auto shadow-md">
                        <!-- Icon dynamic -->
                    </div>
                    <div>
                        <h3 id="result-title" class="font-extrabold text-white text-2xl">Processando Resultados...</h3>
                        <p id="result-subtitle" class="text-sm text-neutral-400 mt-2 leading-relaxed">Carregando seus resultados...</p>
                    </div>

                    <!-- Card Estatístico de Aproveitamento -->
                    <div class="grid grid-cols-2 gap-4 border border-neutral-800 p-5 rounded-2xl bg-neutral-950/40">
                        <div>
                            <span class="block text-xs uppercase tracking-wider text-neutral-500 font-bold">Acertos</span>
                            <span id="result-score-text" class="text-2xl font-extrabold text-white">0 / 5</span>
                        </div>
                        <div>
                            <span class="block text-xs uppercase tracking-wider text-neutral-500 font-bold">Status Final</span>
                            <span id="result-status-text" class="text-lg font-bold">---</span>
                        </div>
                    </div>

                    <!-- Opções de Re-tentativa ou Emissão de Certificado -->
                    <div class="flex justify-center gap-4">
                        <button id="btn-quiz-retry" onclick="reiniciarProva()" class="hidden px-5 py-3 rounded-xl border border-neutral-800 hover:bg-neutral-800 text-neutral-300 font-bold text-sm transition">
                            Tentar Novamente
                        </button>
                        <button id="btn-generate-cert" onclick="abrirCertificado()" class="hidden bg-emerald-600 hover:bg-emerald-700 text-white font-bold px-6 py-3 rounded-xl text-sm shadow-md transition flex items-center gap-2">
                            <i class="fas fa-file-pdf"></i>
                            <span>Emitir Certificado Ampernet</span>
                        </button>
                    </div>
                </div>
            </section>
        </main>
    </div>

    <!-- TELA DO CERTIFICADO (EMISSOR MODAL / PÁGINA IMPRIMÍVEL) -->
    <div id="cert-modal" class="fixed inset-0 bg-neutral-950/90 backdrop-blur-sm z-50 flex items-center justify-center p-4 hidden">
        <div class="bg-neutral-900 rounded-3xl shadow-2xl max-w-4xl w-full overflow-hidden border border-neutral-800 flex flex-col max-h-[90vh]">
            <!-- Header Modal -->
            <div class="bg-neutral-950 px-6 py-4 border-b border-neutral-800 flex justify-between items-center shrink-0">
                <span class="font-bold text-white flex items-center gap-2 text-sm">
                    <i class="fas fa-award text-red-500"></i> Certificado de Capacitação Ampernet
                </span>
                <div class="flex gap-2">
                    <button onclick="window.print()" class="bg-red-600 hover:bg-red-700 text-white px-3 py-1.5 rounded-lg text-xs font-bold transition flex items-center gap-1.5">
                        <i class="fas fa-print"></i> Imprimir / Salvar PDF
                    </button>
                    <button onclick="fecharCertificado()" class="bg-neutral-800 hover:bg-neutral-700 text-neutral-300 px-3 py-1.5 rounded-lg text-xs font-bold transition border border-neutral-700">
                        Fechar
                    </button>
                </div>
            </div>

            <!-- Corpo de Impressão do Certificado -->
            <div class="p-8 sm:p-12 overflow-y-auto flex-1 bg-neutral-950 flex items-center justify-center">
                <!-- Certificado Design -->
                <div id="print-area" class="w-full max-w-3xl aspect-[1.414/1] border-[16px] border-double border-red-700 p-8 sm:p-12 relative bg-white text-neutral-950 flex flex-col justify-between shadow-inner select-none">
                    <!-- Cantos ornamentados -->
                    <div class="absolute top-4 left-4 text-red-700 text-xl font-serif">◆</div>
                    <div class="absolute top-4 right-4 text-red-700 text-xl font-serif">◆</div>
                    <div class="absolute bottom-4 left-4 text-red-700 text-xl font-serif">◆</div>
                    <div class="absolute bottom-4 right-4 text-red-700 text-xl font-serif">◆</div>

                    <!-- Cabeçalho do Certificado -->
                    <div class="text-center space-y-2">
                        <!-- Imagem do Logo no topo do certificado -->
                        <img src="image_bdffa5.png" alt="Ampernet Telecom" class="h-12 w-12 object-contain mx-auto">
                        <h1 class="text-red-700 font-black tracking-widest text-xl sm:text-2xl uppercase">Ampernet Telecom</h1>
                        <p class="text-[10px] sm:text-xs text-red-600 tracking-widest uppercase font-bold">Certificado de Capacitação Técnica</p>
                        <div class="w-24 h-[2px] bg-red-700 mx-auto mt-2"></div>
                    </div>

                    <!-- Conteúdo Central -->
                    <div class="text-center space-y-4 my-6">
                        <p class="text-xs sm:text-sm text-neutral-500 italic">Certificamos para os devidos fins que o colaborador</p>
                        <div class="relative inline-block w-full">
                            <!-- Input para o aluno ver o nome preenchido. O nome foi vinculado no início da sessão do treinamento -->
                            <input type="text" id="cert-student-name" readonly placeholder="[NOME DO TÉCNICO]" class="text-center text-lg sm:text-2xl font-black text-neutral-900 border-b-2 border-red-250 outline-none focus:border-red-600 px-4 py-1 w-full bg-transparent min-w-[300px] pointer-events-none">
                        </div>
                        <p class="text-xs text-neutral-600 max-w-lg mx-auto leading-relaxed">
                            concluiu com êxito o programa de treinamento e proficiência sobre <strong>Comunicação de Setores e Requisição de Ferramentas</strong>, compreendendo o uso dos bots corporativos <span class="font-semibold text-red-700">@amper_opa_bot</span> e <span class="font-semibold text-red-700">@SuperAmpbot</span>.
                        </p>
                    </div>

                    <!-- Rodapé com assinaturas fictícias e data -->
                    <div class="flex justify-between items-end border-t border-red-100 pt-6 text-[10px] text-neutral-500">
                        <div class="text-center">
                            <span class="block font-bold text-neutral-700">Setor de Suporte e Serviços</span>
                            <span>Ampernet Telecom</span>
                        </div>
                        <div class="text-center">
                            <span class="block font-bold text-neutral-700">Data de Conclusão</span>
                            <span id="cert-date">--/--/----</span>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <!-- NOTIFICAÇÃO POPUP CUSTOMIZADO (SUBSTITUIÇÃO DE ALERT) -->
    <div id="toast-container" class="fixed bottom-6 right-6 z-50 flex flex-col gap-2 max-w-xs w-full"></div>

    <!-- CONTROLES JAVASCRIPT DOS SIMULADORES, PROGRESSOS E QUIZ -->
    <script>
        // ESTADO GLOBAL DA APLICAÇÃO
        let userXP = 0;
        let technicianName = ''; // Variável armazenando o nome do técnico
        let moduleStatus = {
            m1: false, // Canais & Links
            m2: false, // Ampernet Interno
            m3: false, // SuperAmpbot
            m4: false  // CST
        };
        let quizStatus = false;

        // ESTADOS DE SIMULADORES
        let m2CurrentStep = 0; // 0: start, 1: select sector, 2: select service, 3: describe subject, 4: select city, 5: finished
        let m2SelectedSector = null;
        let m2SelectedService = null;

        let m3CurrentStep = 0; // 0: start, 1: name/city, 2: regional, 3: item, 4: qty, 5: reason, 6: confirm

        // Dados do Quiz Final (5 perguntas sobre os temas abordados)
        const quizData = [
            {
                id: 1,
                question: "1. Onde estão localizados os links cruciais que direcionam para o Telegram (Atendimento Geral, Pedidos de Ferramentas e CST)?",
                options: [
                    "A) No site público externo da Ampernet.",
                    "B) Na descrição do grupo de WhatsApp 'INFORMATIVO SUP E SERVIÇO'.",
                    "C) Enviados mensalmente no contracheque do colaborador.",
                    "D) Fixados exclusivamente no mural físico da central em Ampére."
                ],
                correct: 1 // index B
            },
            {
                id: 2,
                question: "2. Qual comando deve ser enviado ao bot '@amper_opa_bot' para iniciar o fluxo e gerar o Protocolo de Atendimento?",
                options: [
                    "A) /ajuda",
                    "B) /menu",
                    "C) /start",
                    "D) /solicitacao"
                ],
                correct: 2 // index C
            },
            {
                id: 3,
                question: "3. No Ampernet Interno Bot, qual a opção correta para acionar o setor de 'Suporte e Serviços' no primeiro nível de atendimento?",
                options: [
                    "A) Opção 2 - Suprimentos",
                    "B) Opção 4 - Comercial",
                    "C) Opção 5 - Suporte e Serviços",
                    "D) Opção 8 - NOC"
                ],
                correct: 2 // index C
            },
            {
                id: 4,
                question: "4. No bot '@SuperAmpbot', quais dados estruturados são coletados do colaborador para realizar o pedido de ferramentas?",
                options: [
                    "A) CPF, RG, CNH, Tipo sanguíneo e Telefone de emergência.",
                    "B) Nome e cidade, regional de atuação, descrição do pedido, quantidade, motivo e confirmação.",
                    "C) Código da Ordem de Serviço, Foto do poste geolocalizada e Modelo da ONU.",
                    "D) Apenas o nome completo do técnico, sem necessidade de justificativa de uso."
                ],
                correct: 1 // index B
            },
            {
                id: 5,
                question: "5. O que deve ser evitado no envio de chamados técnicos para agilizar o atendimento, de acordo com as instruções do bot?",
                options: [
                    "A) Digitar o texto com descrição detalhada.",
                    "B) Enviar mensagens de texto curtas e objetivas.",
                    "C) O envio excessivo de fotos e áudios que atrasem o processamento.",
                    "D) Indicar o nome completo do cliente afetado."
                ],
                correct: 2 // index C
            }
        ];

        // Função de envio de identificação inicial
        function submitTechnicianName() {
            const inputName = document.getElementById('tech-name-input');
            const nameValue = inputName.value.trim();
            const errorElement = document.getElementById('name-error');

            if (nameValue.length < 5) {
                errorElement.classList.remove('hidden');
                return;
            }

            errorElement.classList.add('hidden');
            technicianName = nameValue;

            // Insere o nome no certificado imediatamente para segurança
            document.getElementById('cert-student-name').value = technicianName;

            // Remove a tela de entrada com transição suave
            const modal = document.getElementById('name-entry-modal');
            modal.classList.add('opacity-0', 'pointer-events-none');
            setTimeout(() => {
                modal.remove();
            }, 300);

            // Adiciona pontos de identificação inicial e inicia o portal
            addXP(100, "Identificação realizada com sucesso!");
            showToast(`Bem-vindo, Técnico ${technicianName}!`, "success");
        }

        // Atualizar interface de progresso
        function updateProgress() {
            let completedCount = 0;
            if(moduleStatus.m1) completedCount++;
            if(moduleStatus.m2) completedCount++;
            if(moduleStatus.m3) completedCount++;
            if(moduleStatus.m4) completedCount++;

            let percent = Math.round((completedCount / 4) * 100);
            document.getElementById('progress-bar').style.width = percent + '%';
            document.getElementById('progress-text').innerText = percent + '%';

            // Atualização de Badges Laterais
            updateBadge('badge-m1', moduleStatus.m1);
            updateBadge('badge-m2', moduleStatus.m2);
            updateBadge('badge-m3', moduleStatus.m3);
            updateBadge('badge-m4', moduleStatus.m4);

            // Atualização de Status Cards no Painel
            updateStatusCard('status-card-m1', moduleStatus.m1);
            updateStatusCard('status-card-m2', moduleStatus.m2);
            updateStatusCard('status-card-m3', moduleStatus.m3);
            updateStatusCard('status-card-m4', moduleStatus.m4);

            // Liberar avaliação final caso todos estejam completos
            const btnQuiz = document.getElementById('btn-tab-quiz');
            const badgeQuiz = document.getElementById('badge-quiz');
            if (completedCount === 4) {
                btnQuiz.classList.remove('text-neutral-500', 'cursor-not-allowed');
                btnQuiz.classList.add('text-red-400', 'font-bold');
                badgeQuiz.innerText = "Liberado";
                badgeQuiz.classList.remove('bg-neutral-900', 'text-neutral-600', 'border-neutral-800');
                badgeQuiz.classList.add('bg-red-950/40', 'text-red-400', 'border-red-500/20', 'font-semibold');
                
                document.getElementById('quiz-locked').classList.add('hidden');
                document.getElementById('quiz-active').classList.remove('hidden');
            }
        }

        function updateBadge(id, completed) {
            const badge = document.getElementById(id);
            if(completed) {
                badge.innerText = "Concluído";
                badge.classList.remove('bg-neutral-850', 'text-neutral-400');
                badge.classList.add('bg-red-950/40', 'text-red-400', 'border', 'border-red-500/20', 'font-semibold');
            } else {
                badge.innerText = "Pendente";
                badge.classList.remove('bg-red-950/40', 'text-red-400', 'border', 'border-red-500/20');
                badge.classList.add('bg-neutral-850', 'text-neutral-400');
            }
        }

        function updateStatusCard(id, completed) {
            const el = document.getElementById(id);
            if(completed) {
                el.innerText = "Concluído";
                el.classList.remove('text-red-500', 'border-red-500/10');
                el.classList.add('bg-red-950/30', 'text-red-400', 'border-red-500/20');
            }
        }

        function addXP(amount, reason) {
            userXP += amount;
            document.getElementById('user-points').innerHTML = `<i class="fas fa-fire mr-1"></i> ${userXP} XP`;
            showToast(`+${amount} XP: ${reason}`, 'success');
        }

        // Sistema de Toasts
        function showToast(message, type = 'info') {
            const container = document.getElementById('toast-container');
            const toast = document.createElement('div');
            toast.className = `p-4 rounded-xl shadow-lg text-xs font-semibold text-white flex items-center gap-3 transform transition duration-300 translate-y-2 opacity-0 border border-neutral-800`;
            
            if (type === 'success') {
                toast.classList.add('bg-red-950', 'text-red-400', 'border-red-500/30');
                toast.innerHTML = `<i class="fas fa-check-circle text-lg text-red-500"></i> <span>${message}</span>`;
            } else if (type === 'error') {
                toast.classList.add('bg-red-950', 'text-red-400', 'border-red-500/30');
                toast.innerHTML = `<i class="fas fa-times-circle text-lg text-red-500"></i> <span>${message}</span>`;
            } else {
                toast.classList.add('bg-neutral-900', 'text-neutral-300');
                toast.innerHTML = `<i class="fas fa-info-circle text-lg text-red-500"></i> <span>${message}</span>`;
            }

            container.appendChild(toast);
            
            setTimeout(() => {
                toast.classList.remove('translate-y-2', 'opacity-0');
            }, 50);

            setTimeout(() => {
                toast.classList.add('translate-y-2', 'opacity-0');
                setTimeout(() => {
                    toast.remove();
                }, 300);
            }, 3500);
        }

        function switchTab(tabId) {
            document.querySelectorAll('.tab-content').forEach(section => {
                section.classList.add('hidden');
                section.classList.remove('block');
            });
            document.getElementById(`tab-${tabId}`).classList.remove('hidden');
            document.getElementById(`tab-${tabId}`).classList.add('block');

            document.querySelectorAll('.tab-btn').forEach(btn => {
                btn.classList.remove('bg-red-600/10', 'text-red-500', 'border', 'border-red-500/20', 'shadow-sm');
                btn.classList.add('text-neutral-400', 'hover:bg-neutral-800');
            });
            const activeBtn = document.getElementById(`btn-tab-${tabId}`);
            if (activeBtn) {
                activeBtn.classList.remove('text-neutral-400', 'hover:bg-neutral-800');
                activeBtn.classList.add('bg-red-600/10', 'text-red-500', 'border', 'border-red-500/20', 'shadow-sm');
            }
        }

        // ==================== CONTROLES MÓDULO 1 ====================
        function completarModulo1() {
            if(!moduleStatus.m1) {
                moduleStatus.m1 = true;
                addXP(100, "Descrição de Canais Lida");
                updateProgress();
            }
            switchTab('modulo2');
        }

        // ==================== STREAMING_CHUNK: Implementing robust Telegram Módulo 2 step controllers... ====================
        // ==================== SIMULADOR MÓDULO 2 (AMPERNET INTERNO BOT) ====================
        function m2SendStart() {
            const chat = document.getElementById('m2-chat-area');
            const actions = document.getElementById('m2-actions-container');
            const input = document.getElementById('m2-text-input');
            const btnSend = document.getElementById('btn-m2-send');

            if (!chat || !actions || !input || !btnSend) return;

            actions.innerHTML = '';
            appendMessage(chat, 'user', '/start');
            input.placeholder = 'Digitando...';
            m2CurrentStep = 1;

            setTimeout(() => {
                appendMessage(chat, 'bot', 'Olá, Bem vindo à Ampernet Telecom, irei ajudar no seu atendimento.');
                setTimeout(() => {
                    const protocol = "AMP2026" + Math.floor(100000 + Math.random() * 900000);
                    appendMessage(chat, 'bot', `Seu protocolo de atendimento é <strong>${protocol}</strong>.<br><br>Selecione, por favor, o setor responsável:<br><br><strong>1</strong> - Financeiro<br><strong>2</strong> - Suprimentos<br><strong>3</strong> - Administrativo<br><strong>4</strong> - Comercial<br><strong>5</strong> - Suporte e Serviços<br><strong>6</strong> - Recursos Humanos<br><strong>7</strong> - Serviços e Tecnologia<br><strong>8</strong> - NOC`);
                    
                    // Ativa input e ações rápidas
                    input.disabled = false;
                    btnSend.disabled = false;
                    input.placeholder = 'Digite uma das opções (ex: 5)...';
                    input.focus();

                    actions.innerHTML = `
                        <button onclick="m2SelectSector(5, 'Suporte e Serviços')" class="bg-red-600 hover:bg-red-500 text-white px-3 py-1.5 rounded-xl font-bold text-[10px] transition shadow-md shadow-red-900/20">5 - Suporte e Serviços</button>
                        <button onclick="m2SelectSector(4, 'Comercial')" class="bg-red-600 hover:bg-red-500 text-white px-3 py-1.5 rounded-xl font-bold text-[10px] transition shadow-md shadow-red-900/20">4 - Comercial</button>
                    `;
                }, 1000);
            }, 800);
        }

        function m2SubmitText() {
            const input = document.getElementById('m2-text-input');
            const val = input.value.trim();
            if(!val) return;

            const chat = document.getElementById('m2-chat-area');
            appendMessage(chat, 'user', val);
            input.value = '';

            input.disabled = true;
            document.getElementById('btn-m2-send').disabled = true;

            setTimeout(() => {
                processM2Input(val);
            }, 800);
        }

        function processM2Input(val) {
            const chat = document.getElementById('m2-chat-area');
            const actions = document.getElementById('m2-actions-container');
            const input = document.getElementById('m2-text-input');
            const btnSend = document.getElementById('btn-m2-send');

            if (m2CurrentStep === 1) {
                // Seleção de Setores Inicial (Pág 3/5/6)
                if (val === '5') {
                    m2SelectSector(5, 'Suporte e Serviços');
                } else if (val === '4') {
                    m2SelectSector(4, 'Comercial');
                } else {
                    appendMessage(chat, 'bot', 'Opção inválida para esta simulação. Por favor, escolha <strong>4</strong> para Comercial ou <strong>5</strong> para Suporte e Serviços.');
                    input.disabled = false;
                    btnSend.disabled = false;
                    input.focus();
                }
            } else if (m2CurrentStep === 2) {
                // Seleção do Serviço dentro do setor
                if (m2SelectedSector === 5) {
                    if (val === '1') {
                        m2SelectService(1, 'Agendamento');
                    } else if (val === '2') {
                        m2SelectService(2, 'TAC');
                    } else {
                        appendMessage(chat, 'bot', 'Opção inválida. Selecione <strong>1</strong> (Agendamento) ou <strong>2</strong> (TAC).');
                        input.disabled = false;
                        btnSend.disabled = false;
                        input.focus();
                    }
                } else if (m2SelectedSector === 4) {
                    if (val === '1') {
                        m2SelectService(1, 'BackOffice');
                    } else if (val === '2') {
                        m2SelectService(2, 'Analista');
                    } else {
                        appendMessage(chat, 'bot', 'Opção inválida. Selecione <strong>1</strong> ou <strong>2</strong>.');
                        input.disabled = false;
                        btnSend.disabled = false;
                        input.focus();
                    }
                }
            } else if (m2CurrentStep === 3) {
                // Descrição do assunto pelo usuário
                appendMessage(chat, 'bot', 'Qual cidade deseja suporte?');
                
                // Opções rápidas de cidades para o usuário (Pág 5)
                actions.innerHTML = `
                    <div class="grid grid-cols-2 gap-2 w-full px-2">
                        <button onclick="m2SelectCity('1', 'Ampére')" class="bg-red-600 hover:bg-red-500 text-white py-1 px-2 rounded-xl font-bold text-[9px] transition">1 - Ampére</button>
                        <button onclick="m2SelectCity('13', 'Francisco Beltrão')" class="bg-red-600 hover:bg-red-500 text-white py-1 px-2 rounded-xl font-bold text-[9px] transition">13 - Francisco Beltrão</button>
                    </div>
                `;
                input.placeholder = 'Digite o número ou nome da cidade...';
                input.disabled = false;
                btnSend.disabled = false;
                input.focus();
                m2CurrentStep = 4;
            } else if (m2CurrentStep === 4) {
                // Seleção de cidade finalizada
                m2SelectCity('Personalizado', val);
            }
        }

        function m2SelectSector(number, name) {
            const chat = document.getElementById('m2-chat-area');
            const actions = document.getElementById('m2-actions-container');
            const input = document.getElementById('m2-text-input');
            const btnSend = document.getElementById('btn-m2-send');

            m2SelectedSector = number;
            actions.innerHTML = '';
            
            // Caso tenha clicado no botão rápido, adiciona a mensagem
            if (document.activeElement !== input) {
                appendMessage(chat, 'user', `${number}`);
            }

            input.placeholder = 'Processando...';

            setTimeout(() => {
                if (number === 5) {
                    // Fluxo Suporte e Serviços (Pág 5 e Pág 6)
                    appendMessage(chat, 'bot', `Bem Vindo ao Suporte e Serviços.<br><br>Escolha o serviço necessário:<br><strong>1</strong> - Agendamento<br><strong>2</strong> - TAC<br><strong>3</strong> - Erro de seleção<br><strong>4</strong> - Suporte Inmap<br><strong>5</strong> - STFC`);
                    
                    actions.innerHTML = `
                        <button onclick="m2SelectService(1, 'Agendamento')" class="bg-red-600 hover:bg-red-500 text-white px-3 py-1.5 rounded-xl font-bold text-[10px] transition shadow-md">1 - Agendamento</button>
                        <button onclick="m2SelectService(2, 'TAC')" class="bg-red-600 hover:bg-red-500 text-white px-3 py-1.5 rounded-xl font-bold text-[10px] transition shadow-md">2 - TAC</button>
                    `;
                    input.placeholder = 'Digite 1 ou 2...';
                } else if (number === 4) {
                    // Fluxo Comercial (Pág 8)
                    appendMessage(chat, 'bot', `Bem vindo ao Comercial!<br><br>Selecione o serviço necessário:<br><strong>1</strong> - BackOffice<br><strong>2</strong> - Analista<br><strong>3</strong> - Erro de Seleção`);
                    
                    actions.innerHTML = `
                        <button onclick="m2SelectService(1, 'BackOffice')" class="bg-red-600 hover:bg-red-500 text-white px-3 py-1.5 rounded-xl font-bold text-[10px] transition shadow-md">1 - BackOffice</button>
                        <button onclick="m2SelectService(2, 'Analista')" class="bg-red-600 hover:bg-red-500 text-white px-3 py-1.5 rounded-xl font-bold text-[10px] transition shadow-md">2 - Analista</button>
                    `;
                    input.placeholder = 'Digite 1 ou 2...';
                }
                
                input.disabled = false;
                btnSend.disabled = false;
                input.focus();
                m2CurrentStep = 2;
            }, 800);
        }

        function m2SelectService(number, name) {
            const chat = document.getElementById('m2-chat-area');
            const actions = document.getElementById('m2-actions-container');
            const input = document.getElementById('m2-text-input');
            const btnSend = document.getElementById('btn-m2-send');

            m2SelectedService = number;
            actions.innerHTML = '';

            if (document.activeElement !== input) {
                appendMessage(chat, 'user', `${number}`);
            }

            input.placeholder = 'Processando...';

            setTimeout(() => {
                if (m2SelectedSector === 5 && number === 1) {
                    // Agendamento (Pág 5)
                    appendMessage(chat, 'bot', 'Por favor, poderia descrever brevemente o assunto para que possamos direcionar seu atendimento com mais agilidade?');
                    input.placeholder = 'Digite o assunto do chamado técnico...';
                    input.disabled = false;
                    btnSend.disabled = false;
                    input.focus();
                    m2CurrentStep = 3;
                } else if (m2SelectedSector === 5 && number === 2) {
                    // TAC (Pág 6)
                    appendMessage(chat, 'bot', 'Para AGILIZAR seu atendimento, DESCREVA a sua solicitação:<br>⚠️ <strong>PEDIMOS QUE EVITEM ENVIAR FOTOS E ÁUDIOS NESTE CANAL!</strong>');
                    
                    actions.innerHTML = `
                        <button onclick="m2AutoFillTAC()" class="bg-red-950 text-red-400 border border-red-800/40 px-3 py-1.5 rounded-xl font-bold text-[10px] transition shadow-md">Preencher Modelo (Pág 6)</button>
                    `;
                    input.placeholder = 'Descreva a solicitação ou use o preenchimento automático...';
                    input.disabled = false;
                    btnSend.disabled = false;
                    input.focus();
                    m2CurrentStep = 3;
                } else if (m2SelectedSector === 4) {
                    // Comercial (Pág 8)
                    if (number === 1) {
                        appendMessage(chat, 'bot', '<strong>1 - BackOffice:</strong> Para ver login e senha de aplicativos de TV como HBO, Watch TVBR, solicitar Rede Mesh.');
                    } else {
                        appendMessage(chat, 'bot', '<strong>2 - Analista:</strong> Confirmar algo mais específico como contrato, plano e assinatura.');
                    }
                    concluirM2FluxoCompleto();
                }
            }, 800);
        }

        function m2AutoFillTAC() {
            const input = document.getElementById('m2-text-input');
            input.value = `Estou no cliente: Fulano Ciclano\nID: 123456\nMac: FHTT12345678\nEstá com lentidão, já fiz testes e não funcionou.`;
            input.focus();
        }

        function m2SelectCity(code, name) {
            const chat = document.getElementById('m2-chat-area');
            const actions = document.getElementById('m2-actions-container');
            const input = document.getElementById('m2-text-input');

            actions.innerHTML = '';
            appendMessage(chat, 'user', name);

            setTimeout(() => {
                appendMessage(chat, 'bot', `Cidade selecionada: <strong>${name}</strong>.<br>Sua solicitação de Agendamento foi direcionada com sucesso para a central responsável.`);
                concluirM2FluxoCompleto();
            }, 800);
        }

        function concluirM2FluxoCompleto() {
            const chat = document.getElementById('m2-chat-area');
            const btnNext = document.getElementById('btn-next-m2');
            const input = document.getElementById('m2-text-input');
            const btnSend = document.getElementById('btn-m2-send');

            input.disabled = true;
            btnSend.disabled = true;

            setTimeout(() => {
                appendMessage(chat, 'system', 'Simulação finalizada de forma rápida e direta!');
                input.placeholder = 'Fluxo Concluído.';
                
                btnNext.disabled = false;
                btnNext.classList.remove('bg-neutral-850', 'text-neutral-600', 'cursor-not-allowed');
                btnNext.classList.add('bg-red-600', 'hover:bg-red-700', 'text-white');
                btnNext.innerHTML = `<span>Ir para Módulo 3</span> <i class="fas fa-arrow-right"></i>`;
                btnNext.setAttribute('onclick', 'concluirModulo2()');

                if(!moduleStatus.m2) {
                    moduleStatus.m2 = true;
                    addXP(150, "Simulador de Triagem Concluído");
                    updateProgress();
                }
            }, 800);
        }

        function concluirModulo2() {
            switchTab('modulo3');
        }

        // ==================== STREAMING_CHUNK: Developing Módulo 3 SuperAmpbot multi-step flow engine... ====================
        // ==================== SIMULADOR MÓDULO 3 (SUPERAMPBOT) ====================
        function m3StartFlow() {
            const chat = document.getElementById('m3-chat-area');
            const actions = document.getElementById('m3-actions-container');
            const input = document.getElementById('m3-text-input');
            const btnSend = document.getElementById('btn-m3-send');

            actions.innerHTML = '';
            appendMessage(chat, 'user', 'Iniciar Pedido de Ferramentas');

            setTimeout(() => {
                appendMessage(chat, 'bot', 'Olá, bem-vindo! Qual é o seu nome completo e cidade (Colaborador)?');
                
                // Habilitar entrada de texto
                input.disabled = false;
                btnSend.disabled = false;
                
                // Pré-preenche o nome do técnico se ele já se identificou na entrada do portal
                if (technicianName) {
                    input.value = `${technicianName} - Ampére`;
                }
                
                input.placeholder = 'Digite seu Nome e Cidade (ex: Thiago - Ampére)...';
                input.focus();
                m3CurrentStep = 1;
            }, 800);
        }

        function m3SubmitText() {
            const input = document.getElementById('m3-text-input');
            const val = input.value.trim();
            if(!val) return;

            const chat = document.getElementById('m3-chat-area');
            appendMessage(chat, 'user', val);
            input.value = '';

            input.disabled = true;
            document.getElementById('btn-m3-send').disabled = true;

            setTimeout(() => {
                processM3Flow(val);
            }, 800);
        }

        function processM3Flow(inputVal) {
            const chat = document.getElementById('m3-chat-area');
            const actions = document.getElementById('m3-actions-container');
            const input = document.getElementById('m3-text-input');
            const btnSend = document.getElementById('btn-m3-send');

            if(m3CurrentStep === 1) {
                const parts = inputVal.split('-');
                m3Data.colaborador = parts[0]?.trim() || inputVal;
                m3Data.cidade = parts[1]?.trim() || "Ampére";

                appendMessage(chat, 'bot', 'Selecione a regional correspondente ao seu polo de atuação:');
                
                actions.innerHTML = `
                    <div class="grid grid-cols-2 gap-2 w-full px-2">
                        <button onclick="m3SelectRegional('Ampére')" class="bg-red-600 hover:bg-red-500 text-white py-1 px-2 rounded-xl font-bold text-[9px] transition">Ampére</button>
                        <button onclick="m3SelectRegional('Francisco Beltrão')" class="bg-red-600 hover:bg-red-500 text-white py-1 px-2 rounded-xl font-bold text-[9px] transition">Francisco Beltrão</button>
                        <button onclick="m3SelectRegional('Fazenda Rio Grande')" class="bg-red-600 hover:bg-red-500 text-white py-1 px-2 rounded-xl font-bold text-[9px] transition">Fazenda Rio Grande</button>
                        <button onclick="m3SelectRegional('Guaíra')" class="bg-red-600 hover:bg-red-500 text-white py-1 px-2 rounded-xl font-bold text-[9px] transition">Guaíra</button>
                        <button onclick="m3SelectRegional('Laranjeiras')" class="bg-red-600 hover:bg-red-500 text-white py-1 px-2 rounded-xl font-bold text-[9px] transition">Laranjeiras</button>
                        <button onclick="m3SelectRegional('Pato Branco')" class="bg-red-600 hover:bg-red-500 text-white py-1 px-2 rounded-xl font-bold text-[9px] transition">Pato Branco</button>
                        <button onclick="m3SelectRegional('Ponta Grossa')" class="bg-red-600 hover:bg-red-500 text-white py-1 px-2 rounded-xl font-bold text-[9px] transition">Ponta Grossa</button>
                        <button onclick="m3SelectRegional('São Lourenço')" class="bg-red-600 hover:bg-red-500 text-white py-1 px-2 rounded-xl font-bold text-[9px] transition">São Lourenço</button>
                    </div>
                `;
                input.placeholder = 'Selecione uma regional acima...';
            }
            else if(m3CurrentStep === 3) {
                m3Data.pedido = inputVal;
                appendMessage(chat, 'bot', 'Qual é a quantidade de cada item solicitado?');
                
                input.disabled = false;
                btnSend.disabled = false;
                input.placeholder = 'Digite a quantidade (ex: 01 par, 02 unidades)...';
                input.focus();
                m3CurrentStep = 4;
            }
            else if(m3CurrentStep === 4) {
                m3Data.quantidade = inputVal;
                appendMessage(chat, 'bot', 'Qual é o motivo do pedido de novas ferramentas?');
                
                input.disabled = false;
                btnSend.disabled = false;
                input.placeholder = 'Digite a justificativa detalhada do pedido...';
                input.focus();
                m3CurrentStep = 5;
            }
            else if(m3CurrentStep === 5) {
                m3Data.motivo = inputVal;
                
                appendMessage(chat, 'bot', `Confirme os dados do pedido de ferramentas:<br><br>
                <strong>Colaborador:</strong> ${m3Data.colaborador}<br>
                <strong>Cidade / Regional:</strong> ${m3Data.cidade}<br>
                <strong>Pedido:</strong> ${m3Data.pedido}<br>
                <strong>Quantidade:</strong> ${m3Data.quantidade}<br>
                <strong>Motivo:</strong> ${m3Data.motivo}<br><br>
                Digite '<strong>sim</strong>' para confirmar ou '<strong>não</strong>' para refazer.`);

                actions.innerHTML = `
                    <button onclick="m3Confirm(true)" class="bg-emerald-600 hover:bg-emerald-500 text-white px-4 py-1.5 rounded-xl font-bold text-[10px] transition mr-2 shadow-sm">Confirmar (Sim)</button>
                    <button onclick="m3Confirm(false)" class="bg-red-600 hover:bg-red-500 text-white px-4 py-1.5 rounded-xl font-bold text-[10px] transition shadow-sm">Refazer (Não)</button>
                `;
                input.placeholder = 'Confirme o pedido acima...';
            }
        }

        function m3SelectRegional(regional) {
            const chat = document.getElementById('m3-chat-area');
            const actions = document.getElementById('m3-actions-container');
            const input = document.getElementById('m3-text-input');
            const btnSend = document.getElementById('btn-m3-send');

            actions.innerHTML = '';
            appendMessage(chat, 'user', regional);
            m3Data.cidade = regional;

            setTimeout(() => {
                appendMessage(chat, 'bot', 'Qual é o seu pedido? (Descreva detalhadamente a ferramenta ou EPI)');
                
                input.disabled = false;
                btnSend.disabled = false;
                input.placeholder = 'Descreva a ferramenta (ex: 01 Alicate de Crimpagem)...';
                input.focus();
                m3CurrentStep = 3;
            }, 800);
        }

        function m3Confirm(yes) {
            const chat = document.getElementById('m3-chat-area');
            const actions = document.getElementById('m3-actions-container');
            const input = document.getElementById('m3-text-input');

            actions.innerHTML = '';
            appendMessage(chat, 'user', yes ? 'sim' : 'não');

            setTimeout(() => {
                if(yes) {
                    appendMessage(chat, 'bot', 'Pedido enviado com sucesso para o setor de suprimentos! Seu chamado de ferramentas foi gerado.');
                    
                    setTimeout(() => {
                        appendMessage(chat, 'system', 'Simulação de Pedido de Insumos finalizada!');
                        input.placeholder = 'Fluxo Finalizado.';
                        
                        const btnNext = document.getElementById('btn-next-m3');
                        btnNext.disabled = false;
                        btnNext.classList.remove('bg-neutral-850', 'text-neutral-600', 'cursor-not-allowed');
                        btnNext.classList.add('bg-red-600', 'hover:bg-red-700', 'text-white');
                        btnNext.innerHTML = `<span>Ir para Módulo 4</span> <i class="fas fa-arrow-right"></i>`;
                        btnNext.setAttribute('onclick', 'concluirModulo3()');

                        if(!moduleStatus.m3) {
                            moduleStatus.m3 = true;
                            addXP(150, "Requisição de Ferramenta Efetuada");
                            updateProgress();
                        }
                    }, 800);
                } else {
                    appendMessage(chat, 'bot', 'Pedido cancelado. Reiniciando o fluxo...');
                    setTimeout(() => {
                        m3StartFlow();
                    }, 1000);
                }
            }, 800);
        }

        function concluirModulo3() {
            switchTab('modulo4');
        }

        // ==================== CONTROLES MÓDULO 4 ====================
        function completarModulo4() {
            if(!moduleStatus.m4) {
                moduleStatus.m4 = true;
                addXP(100, "Fluxos de CST e Indicações Lidos");
                updateProgress();
            }
            switchTab('quiz');
        }

        // ==================== STREAMING_CHUNK: Generating final evaluation dynamic quiz blocks... ====================
        // ==================== SISTEMA DE QUIZ DE AVALIAÇÃO ====================
        function buildQuiz() {
            const container = document.getElementById('quiz-questions-container');
            container.innerHTML = '';

            quizData.forEach((q, qIndex) => {
                const qDiv = document.createElement('div');
                qDiv.className = "bg-neutral-950 p-5 rounded-2xl border border-neutral-800 space-y-3";
                
                qDiv.innerHTML = `
                    <h4 class="font-bold text-white text-sm">${q.question}</h4>
                    <div class="grid grid-cols-1 gap-2.5 mt-2">
                        ${q.options.map((opt, optIndex) => `
                            <label class="flex items-start gap-3 p-3 rounded-xl border border-neutral-800 hover:border-red-500 bg-neutral-900 cursor-pointer transition select-none">
                                <input type="radio" name="q-${q.id}" value="${optIndex}" class="mt-1 h-4 w-4 text-red-600 border-neutral-700 focus:ring-red-500 bg-neutral-950">
                                <span class="text-xs text-neutral-300 font-medium">${opt}</span>
                            </label>
                        `).join('')}
                    </div>
                `;
                container.appendChild(qDiv);
            });
        }

        function resetarQuiz() {
            buildQuiz();
            document.getElementById('quiz-alert').classList.add('hidden');
            showToast("Quiz reiniciado!", "info");
        }

        function corrigirQuiz() {
            const alert = document.getElementById('quiz-alert');
            let answeredCount = 0;
            let score = 0;

            quizData.forEach(q => {
                const selected = document.querySelector(`input[name="q-${q.id}"]:checked`);
                if(selected) {
                    answeredCount++;
                    if(parseInt(selected.value) === q.correct) {
                        score++;
                    }
                }
            });

            if (answeredCount < quizData.length) {
                alert.classList.remove('hidden');
                showToast("Por favor, responda a todas as perguntas!", "error");
                return;
            }

            alert.classList.add('hidden');

            document.getElementById('quiz-active').classList.add('hidden');
            document.getElementById('quiz-results').classList.remove('hidden');

            const iconContainer = document.getElementById('result-icon-container');
            const resTitle = document.getElementById('result-title');
            const resSubtitle = document.getElementById('result-subtitle');
            const scoreText = document.getElementById('result-score-text');
            const statusText = document.getElementById('result-status-text');
            const btnRetry = document.getElementById('btn-quiz-retry');
            const btnCert = document.getElementById('btn-generate-cert');

            scoreText.innerText = `${score} / 5`;

            if(score >= 4) {
                iconContainer.className = "h-20 w-20 rounded-full flex items-center justify-center text-4xl mx-auto shadow-md bg-red-950/50 border border-red-500/30 text-red-500";
                iconContainer.innerHTML = `<i class="fas fa-graduation-cap"></i>`;
                resTitle.innerText = "Parabéns! Você foi Aprovado!";
                resSubtitle.innerText = "Excelente aproveitamento operacional! Você domina todos os fluxos de canais de comunicação, abertura de chamados intersetoriais e requisição de ferramentas.";
                
                statusText.innerText = "APROVADO";
                statusText.className = "text-lg font-bold text-red-500";
                
                btnRetry.classList.add('hidden');
                btnCert.classList.remove('hidden');

                addXP(300, "Exame de Proficiência Aprovado");
            } else {
                iconContainer.className = "h-20 w-20 rounded-full flex items-center justify-center text-4xl mx-auto shadow-md bg-neutral-950 border border-neutral-800 text-neutral-500";
                iconContainer.innerHTML = `<i class="fas fa-times"></i>`;
                resTitle.innerText = "Tente Novamente";
                resSubtitle.innerText = "Infelizmente você não alcançou o aproveitamento mínimo de 80% (4 de 5 perguntas corretas) nesta tentativa. Revise os fluxos e tente novamente.";
                
                statusText.innerText = "REPROVADO";
                statusText.className = "text-lg font-bold text-neutral-500";
                
                btnRetry.classList.remove('hidden');
                btnCert.classList.add('hidden');

                showToast("Nota insuficiente para certificação. Necessário acertar pelo menos 4 perguntas.", "error");
            }
        }

        function reiniciarProva() {
            document.getElementById('quiz-results').classList.add('hidden');
            document.getElementById('quiz-active').classList.remove('hidden');
            resetarQuiz();
        }

        // ==================== GERENCIA CERTIFICADO E IMPRESSÃO ====================
        function abrirCertificado() {
            const hoje = new Date();
            const dia = String(hoje.getDate()).padStart(2, '0');
            const mes = String(hoje.getMonth() + 1).padStart(2, '0');
            const ano = hoje.getFullYear();
            document.getElementById('cert-date').innerText = `${dia}/${mes}/${ano}`;

            // Abre modal do Certificado
            document.getElementById('cert-modal').classList.remove('hidden');
        }

        function fecharCertificado() {
            document.getElementById('cert-modal').classList.add('hidden');
        }

        window.onload = function() {
            buildQuiz();
            updateProgress();

            // Adiciona listener para teclas físicos (Enter) nos inputs dos simuladores
            document.getElementById('m2-text-input').addEventListener('keypress', function(e) {
                if(e.key === 'Enter') {
                    m2SubmitText();
                }
            });

            document.getElementById('m3-text-input').addEventListener('keypress', function(e) {
                if(e.key === 'Enter') {
                    m3SubmitText();
                }
            });

            showToast("Portal de Capacitação Ampernet carregado!", "info");
        };
    </script>

    <!-- ESTILO ESPECIAL DE IMPRESSÃO DO CERTIFICADO -->
    <style>
        @media print {
            body * {
                visibility: hidden;
            }
            #cert-modal, #cert-modal * {
                visibility: visible;
            }
            #cert-modal {
                position: absolute;
                left: 0;
                top: 0;
                width: 100%;
                height: auto;
                background: white !important;
                backdrop-filter: none !important;
            }
            #cert-modal > div > div:first-child {
                display: none;
            }
            #print-area {
                border: 20px double #b91c1c !important;
                box-shadow: none !important;
                margin: 0 auto;
                width: 100%;
                max-width: 100% !important;
                background-color: white !important;
                color: black !important;
            }
            input#cert-student-name {
                border-bottom: none !important;
            }
        }
    </style>
</body>
</html>
