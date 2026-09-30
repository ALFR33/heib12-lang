<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>heib12 Sovereign Mail - Zero-Knowledge Encrypted Webmail</title>
    <!-- Tailwind CSS CDN -->
    <script src="https://cdn.jsdelivr.net/npm/@tailwindcss/browser@4"></script>
    <!-- Lucide Icons -->
    <script src="https://unpkg.com/lucide@latest"></script>
    <link href="https://fonts.googleapis.com/css2?family=Tajawal:wght@400;500;700;900&family=Fira+Code:wght@400;600&display=swap" rel="stylesheet">
    <style>
        body { font-family: 'Tajawal', sans-serif; -webkit-tap-highlight-color: transparent; }
        .font-mono { font-family: 'Fira Code', monospace; }
        .scrollbar-none::-webkit-scrollbar { display: none; }
        .scrollbar-none { -ms-overflow-style: none; scrollbar-width: none; }
    </style>
</head>
<body class="min-h-screen w-full bg-slate-950 text-slate-100 flex flex-col font-sans antialiased">

    <!-- Toast Notification -->
    <div id="toast-banner" class="fixed top-16 left-1/2 -translate-x-1/2 z-50 px-4 py-2 bg-cyan-400 text-slate-950 font-bold text-xs sm:text-sm rounded-full shadow-2xl shadow-cyan-500/50 border border-white/60 flex items-center gap-2 pointer-events-none transition-all duration-300 opacity-0 scale-95">
        <i data-lucide="sparkles" class="w-4 h-4"></i>
        <span id="toast-text">تمت العملية بنجاح</span>
    </div>

    <!-- Top Application Header -->
    <header class="border-b border-slate-800 bg-slate-900/95 backdrop-blur sticky top-0 z-40">
        <div class="max-w-7xl mx-auto px-4 h-16 flex items-center justify-between gap-4">
            <div class="flex items-center gap-3">
                <button type="button" onclick="toggleMobileSidebar()" class="lg:hidden p-2 rounded-xl bg-slate-800 text-slate-300 hover:text-white cursor-pointer">
                    <i data-lucide="menu" class="w-4 h-4"></i>
                </button>
                <div class="w-9 h-9 rounded-xl bg-gradient-to-br from-cyan-500 to-blue-600 flex items-center justify-center font-black text-slate-950 text-base shadow-lg shadow-cyan-500/25">
                    h12
                </div>
                <div>
                    <h1 class="font-bold text-base sm:text-lg text-cyan-400 leading-tight flex items-center gap-2">
                        <span>heib12 Sovereign Mail</span>
                        <span class="text-[10px] font-mono text-emerald-400 bg-emerald-500/10 px-2 py-0.5 rounded-full border border-emerald-500/30">Zero-Knowledge</span>
                    </h1>
                    <p class="text-[10px] text-slate-400 font-mono">Encrypted Webmail & Telemetry Dispatch</p>
                </div>
            </div>

            <!-- Navigation Mode Switcher -->
            <div class="flex items-center gap-1 bg-slate-950 p-1 rounded-2xl border border-slate-800 text-xs font-mono">
                <button type="button" onclick="switchViewMode('webmail')" id="nav-btn-webmail" class="px-3 py-1.5 rounded-xl font-bold transition-all flex items-center gap-1.5 bg-cyan-500 text-slate-950 shadow cursor-pointer">
                    <i data-lucide="mail" class="w-3.5 h-3.5"></i> <span>Webmail</span>
                </button>
                <button type="button" onclick="requestAdminView('users')" id="nav-btn-users" class="px-3 py-1.5 rounded-xl font-bold transition-all flex items-center gap-1.5 text-slate-400 hover:text-amber-400 cursor-pointer">
                    <i data-lucide="lock" class="w-3 h-3 text-amber-400"></i> <span id="users-tab-label">Users</span>
                </button>
                <button type="button" onclick="requestAdminView('monitor')" id="nav-btn-monitor" class="px-3 py-1.5 rounded-xl font-bold transition-all flex items-center gap-1.5 text-slate-400 hover:text-amber-400 cursor-pointer">
                    <i data-lucide="terminal" class="w-3 h-3 text-amber-400"></i> <span id="monitor-tab-label">Server Logs</span>
                </button>
            </div>

            <!-- User Account Capsule & Compose -->
            <div class="flex items-center gap-2">
                <div class="hidden sm:flex items-center bg-slate-950 rounded-xl border border-slate-800 p-0.5 font-mono text-xs">
                    <span class="px-3 py-1.5 text-cyan-300 font-bold" id="current-user-email">salh@heib12.org</span>
                    <button type="button" onclick="copyCurrentEmail()" class="p-1.5 hover:bg-slate-800 rounded-lg text-slate-400 hover:text-cyan-300 border-l border-slate-800 cursor-pointer" title="نسخ الإيميل">
                        <i data-lucide="copy" class="w-3.5 h-3.5"></i>
                    </button>
                </div>

                <button type="button" onclick="openCompose()" class="flex items-center gap-1.5 bg-cyan-500 hover:bg-cyan-400 text-slate-950 font-black px-4 py-2 rounded-xl text-xs sm:text-sm shadow-lg shadow-cyan-500/25 cursor-pointer active:scale-95">
                    <i data-lucide="plus" class="w-4 h-4"></i> <span>Compose</span>
                </button>
            </div>
        </div>
    </header>

    <!-- Main Workspace Container -->
    <div id="view-webmail" class="flex-1 max-w-7xl mx-auto w-full flex overflow-hidden">
        
        <!-- Left Sidebar Folders -->
        <aside id="mobile-sidebar" class="fixed lg:static inset-y-0 left-0 z-40 w-64 bg-slate-900 border-r border-slate-800 flex flex-col justify-between p-4 transform -translate-x-full lg:translate-x-0 transition-transform duration-300">
            <div class="space-y-4">
                <div class="flex lg:hidden justify-between items-center pb-2 border-b border-slate-800">
                    <span class="font-bold text-xs text-slate-400">Navigation</span>
                    <button type="button" onclick="toggleMobileSidebar()" class="text-slate-400 hover:text-white"><i data-lucide="x" class="w-4 h-4"></i></button>
                </div>

                <div class="space-y-1 font-mono text-xs" id="folders-nav-container">
                    <button type="button" onclick="switchFolder('inbox')" id="folder-inbox" class="w-full flex items-center justify-between px-3 py-2.5 rounded-xl bg-cyan-500 text-slate-950 font-bold shadow-md cursor-pointer">
                        <div class="flex items-center gap-2.5"><i data-lucide="inbox" class="w-4 h-4"></i> <span>Inbox</span></div>
                        <span class="text-[10px] px-2 py-0.5 rounded-full bg-slate-950 text-cyan-300 font-bold" id="badge-inbox">1</span>
                    </button>
                    <button type="button" onclick="switchFolder('sent')" id="folder-sent" class="w-full flex items-center justify-between px-3 py-2.5 rounded-xl text-slate-400 hover:bg-slate-800/60 cursor-pointer">
                        <div class="flex items-center gap-2.5"><i data-lucide="send" class="w-4 h-4"></i> <span>Sent Mail</span></div>
                    </button>
                    <button type="button" onclick="switchFolder('vault')" id="folder-vault" class="w-full flex items-center justify-between px-3 py-2.5 rounded-xl text-slate-400 hover:bg-slate-800/60 cursor-pointer">
                        <div class="flex items-center gap-2.5"><i data-lucide="lock" class="w-4 h-4"></i> <span>Quantum Vault</span></div>
                    </button>
                    <button type="button" onclick="switchFolder('telemetry')" id="folder-telemetry" class="w-full flex items-center justify-between px-3 py-2.5 rounded-xl text-slate-400 hover:bg-slate-800/60 cursor-pointer">
                        <div class="flex items-center gap-2.5"><i data-lucide="terminal" class="w-4 h-4"></i> <span>Industrial Telemetry</span></div>
                    </button>
                </div>
            </div>

            <!-- Infrastructure Health Widget -->
            <div class="bg-slate-950 p-3 rounded-2xl border border-slate-800 space-y-2 text-[11px] font-mono">
                <div class="flex items-center justify-between text-slate-400 font-bold border-b border-slate-800 pb-1">
                    <span class="flex items-center gap-1.5 text-cyan-400"><i data-lucide="server" class="w-3.5 h-3.5"></i> h12 Infrastructure</span>
                    <span class="text-emerald-400 text-[10px]">Active</span>
                </div>
                <div class="space-y-1 text-slate-400">
                    <div class="flex justify-between"><span>SMTP Submission:</span><span class="text-slate-200 font-bold">Port 587</span></div>
                    <div class="flex justify-between"><span>DKIM Signature:</span><span class="text-emerald-400 font-bold">Kyber-1024</span></div>
                </div>
            </div>
        </aside>

        <!-- Middle Pane: Email List -->
        <section id="pane-list" class="flex-1 lg:max-w-md w-full border-r border-slate-800 flex flex-col bg-slate-950 overflow-hidden">
            <div class="p-3 border-b border-slate-800 space-y-2 bg-slate-900/50">
                <div class="relative">
                    <i data-lucide="search" class="w-3.5 h-3.5 absolute left-3 top-3 text-slate-500"></i>
                    <input type="text" id="search-input" oninput="filterEmails()" placeholder="Search subject, sender, telemetry..." class="w-full bg-slate-950 pl-9 pr-3 py-2 rounded-xl border border-slate-800 text-xs text-cyan-300 focus:outline-none focus:border-cyan-500" />
                </div>
            </div>
            <div class="flex-1 overflow-y-auto divide-y divide-slate-800/80" id="emails-list-container"></div>
        </section>

        <!-- Right Pane: Email Reader -->
        <section id="pane-detail" class="hidden lg:flex flex-1 flex-col bg-slate-900 overflow-hidden">
            <div id="email-detail-container" class="flex-1 flex flex-col h-full overflow-hidden p-8 text-center text-slate-500 justify-center items-center">
                <i data-lucide="mail" class="w-8 h-8 text-slate-700 mb-2"></i>
                <p class="text-xs">Select an email to view full encrypted payload.</p>
            </div>
        </section>
    </div>

    <!-- View Mode 2: User Directory (Admin Only) -->
    <main id="view-users" class="flex-1 max-w-7xl mx-auto w-full p-4 sm:p-6 space-y-6 overflow-y-auto hidden">
        <div class="flex justify-between items-center border-b border-slate-800 pb-4">
            <div>
                <h2 class="text-xl font-black text-cyan-400">إدارة المستخدمين وصناديق البريد (User Directory)</h2>
                <p class="text-xs text-slate-400 font-mono mt-1">لوحة تحكم المالك والمؤسس لإدارة الإيميلات المنشأة ونشاطها.</p>
            </div>
            <button type="button" onclick="openNewAccountModal()" class="bg-cyan-500 hover:bg-cyan-400 text-slate-950 font-black px-4 py-2.5 rounded-xl text-xs cursor-pointer">+ إنشاء إيميل جديد</button>
        </div>
        <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-4" id="users-grid-container"></div>
    </main>

    <!-- View Mode 3: Server Logs (Admin Only) -->
    <main id="view-monitor" class="flex-1 max-w-7xl mx-auto w-full p-4 sm:p-6 space-y-6 overflow-y-auto hidden">
        <div class="flex justify-between items-center border-b border-slate-800 pb-4">
            <div>
                <h2 class="text-xl font-black text-cyan-400">مراقبة حركة البريد وسجلات السيرفر (Server Logs)</h2>
                <p class="text-xs text-slate-400 font-mono mt-1">سجل التدفق الحي لجميع الإيميلات الواردة والصادرة.</p>
            </div>
            <span class="text-xs font-mono text-emerald-400 bg-emerald-500/10 px-3 py-1.5 rounded-xl border border-emerald-500/30">SMTP Server: Active</span>
        </div>
        <div class="bg-slate-900 border border-slate-800 rounded-3xl overflow-hidden shadow-2xl">
            <div class="overflow-x-auto">
                <table class="w-full text-right text-xs font-mono">
                    <thead class="bg-slate-950 border-b border-slate-800 text-slate-400">
                        <tr><th class="p-3.5">المرسل</th><th class="p-3.5">المستلم</th><th class="p-3.5">الموضوع</th><th class="p-3.5">التشفير</th><th class="p-3.5">الحالة</th></tr>
                    </thead>
                    <tbody class="divide-y divide-slate-800 text-slate-300" id="logs-table-body"></tbody>
                </table>
            </div>
        </div>
    </main>

    <!-- Admin PIN Gate Modal -->
    <div id="modal-admin-gate" class="fixed inset-0 bg-slate-950/85 backdrop-blur-md z-50 flex items-center justify-center p-4 hidden">
        <div class="bg-slate-900 border border-amber-500/40 rounded-3xl p-6 max-w-md w-full shadow-2xl space-y-5 relative">
            <button type="button" onclick="closeAdminGate()" class="absolute top-4 right-4 text-slate-400 hover:text-white font-bold">✕</button>
            <div class="flex items-center gap-3">
                <div class="w-12 h-12 rounded-2xl bg-amber-400 flex items-center justify-center text-slate-950 font-black"><i data-lucide="shield" class="w-6 h-6"></i></div>
                <div>
                    <h3 class="font-bold text-lg text-slate-100">منطقة الإدارة والمؤسس</h3>
                    <p class="text-xs text-slate-400">محصورة فقط بالمؤسس Salh Alheib (الرمز: 0527550114)</p>
                </div>
            </div>
            <div class="space-y-3 font-mono text-xs">
                <input type="password" id="admin-pin-input" placeholder="أدخل رمز المؤسس السري..." class="w-full bg-slate-950 p-3 rounded-xl border border-slate-800 text-amber-400 focus:outline-none focus:border-amber-400" />
                <p id="admin-pin-error" class="text-xs text-rose-400 hidden">الرمز غير صحيح! هذا القسم مخصص للمؤسس فقط.</p>
            </div>
            <button type="button" onclick="verifyAdminPin()" class="w-full bg-amber-400 hover:bg-amber-300 text-slate-950 font-black py-3 rounded-xl text-sm cursor-pointer">تحقق والدخول للوحة التحكم</button>
        </div>
    </div>

    <!-- Create New Mailbox Modal -->
    <div id="modal-new-mailbox" class="fixed inset-0 bg-slate-950/85 backdrop-blur-md z-50 flex items-center justify-center p-4 hidden">
        <div class="bg-slate-900 border border-cyan-500/40 rounded-3xl p-6 max-w-md w-full shadow-2xl space-y-4 relative">
            <button type="button" onclick="closeNewMailboxModal()" class="absolute top-4 right-4 text-slate-400 hover:text-white font-bold">✕</button>
            <h3 class="font-bold text-lg text-slate-100">إنشاء صندوق بريد جديد</h3>
            <div class="space-y-3 font-mono text-xs">
                <input type="text" id="new-fullname" placeholder="الاسم الكامل (مثلاً: يوسف الهيب)" class="w-full bg-slate-950 p-3 rounded-xl border border-slate-800 text-slate-200 focus:outline-none" />
                <div class="flex rounded-xl border border-slate-800 overflow-hidden bg-slate-950">
                    <input type="text" id="new-username" placeholder="اسم المستخدم (مثلاً: yosf)" class="flex-1 bg-transparent p-3 text-cyan-400 font-bold focus:outline-none" />
                    <span class="p-3 bg-slate-900 text-slate-400">@heib12.org</span>
                </div>
            </div>
            <button type="button" onclick="submitNewMailbox()" class="w-full bg-cyan-500 text-slate-950 font-black py-3 rounded-xl text-sm cursor-pointer">إنشاء الصندوق فوراً</button>
        </div>
    </div>

    <!-- Compose Modal -->
    <div id="modal-compose" class="fixed inset-0 bg-slate-950/85 backdrop-blur-md z-50 flex items-center justify-center p-4 hidden">
        <div class="bg-slate-900 border border-cyan-500/40 rounded-3xl p-6 max-w-xl w-full shadow-2xl space-y-4 relative">
            <div class="flex justify-between items-center border-b border-slate-800 pb-3">
                <h3 class="font-bold text-base text-white">رسالة مشفرة جديدة (New Secure Message)</h3>
                <button type="button" onclick="closeCompose()" class="text-slate-400 hover:text-white font-bold">✕</button>
            </div>
            <div class="space-y-3 font-mono text-xs">
                <input type="email" id="compose-to" placeholder="المرسل إليه (recipient@domain.com)" class="w-full bg-slate-950 p-3 rounded-xl border border-slate-800 text-slate-200 focus:outline-none" />
                <input type="text" id="compose-subject" placeholder="موضوع الرسالة..." class="w-full bg-slate-950 p-3 rounded-xl border border-slate-800 text-slate-200 font-bold focus:outline-none" />
                <textarea id="compose-body" placeholder="اكتب رسالتك الآمنة هنا..." class="w-full h-40 bg-slate-950 p-3 rounded-2xl border border-slate-800 text-slate-200 focus:outline-none font-sans text-xs resize-none"></textarea>
            </div>
            <button type="button" onclick="dispatchEmail()" class="w-full bg-cyan-500 text-slate-950 font-black py-3 rounded-xl text-sm cursor-pointer">إرسال عبر SMTP الآمن</button>
        </div>
    </div>

    <!-- Footer -->
    <footer class="border-t border-slate-800 py-6 text-center text-xs text-slate-500 space-y-1">
        <p>heib12 Universal Sovereign System & Language Studio</p>
        <p class="text-slate-400 font-mono">Official Support: <a href="mailto:alasod5550@gmail.com" class="text-cyan-400 hover:underline">alasod5550@gmail.com</a></p>
    </footer>

    <!-- JavaScript Controllers -->
    <script>
        lucide.createIcons();

        let accounts = [
            { name: "Salh Alheib", email: "salh@heib12.org", role: "Founder & Chief Architect", pin: "0527550114" },
            { name: "Yosf Heib Klel", email: "yosf@heib12.org", role: "Co-Founder & Deputy" }
        ];
        let currentAccountIndex = 0;
        let activeFolder = "inbox";
        let selectedEmailId = "email-1";
        let isAdminUnlocked = false;
        let pendingAdminView = null;

        let emails = [
            { id: "email-1", senderName: "heib12 Tokamak Core", senderEmail: "tokamak-telemetry@energy.h12.org", recipientEmail: "salh@heib12.org", subject: "[TELEMETRY] 150,000,000°C Plasma Confinement Stabilized", body: "Diagnostic Report: Tokamak Plasma Fusion Core (v12.0)\nTimestamp: Real-time 0.008ms Deterministic Telemetry Cycle\nSTATUS: OPTIMAL CONFINEMENT (Zero Disruptions)\nCore Toroidal Field: 13.52 Tesla", date: "10:42 AM", read: false, folder: "inbox", securityTier: "Quantum Ring0", tags: ["Industrial", "Fusion"] },
            { id: "email-2", senderName: "Yosf Heib Klel", senderEmail: "yosf@heib12.org", recipientEmail: "salh@heib12.org", subject: "Sovereign Mail Infrastructure Active", body: "I have finalized the sovereign mail server architecture for @heib12.org infrastructure with DKIM and DMARC enforcement.", date: "09:15 AM", read: true, folder: "inbox", securityTier: "Post-Quantum Kyber", tags: ["Founders"] },
            { id: "email-3", senderName: "Aerospace Flight Command", senderEmail: "avionics@orbit.h12.org", recipientEmail: "salh@heib12.org", subject: "[FLIGHT REPORT] Orbital Rocket Landing Burn Verified", body: "Mission Telemetry Log: Orbital Multistage Rocket (Flight H12-ORBIT-09)\nResult: 100% Deterministic Execution with Zero Memory Interrupts.", date: "Yesterday", read: true, folder: "telemetry", securityTier: "Quantum Ring0", tags: ["Aerospace"] }
        ];

        function showToast(msg) {
            const banner = document.getElementById('toast-banner');
            const text = document.getElementById('toast-text');
            if(!banner || !text) return;
            text.innerText = msg;
            banner.classList.remove('opacity-0', 'scale-95');
            banner.classList.add('opacity-100', 'scale-100');
            setTimeout(() => {
                banner.classList.remove('opacity-100', 'scale-100');
                banner.classList.add('opacity-0', 'scale-95');
            }, 2500);
        }

        function copyCurrentEmail() {
            const cur = accounts[currentAccountIndex].email;
            navigator.clipboard.writeText(cur);
            showToast("✓ تم نسخ الإيميل: " + cur);
        }

        function switchViewMode(mode) {
            ['webmail', 'users', 'monitor'].forEach(m => {
                document.getElementById('view-' + m).classList.add('hidden');
                const btn = document.getElementById('nav-btn-' + m);
                if(btn) btn.className = "px-3 py-1.5 rounded-xl font-bold transition-all flex items-center gap-1.5 text-slate-400 hover:text-white cursor-pointer";
            });
            document.getElementById('view-' + mode).classList.remove('hidden');
            const activeBtn = document.getElementById('nav-btn-' + mode);
            if(activeBtn) activeBtn.className = "px-3 py-1.5 rounded-xl font-bold transition-all flex items-center gap-1.5 bg-cyan-500 text-slate-950 shadow cursor-pointer";
            
            if(mode === 'users') renderUsersDirectory();
            if(mode === 'monitor') renderServerLogs();
        }

        function requestAdminView(view) {
            if(isAdminUnlocked) {
                switchViewMode(view);
            } else {
                pendingAdminView = view;
                document.getElementById('modal-admin-gate').classList.remove('hidden');
            }
        }

        function closeAdminGate() { document.getElementById('modal-admin-gate').classList.add('hidden'); }

        function verifyAdminPin() {
            const pin = document.getElementById('admin-pin-input').value.trim();
            if(pin === "0527550114") {
                isAdminUnlocked = true;
                closeAdminGate();
                document.getElementById('users-tab-label').innerText = "Users (Unlocked)";
                document.getElementById('monitor-tab-label').innerText = "Server Logs (Unlocked)";
                showToast("✓ تم التحقق: مرحباً بك يا مؤسس النظام!");
                if(pendingAdminView) switchViewMode(pendingAdminView);
            } else {
                document.getElementById('admin-pin-error').classList.remove('hidden');
            }
        }

        function switchFolder(folder) {
            activeFolder = folder;
            ['inbox', 'sent', 'vault', 'telemetry'].forEach(f => {
                const el = document.getElementById('folder-' + f);
                if(el) el.className = "w-full flex items-center justify-between px-3 py-2.5 rounded-xl text-slate-400 hover:bg-slate-800/60 cursor-pointer";
            });
            const sel = document.getElementById('folder-' + folder);
            if(sel) sel.className = "w-full flex items-center justify-between px-3 py-2.5 rounded-xl bg-cyan-500 text-slate-950 font-bold shadow-md cursor-pointer";
            renderEmailsList();
            if(window.innerWidth < 1024) toggleMobileSidebar();
        }

        function toggleMobileSidebar() {
            const sb = document.getElementById('mobile-sidebar');
            sb.classList.toggle('-translate-x-full');
        }

        function renderEmailsList() {
            const container = document.getElementById('emails-list-container');
            const curEmail = accounts[currentAccountIndex].email.toLowerCase();
            
            const visible = emails.filter(e => {
                if(e.folder !== activeFolder) return false;
                if(!isAdminUnlocked && e.recipientEmail.toLowerCase() !== curEmail && e.senderEmail.toLowerCase() !== curEmail) return false;
                return true;
            });

            if(visible.length === 0) {
                container.innerHTML = `<div class="p-8 text-center text-slate-500 text-xs">No messages found in this folder.</div>`;
                return;
            }

            container.innerHTML = visible.map(e => `
                <div onclick="selectEmail('${e.id}')" class="p-3.5 transition-all cursor-pointer space-y-1.5 ${e.id === selectedEmailId ? 'bg-slate-900 border-l-4 border-l-cyan-400' : 'hover:bg-slate-900/60'}">
                    <div class="flex items-center justify-between text-xs">
                        <span class="font-bold ${!e.read ? 'text-cyan-400' : 'text-slate-200'}">${e.senderName}</span>
                        <span class="text-[10px] font-mono text-slate-500">${e.date}</span>
                    </div>
                    <div class="text-xs font-semibold text-slate-300 truncate">${e.subject}</div>
                    <p class="text-[11px] text-slate-500 line-clamp-2">${e.body}</p>
                </div>
            `).join('');
            
            if(visible.length > 0 && !visible.find(x => x.id === selectedEmailId)) {
                selectEmail(visible[0].id);
            }
        }

        function selectEmail(id) {
            selectedEmailId = id;
            const email = emails.find(e => e.id === id);
            if(!email) return;
            email.read = true;
            renderEmailsList();

            const detail = document.getElementById('email-detail-container');
            detail.innerHTML = `
                <div class="p-4 sm:p-6 border-b border-slate-800 bg-slate-950/60 space-y-3 text-right">
                    <div class="flex items-center justify-between">
                        <div>
                            <h2 class="font-bold text-base text-slate-100">${email.senderName} <span class="text-xs text-slate-400 font-mono">(${email.senderEmail})</span></h2>
                            <p class="text-[11px] text-slate-400 font-mono">To: ${email.recipientEmail} • ${email.date}</p>
                        </div>
                        <span class="text-[10px] font-mono text-emerald-400 bg-emerald-500/10 border border-emerald-500/30 px-2.5 py-0.5 rounded-full font-bold">${email.securityTier}</span>
                    </div>
                    <h3 class="text-base font-black text-white">${email.subject}</h3>
                </div>
                <div class="flex-1 p-6 overflow-y-auto text-xs text-slate-200 font-mono whitespace-pre-wrap leading-relaxed text-right">${email.body}</div>
            `;
            if(window.innerWidth < 1024) {
                document.getElementById('pane-list').classList.add('hidden');
                document.getElementById('pane-detail').classList.remove('hidden');
            }
        }

        function renderUsersDirectory() {
            const container = document.getElementById('users-grid-container');
            container.innerHTML = accounts.map((acc, idx) => `
                <div class="bg-slate-900 border ${idx === currentAccountIndex ? 'border-cyan-500 ring-2 ring-cyan-500/30' : 'border-slate-800'} p-5 rounded-2xl flex flex-col justify-between gap-4">
                    <div>
                        <h4 class="font-bold text-sm text-slate-100">${acc.name}</h4>
                        <p class="text-xs font-mono text-cyan-300 mt-0.5">${acc.email}</p>
                        <p class="text-[10px] text-slate-400 mt-0.5">${acc.role}</p>
                    </div>
                    <button type="button" onclick="currentAccountIndex=${idx}; switchViewMode('webmail'); showToast('تم التبديل إلى: ${acc.email}');" class="bg-slate-800 hover:bg-cyan-500 hover:text-slate-950 text-slate-200 font-bold py-2 rounded-xl text-xs transition-all cursor-pointer">الدخول لبريده</button>
                </div>
            `).join('');
        }

        function renderServerLogs() {
            const tbody = document.getElementById('logs-table-body');
            tbody.innerHTML = emails.map(e => `
                <tr class="hover:bg-slate-800/40">
                    <td class="p-3.5">${e.senderName}<br><span class="text-[10px] text-slate-500">${e.senderEmail}</span></td>
                    <td class="p-3.5">${e.recipientEmail}</td>
                    <td class="p-3.5 font-bold text-white">${e.subject}</td>
                    <td class="p-3.5"><span class="text-[10px] bg-emerald-500/10 text-emerald-400 px-2 py-0.5 rounded">${e.securityTier}</span></td>
                    <td class="p-3.5"><span class="text-[10px] bg-cyan-500/10 text-cyan-400 px-2 py-0.5 rounded font-bold">Delivered (250 OK)</span></td>
                </tr>
            `).join('');
        }

        function openNewAccountModal() { document.getElementById('modal-new-mailbox').classList.remove('hidden'); }
        function closeNewMailboxModal() { document.getElementById('modal-new-mailbox').classList.add('hidden'); }
        function submitNewMailbox() {
            const name = document.getElementById('new-fullname').value.trim();
            const user = document.getElementById('new-username').value.trim();
            if(!user) { showToast("يرجى إدخال اسم المستخدم"); return; }
            accounts.push({ name: name || user, email: user + "@heib12.org", role: "Certified User" });
            closeNewMailboxModal();
            showToast("✓ تم إنشاء صندوق البريد بنجاح!");
            if(document.getElementById('view-users').classList.contains('hidden') === false) renderUsersDirectory();
        }

        function openCompose() { document.getElementById('modal-compose').classList.remove('hidden'); }
        function closeCompose() { document.getElementById('modal-compose').classList.add('hidden'); }
        function dispatchEmail() {
            const to = document.getElementById('compose-to').value.trim();
            const sub = document.getElementById('compose-subject').value.trim();
            const body = document.getElementById('compose-body').value.trim();
            if(!to || !sub) { showToast("يرجى تعبئة الحقول الأساسية"); return; }

            emails.unshift({
                id: "email-" + Date.now(),
                senderName: accounts[currentAccountIndex].name,
                senderEmail: accounts[currentAccountIndex].email,
                recipientEmail: to,
                subject: sub,
                body: body || "[Empty]",
                date: "الآن",
                read: true,
                folder: "sent",
                securityTier: "Quantum Ring0",
                tags: ["Outgoing"]
            });
            closeCompose();
            showToast("✓ تم إرسال الرسالة عبر SMTP الآمن!");
            if(activeFolder === 'sent') renderEmailsList();
        }

        function filterEmails() { renderEmailsList(); }

        // Initial render
        document.getElementById('current-user-email').innerText = accounts[0].email;
        renderEmailsList();
    </script>
</body>
</html>
