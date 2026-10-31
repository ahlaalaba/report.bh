<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>نظام بلاغات وتقارير المضيف - العباءة</title>
    <!-- Tailwind CSS CDN -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- FontAwesome Icons -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <!-- Cairo Font -->
    <link href="https://fonts.googleapis.com/css2?family=Cairo:wght@300;400;600;700;800&display=swap" rel="stylesheet">
    <style>
        body {
            font-family: 'Cairo', sans-serif;
        }
        .glass-modal {
            background: rgba(15, 23, 42, 0.75);
            backdrop-filter: blur(12px);
        }
    </style>
</head>
<body class="bg-slate-100 text-slate-800 min-h-screen flex flex-col justify-between selection:bg-amber-500 selection:text-white">

    <!-- Header / Navbar -->
    <header class="bg-slate-900 text-white sticky top-0 z-30 shadow-md">
        <div class="max-w-5xl mx-auto px-4 sm:px-6 h-20 flex items-center justify-between">
            <div class="flex items-center space-x-3 space-x-reverse">
                <div class="w-11 h-11 bg-amber-500 text-slate-900 rounded-xl flex items-center justify-center font-bold text-xl shadow-md">
                    <i class="fa-solid fa-vest-patches"></i>
                </div>
                <div>
                    <h1 class="text-base sm:text-lg font-bold leading-tight">نظام تقارير المضيف - العباء</h1>
                    <p class="text-xs text-slate-400">نموذج إرسال البلاغات السريع</p>
                </div>
            </div>

            <!-- Admin Access Trigger (Lock Icon) -->
            <button onclick="openPasscodeModal()" 
                    class="px-4 py-2 bg-slate-800 hover:bg-slate-700 text-amber-400 rounded-xl border border-slate-700 text-xs font-bold transition-all flex items-center gap-2 shadow-sm">
                <i class="fa-solid fa-lock text-sm"></i>
                <span>لوحة الرصد والعرض</span>
            </button>
        </div>
    </header>

    <!-- Main Content Area -->
    <main class="max-w-3xl mx-auto px-4 sm:px-6 py-8 flex-grow w-full">
        
        <!-- View 1: Send Report Form Only -->
        <div id="submitFormSection" class="bg-white rounded-3xl shadow-sm border border-slate-200/80 p-6 sm:p-8">
            <div class="flex items-center justify-between mb-6 pb-4 border-b border-slate-100">
                <div class="flex items-center gap-3">
                    <div class="w-10 h-10 bg-amber-50 text-amber-600 rounded-xl flex items-center justify-center text-lg">
                        <i class="fa-solid fa-paper-plane"></i>
                    </div>
                    <div>
                        <h2 class="text-lg font-bold text-slate-800">إرسال بلاغ جديد</h2>
                        <p class="text-xs text-slate-400">يرجى تعبئة التفاصيل بدقة لإرسال التقرير فوراً</p>
                    </div>
                </div>
                <span class="text-xs font-semibold px-2.5 py-1 bg-emerald-50 text-emerald-600 rounded-lg border border-emerald-200">
                    <i class="fa-solid fa-circle text-[8px] ml-1"></i> النظام مباشر
                </span>
            </div>

            <!-- Success Alert Toast -->
            <div id="successToast" class="hidden mb-6 p-4 bg-emerald-50 text-emerald-800 text-xs sm:text-sm rounded-2xl border border-emerald-200 flex items-center gap-3 animate-bounce">
                <i class="fa-solid fa-circle-check text-emerald-600 text-lg"></i>
                <div>
                    <strong class="block font-bold">تم إرسال التقرير بنجاح!</strong>
                    <span>تم حفظ البلاغ في لوحة الرصد المركزية.</span>
                </div>
            </div>

            <form id="reportForm" onsubmit="submitReport(event)" class="space-y-5">
                
                <!-- Host Name & Date -->
                <div class="grid grid-cols-1 sm:grid-cols-2 gap-4">
                    <div>
                        <label class="block text-xs font-bold text-slate-700 mb-1.5">اسم المضيف / الموظف *</label>
                        <input type="text" id="hostName" required placeholder="أدخل الاسم..."
                               class="w-full px-4 py-3 rounded-xl border border-slate-300 text-sm focus:ring-2 focus:ring-amber-500 focus:border-amber-500 focus:outline-none transition-all">
                    </div>
                    <div>
                        <label class="block text-xs font-bold text-slate-700 mb-1.5">تاريخ البلاغ *</label>
                        <input type="date" id="reportDate" required
                               class="w-full px-4 py-3 rounded-xl border border-slate-300 text-sm focus:ring-2 focus:ring-amber-500 focus:border-amber-500 focus:outline-none transition-all">
                    </div>
                </div>

    
                        <label class="block text-xs font-bold text-slate-700 mb-1.5">/ رقم الهادف</label>
                        <input type="text" id="abayaTag" placeholder="  15"
                               class="w-full px-4 py-3 rounded-xl border border-slate-300 text-sm focus:ring-2 focus:ring-amber-500 focus:border-amber-500 focus:outline-none transition-all">
                    </div>
                </div>

                <!-- Priority Selection -->
                <div>
                    <label class="block text-xs font-bold text-slate-700 mb-1.5">درجة الأهمية *</label>
                    <div class="grid grid-cols-3 gap-3">
                        <label class="cursor-pointer">
                            <input type="radio" name="priority" value="عادي" checked class="peer hidden">
                            <div class="text-center py-2.5 px-2 text-xs rounded-xl border border-slate-200 peer-checked:bg-emerald-50 peer-checked:border-emerald-500 peer-checked:text-emerald-700 font-bold transition-all">
                                عادي
                            </div>
                        </label>
                        <label class="cursor-pointer">
                            <input type="radio" name="priority" value="هام" class="peer hidden">
                            <div class="text-center py-2.5 px-2 text-xs rounded-xl border border-slate-200 peer-checked:bg-amber-50 peer-checked:border-amber-500 peer-checked:text-amber-700 font-bold transition-all">
                                هام
                            </div>
                        </label>
                        <label class="cursor-pointer">
                            <input type="radio" name="priority" value="عاجل جداً" class="peer hidden">
                            <div class="text-center py-2.5 px-2 text-xs rounded-xl border border-slate-200 peer-checked:bg-rose-50 peer-checked:border-rose-500 peer-checked:text-rose-700 font-bold transition-all">
                                عاجل جداً
                            </div>
                        </label>
                    </div>
                </div>

                <!-- Details textarea -->
                <div>
                    <label class="block text-xs font-bold text-slate-700 mb-1.5">التفاصيل والملاحظات *</label>
                    <textarea id="reportDetails" rows="4" required placeholder="اكتب تفاصيل البلاغ والملاحظات المطلوبة هنا..."
                              class="w-full px-4 py-3 rounded-xl border border-slate-300 text-sm focus:ring-2 focus:ring-amber-500 focus:border-amber-500 focus:outline-none transition-all resize-none"></textarea>
                </div>

                <!-- Submit Button -->
                <button type="submit"
                        class="w-full py-4 bg-amber-500 hover:bg-amber-600 text-slate-900 font-extrabold rounded-xl shadow-md hover:shadow-lg transition-all flex items-center justify-center gap-2 text-base">
                    <i class="fa-solid fa-paper-plane"></i>
                    <span>إرسال البلاغ فوراً</span>
                </button>
            </form>
        </div>

        <!-- View 2: Dashboard / Monitor Board (Only Visible after Password) -->
        <div id="dashboardSection" class="hidden bg-white rounded-3xl shadow-sm border border-slate-200/80 p-6 sm:p-8">
            <div class="flex flex-col sm:flex-row sm:items-center justify-between gap-4 mb-6 pb-4 border-b border-slate-100">
                <div>
                    <div class="flex items-center gap-2">
                        <span class="w-3 h-3 rounded-full bg-emerald-500 animate-pulse"></span>
                        <h2 class="text-xl font-bold text-slate-800">لوحة رصد وعرض البلاغات</h2>
                    </div>
                    <p class="text-xs text-slate-400 mt-1">جميع البلاغات المحفوظة في النظام متزامنة باستمرار</p>
                </div>

                <div class="flex items-center gap-2">
                    <!-- Filter Dropdown -->
                    <select id="filterCategory" onchange="renderReports()" class="text-xs bg-slate-100 border border-slate-200 rounded-xl px-3 py-2 focus:outline-none focus:ring-2 focus:ring-amber-500 font-semibold">
                        <option value="الكل">جميع البلاغات</option>
                        <option value="عاجل جداً">عاجل جداً فقط</option>
                        <option value="عباءة مفقودة / عُثر عليها">مفقودة / عُثر عليها</option>
                        <option value="تبديل عباءة بالخطأ">تبديل بالخطأ</option>
                    </select>

                    <button onclick="closeDashboard()" 
                            class="px-3.5 py-2 bg-slate-100 hover:bg-slate-200 text-slate-700 rounded-xl text-xs font-bold transition-all flex items-center gap-1.5">
                        <i class="fa-solid fa-arrow-right"></i>
                        <span>قفل اللوحة</span>
                    </button>
                </div>
            </div>

            <!-- List Container -->
            <div id="reportsList" class="space-y-4">
                <!-- Items generated via JS -->
            </div>

            <!-- Empty State -->
            <div id="emptyState" class="hidden py-16 text-center">
                <div class="w-16 h-16 bg-slate-100 text-slate-400 rounded-full flex items-center justify-center mx-auto mb-3 text-2xl">
                    <i class="fa-solid fa-folder-open"></i>
                </div>
                <h3 class="text-slate-700 font-bold text-sm">لا توجد بلاغات مسجلة حالياً</h3>
                <p class="text-slate-400 text-xs mt-1">لم يتم إرسال أي بلاغات جديدة بعد</p>
            </div>

            <!-- Stats & Clear Action -->
            <div class="mt-8 pt-4 border-t border-slate-100 flex items-center justify-between text-xs text-slate-500">
                <div>إجمالي البلاغات الرصد: <span id="totalCount" class="font-bold text-slate-800">0</span></div>
                <button onclick="clearAllReports()" class="text-red-500 hover:text-red-700 font-bold text-xs flex items-center gap-1 hover:underline">
                    <i class="fa-solid fa-trash-can"></i> مسح كامل الرصد
                </button>
            </div>
        </div>

    </main>

    <!-- Passcode Modal -->
    <div id="passcodeModal" class="hidden fixed inset-0 z-50 glass-modal flex items-center justify-center p-4">
        <div class="bg-white max-w-md w-full p-6 sm:p-8 rounded-3xl shadow-2xl border border-slate-100 text-center relative overflow-hidden">
            <button onclick="closePasscodeModal()" class="absolute top-4 left-4 text-slate-400 hover:text-slate-600 p-2">
                <i class="fa-solid fa-xmark text-lg"></i>
            </button>

            <div class="w-16 h-16 bg-amber-50 text-amber-600 rounded-2xl flex items-center justify-center mx-auto mb-4 shadow-sm text-2xl">
                <i class="fa-solid fa-shield-halved"></i>
            </div>
            
            <h3 class="text-xl font-bold text-slate-800 mb-1">فتح لوحة العرض والرصد</h3>
            <p class="text-slate-500 text-xs mb-6">يرجى إدخال الرقم السري المعتمد للوصول للرصد</p>
            
            <form onsubmit="handlePasscodeSubmit(event)" class="space-y-4">
                <div>
                    <input type="password" id="passcodeInput" maxlength="12" placeholder="أدخل الرقم السري..." 
                           class="w-full px-4 py-3 text-center text-xl font-bold tracking-widest rounded-xl border border-slate-300 focus:outline-none focus:ring-2 focus:ring-amber-500 transition-all">
                </div>
                <div id="passcodeError" class="hidden text-red-500 text-xs font-semibold">
                    <i class="fa-solid fa-circle-exclamation ml-1"></i> الرقم السري غير صحيح!
                </div>
                <button type="submit" 
                        class="w-full py-3.5 bg-slate-900 hover:bg-slate-800 text-amber-400 font-bold rounded-xl shadow-lg transition-all flex items-center justify-center gap-2">
                    <i class="fa-solid fa-unlock"></i>
                    <span>دخول لوحة الرصد</span>
                </button>
            </form>
        </div>
    </div>

    <!-- Footer -->
    <footer class="bg-white border-t border-slate-200 py-4 text-center text-xs text-slate-500">
        <p>نظام إدارة بلاغات العباءة للمضيفين &copy; 2026 - جميع الحقوق محفوظة</p>
    </footer>

    <!-- JavaScript Logic -->
    <script>
        const VALID_PASSCODE = "36386184";
        const STORAGE_KEY = "host_abaya_reports_data";

        // Set Default Date on Load
        window.onload = function() {
            const today = new Date().toISOString().split('T')[0];
            document.getElementById('reportDate').value = today;
        };

        // Open/Close Modal
        function openPasscodeModal() {
            document.getElementById('passcodeModal').classList.remove('hidden');
            document.getElementById('passcodeInput').focus();
            document.getElementById('passcodeError').classList.add('hidden');
            document.getElementById('passcodeInput').value = "";
        }

        function closePasscodeModal() {
            document.getElementById('passcodeModal').classList.add('hidden');
        }

        // Handle Passcode Verification
        function handlePasscodeSubmit(e) {
            e.preventDefault();
            const passInput = document.getElementById('passcodeInput').value.trim();
            const errorEl = document.getElementById('passcodeError');

            if (passInput === VALID_PASSCODE) {
                closePasscodeModal();
                showDashboard();
            } else {
                errorEl.classList.remove('hidden');
                document.getElementById('passcodeInput').focus();
            }
        }

        // Show Dashboard View & Hide Form View
        function showDashboard() {
            document.getElementById('submitFormSection').classList.add('hidden');
            document.getElementById('dashboardSection').classList.remove('hidden');
            renderReports();
        }

        // Close Dashboard View & Return to Form
        function closeDashboard() {
            document.getElementById('dashboardSection').classList.add('hidden');
            document.getElementById('submitFormSection').classList.remove('hidden');
        }

        // Fetch reports from LocalStorage
        function getStoredReports() {
            const data = localStorage.getItem(STORAGE_KEY);
            return data ? JSON.parse(data) : [];
        }

        // Save reports to LocalStorage
        function saveReports(reports) {
            localStorage.setItem(STORAGE_KEY, JSON.stringify(reports));
        }

        // Submit New Report (Saves locally & stays on Form screen)
        function submitReport(e) {
            e.preventDefault();

            const hostName = document.getElementById('hostName').value.trim();
            const reportDate = document.getElementById('reportDate').value;
            const category = document.getElementById('reportCategory').value;
            const abayaTag = document.getElementById('abayaTag').value.trim();
            const priority = document.querySelector('input[name="priority"]:checked').value;
            const details = document.getElementById('reportDetails').value.trim();

            const newReport = {
                id: Date.now(),
                hostName,
                reportDate,
                category,
                abayaTag: abayaTag || "غير محدد",
                priority,
                details,
                timestamp: new Date().toLocaleTimeString('ar-SA', { hour: '2-digit', minute: '2-digit' })
            };

            const reports = getStoredReports();
            reports.unshift(newReport); // Insert latest first
            saveReports(reports);

            // Reset Form fields
            document.getElementById('reportForm').reset();
            document.getElementById('reportDate').value = new Date().toISOString().split('T')[0];

            // Show Feedback Alert Toast
            const toast = document.getElementById('successToast');
            toast.classList.remove('hidden');
            setTimeout(() => {
                toast.classList.add('hidden');
            }, 3500);
        }

        // Delete Individual Report
        function deleteReport(id) {
            let reports = getStoredReports();
            reports = reports.filter(r => r.id !== id);
            saveReports(reports);
            renderReports();
        }

        // Clear All Reports
        function clearAllReports() {
            if (confirm("هل أنت تأكد من رغبتك في مسح كافة بلاغات الرصد المحفوظة؟")) {
                localStorage.removeItem(STORAGE_KEY);
                renderReports();
            }
        }

        // Render Reports List in Dashboard View
        function renderReports() {
            const reports = getStoredReports();
            const filterValue = document.getElementById('filterCategory').value;
            const listContainer = document.getElementById('reportsList');
            const emptyState = document.getElementById('emptyState');
            const totalCountEl = document.getElementById('totalCount');

            // Apply Filters
            let filtered = reports;
            if (filterValue === "عاجل جداً") {
                filtered = reports.filter(r => r.priority === "عاجل جداً");
            } else if (filterValue !== "الكل") {
                filtered = reports.filter(r => r.category === filterValue);
            }

            totalCountEl.textContent = reports.length;

            if (filtered.length === 0) {
                listContainer.innerHTML = '';
                emptyState.classList.remove('hidden');
                return;
            }

            emptyState.classList.add('hidden');

            listContainer.innerHTML = filtered.map(item => {
                let priorityStyle = "bg-slate-100 text-slate-700 border-slate-200";
                if (item.priority === "عاجل جداً") priorityStyle = "bg-rose-50 text-rose-700 border-rose-200 animate-pulse";
                if (item.priority === "هام") priorityStyle = "bg-amber-50 text-amber-700 border-amber-200";

                return `
                    <div class="p-4 sm:p-5 rounded-2xl border border-slate-200 bg-slate-50/60 hover:bg-slate-50 transition-all space-y-3">
                        <div class="flex items-start justify-between gap-3">
                            <div class="flex flex-wrap items-center gap-2">
                                <span class="px-2.5 py-1 text-xs font-bold rounded-lg border ${priorityStyle}">
                                    ${item.priority}
                                </span>
                                <span class="text-xs font-bold px-2.5 py-1 bg-white rounded-lg border border-slate-200 text-slate-700">
                                    <i class="fa-solid fa-tag text-amber-500 ml-1"></i> ${item.category}
                                </span>
                            </div>
                            <button onclick="deleteReport(${item.id})" title="حذف البلاغ" 
                                    class="text-slate-400 hover:text-red-500 transition-colors p-1 text-xs">
                                <i class="fa-solid fa-trash-can text-sm"></i>
                            </button>
                        </div>

                        <div class="text-xs sm:text-sm text-slate-800 leading-relaxed font-semibold bg-white p-3.5 rounded-xl border border-slate-100 shadow-sm">
                            ${item.details}
                        </div>

                        <div class="flex flex-wrap items-center justify-between text-xs text-slate-500 pt-1 gap-2">
                            <div class="flex flex-wrap items-center gap-3">
                                <span><i class="fa-solid fa-user text-slate-400 ml-1"></i> <strong>المضيف:</strong> ${item.hostName}</span>
                                <span><i class="fa-solid fa-calendar text-slate-400 ml-1"></i> <strong>التاريخ:</strong> ${item.reportDate}</span>
                                ${item.abayaTag !== "غير محدد" ? `<span><i class="fa-solid fa-hashtag text-slate-400 ml-1"></i> <strong>الرقم/المكان:</strong> ${item.abayaTag}</span>` : ''}
                            </div>
                            <span class="text-[11px] bg-slate-200 text-slate-700 px-2.5 py-0.5 rounded-lg font-mono font-semibold">
                                ${item.timestamp}
                            </span>
                        </div>
                    </div>
                `;
            }).join('');
        }
    </script>
</body>
</html>
