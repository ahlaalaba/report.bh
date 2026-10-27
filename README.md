<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>نظام بلاغات العباءة للمضيف</title>
    <!-- Tailwind CSS CDN -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- FontAwesome Icons -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <!-- Cairo Font -->
    <link href="https://fonts.googleapis.com/css2?family=Cairo:wght@400;600;700;800&display=swap" rel="stylesheet">
    <style>
        body {
            font-family: 'Cairo', sans-serif;
        }
    </style>
</head>
<body class="bg-slate-100 text-slate-800 min-h-screen flex flex-col justify-between selection:bg-amber-500 selection:text-white">

    <!-- Header -->
    <header class="bg-slate-900 text-white sticky top-0 z-40 shadow-md">
        <div class="max-w-6xl mx-auto px-4 sm:px-6 h-20 flex items-center justify-between">
            <div class="flex items-center gap-3">
                <div class="w-12 h-12 bg-amber-500 text-slate-900 rounded-xl flex items-center justify-center font-bold text-xl shadow-md">
                    <i class="fa-solid fa-vest-patches"></i>
                </div>
                <div>
                    <h1 class="text-lg sm:text-xl font-bold leading-tight">نظام بلاغات العباءة</h1>
                    <p class="text-xs text-slate-400">إرسال واستعراض التقرير مباشر</p>
                </div>
            </div>

            <div class="flex items-center gap-2 bg-slate-800 text-amber-400 px-3 py-1.5 rounded-lg border border-slate-700 text-xs font-semibold">
                <span class="w-2.5 h-2.5 rounded-full bg-emerald-500 animate-pulse"></span>
                <span>النظام مباشر وتلقائي</span>
            </div>
        </div>
    </header>

    <!-- Main Content Grid -->
    <main class="max-w-6xl mx-auto px-4 sm:px-6 py-8 flex-grow w-full">
        <div class="grid grid-cols-1 lg:grid-cols-12 gap-8">
            
            <!-- Form Section (5 Columns) -->
            <section class="lg:col-span-5">
                <div class="bg-white rounded-2xl shadow-sm border border-slate-200 p-6 sticky top-28">
                    <h2 class="text-lg font-bold text-slate-800 flex items-center gap-2 mb-4 pb-3 border-b border-slate-100">
                        <i class="fa-solid fa-paper-plane text-amber-500"></i>
                        تقديم بلاغ جديد
                    </h2>

                    <form id="abayaReportForm" onsubmit="handleReportSubmit(event)" class="space-y-4">
                        <!-- Host Name -->
                        <div>
                            <label class="block text-xs font-bold text-slate-700 mb-1">اسم المضيف / الموظف *</label>
                            <input type="text" id="hostName" required placeholder="أدخل اسمك..."
                                   class="w-full px-3.5 py-2.5 rounded-xl border border-slate-300 text-sm focus:ring-2 focus:ring-amber-500 focus:outline-none transition-all">
                        </div>

                        <!-- Date Selection -->
                        <div>
                            <label class="block text-xs font-bold text-slate-700 mb-1">تاريخ البلاغ *</label>
                            <input type="date" id="reportDate" required
                                   class="w-full px-3.5 py-2.5 rounded-xl border border-slate-300 text-sm focus:ring-2 focus:ring-amber-500 focus:outline-none transition-all">
                        </div>

                        <!-- Report Topic / Subject -->
                        <div>
                            <label class="block text-xs font-bold text-slate-700 mb-1">موضوع / نوع البلاغ *</label>
                            <select id="reportTopic" required class="w-full px-3.5 py-2.5 rounded-xl border border-slate-300 text-sm focus:ring-2 focus:ring-amber-500 focus:outline-none transition-all">
                                <option value="عباءة مفقودة">عباءة مفقودة</option>
                                <option value="عباءة تم العثور عليها">عباءة تم العثور عليها</option>
                                <option value="تبديل عباءة بالخطأ">تبديل عباءة بالخطأ</option>
                                <option value="عباءة بدون رقم أو بطاقة">عباءة بدون رقم / بطاقة</option>
                                <option value="ملاحظة أو استفسار آخر">ملاحظة أو استفسار آخر</option>
                            </select>
                        </div>

                        <!-- Details -->
                        <div>
                            <label class="block text-xs font-bold text-slate-700 mb-1">تفاصيل البلاغ *</label>
                            <textarea id="reportDetails" rows="4" required placeholder="اكتب التفاصيل الكاملة للبلاغ..."
                                      class="w-full px-3.5 py-2.5 rounded-xl border border-slate-300 text-sm focus:ring-2 focus:ring-amber-500 focus:outline-none transition-all resize-none"></textarea>
                        </div>

                        <!-- Submit Button -->
                        <button type="submit" 
                                class="w-full py-3 bg-amber-500 hover:bg-amber-600 active:scale-[0.99] text-slate-900 font-bold rounded-xl shadow-md hover:shadow-lg transition-all flex items-center justify-center gap-2">
                            <i class="fa-solid fa-paper-plane"></i>
                            <span>إرسال وإضافة فورة</span>
                        </button>
                    </form>
                </div>
            </section>

            <!-- Display Section (7 Columns) -->
            <section class="lg:col-span-7">
                <div class="bg-white rounded-2xl shadow-sm border border-slate-200 p-6 min-h-[500px] flex flex-col justify-between">
                    <div>
                        <!-- Header & Search/Filter Bar -->
                        <div class="flex flex-col sm:flex-row sm:items-center justify-between gap-4 mb-6 pb-4 border-b border-slate-100">
                            <div>
                                <h2 class="text-lg font-bold text-slate-800 flex items-center gap-2">
                                    <i class="fa-solid fa-list-check text-amber-500"></i>
                                    البلاغات والتقارير المعروضة
                                </h2>
                                <p class="text-xs text-slate-400">محفوظة تلقائياً ومتاحة دائماً</p>
                            </div>

                            <!-- Quick Filter -->
                            <div class="flex items-center gap-2">
                                <span class="text-xs font-bold text-slate-500 whitespace-nowrap">تصفية:</span>
                                <select id="filterTopic" onchange="renderReports()" class="text-xs bg-slate-100 border border-slate-200 rounded-lg px-2.5 py-1.5 focus:outline-none focus:ring-1 focus:ring-amber-500">
                                    <option value="الكل">عرض الكل</option>
                                    <option value="عباءة مفقودة">عباءة مفقودة</option>
                                    <option value="عباءة تم العثور عليها">تم العثور عليها</option>
                                    <option value="تبديل عباءة بالخطأ">تبديل بالخطأ</option>
                                    <option value="عباءة بدون رقم أو بطاقة">بدون رقم</option>
                                    <option value="ملاحظة أو استفسار آخر">أخرى</option>
                                </select>
                            </div>
                        </div>

                        <!-- Alert message -->
                        <div id="toastMessage" class="hidden mb-4 p-3 bg-emerald-50 text-emerald-700 text-xs rounded-xl border border-emerald-200 flex items-center gap-2">
                            <i class="fa-solid fa-circle-check"></i>
                            <span>تم إرسال البلاغ وحفظه في النظام بنجاح!</span>
                        </div>

                        <!-- Reports List Feed -->
                        <div id="reportsContainer" class="space-y-4">
                            <!-- Dynamic Content Here -->
                        </div>

                        <!-- Empty Placeholder -->
                        <div id="emptyMessage" class="hidden py-16 text-center">
                            <div class="w-16 h-16 bg-slate-100 text-slate-400 rounded-full flex items-center justify-center mx-auto mb-3 text-2xl">
                                <i class="fa-solid fa-clipboard-list"></i>
                            </div>
                            <h3 class="text-slate-600 font-bold text-sm">لا توجد بلاغات حالياً</h3>
                            <p class="text-slate-400 text-xs mt-1">قم بتعبئة النموذج على اليمين لإرسال بلاغ جديد</p>
                        </div>
                    </div>

                    <!-- Footer Details -->
                    <div class="mt-8 pt-4 border-t border-slate-100 flex items-center justify-between text-xs text-slate-500">
                        <div>إجمالي البلاغات: <span id="reportsCount" class="font-bold text-slate-800">0</span></div>
                        <button onclick="clearAllData()" class="text-red-500 hover:text-red-700 text-xs font-semibold flex items-center gap-1 hover:underline">
                            <i class="fa-solid fa-trash-can"></i> مسح الكل
                        </button>
                    </div>
                </div>
            </section>

        </div>
    </main>

    <!-- Footer -->
    <footer class="bg-white border-t border-slate-200 py-4 text-center text-xs text-slate-500">
        <p>نظام إداري مخصص لبلاغات العباءة &copy; 2026</p>
    </footer>

    <!-- JavaScript Logic -->
    <script>
        const STORAGE_KEY = 'abaya_reports_simple_db';

        // Set default date input to today
        document.addEventListener('DOMContentLoaded', () => {
            document.getElementById('reportDate').valueAsDate = new Date();
            renderReports();
        });

        // Get saved data
        function getReports() {
            const data = localStorage.getItem(STORAGE_KEY);
            return data ? JSON.parse(data) : [];
        }

        // Save data
        function saveReports(data) {
            localStorage.setItem(STORAGE_KEY, JSON.stringify(data));
        }

        // Submit new report
        function handleReportSubmit(e) {
            e.preventDefault();

            const hostName = document.getElementById('hostName').value.trim();
            const reportDate = document.getElementById('reportDate').value;
            const reportTopic = document.getElementById('reportTopic').value;
            const reportDetails = document.getElementById('reportDetails').value.trim();

            const newReport = {
                id: Date.now(),
                hostName,
                date: reportDate,
                topic: reportTopic,
                details: reportDetails,
                time: new Date().toLocaleTimeString('ar-SA', { hour: '2-digit', minute: '2-digit' })
            };

            const reports = getReports();
            reports.unshift(newReport); // Add to beginning of array
            saveReports(reports);

            // Reset form fields
            document.getElementById('abayaReportForm').reset();
            document.getElementById('reportDate').valueAsDate = new Date();

            // Show confirmation toast
            const toast = document.getElementById('toastMessage');
            toast.classList.remove('hidden');
            setTimeout(() => {
                toast.classList.add('hidden');
            }, 3000);

            // Re-render display
            renderReports();
        }

        // Delete a single report
        function deleteReport(id) {
            let reports = getReports();
            reports = reports.filter(r => r.id !== id);
            saveReports(reports);
            renderReports();
        }

        // Clear all reports
        function clearAllData() {
            if (confirm("هل تريد حذف كافة البلاغات المسجلة؟")) {
                localStorage.removeItem(STORAGE_KEY);
                renderReports();
            }
        }

        // Render function to list reports
        function renderReports() {
            const reports = getReports();
            const filterValue = document.getElementById('filterTopic').value;
            const container = document.getElementById('reportsContainer');
            const emptyMessage = document.getElementById('emptyMessage');
            const countEl = document.getElementById('reportsCount');

            // Filter logic
            let filtered = reports;
            if (filterValue !== "الكل") {
                filtered = reports.filter(r => r.topic === filterValue);
            }

            countEl.textContent = reports.length;

            if (filtered.length === 0) {
                container.innerHTML = '';
                emptyMessage.classList.remove('hidden');
                return;
            }

            emptyMessage.classList.add('hidden');

            container.innerHTML = filtered.map(item => `
                <div class="p-4 rounded-xl border border-slate-200 bg-slate-50/60 hover:bg-slate-50 transition-all space-y-3">
                    <div class="flex items-center justify-between gap-2">
                        <span class="px-3 py-1 text-xs font-bold rounded-lg bg-amber-100 text-amber-800 border border-amber-200 flex items-center gap-1.5">
                            <i class="fa-solid fa-tag text-amber-600"></i> ${item.topic}
                        </span>
                        <div class="flex items-center gap-3">
                            <span class="text-xs text-slate-400 font-mono"><i class="fa-regular fa-clock ml-1"></i>${item.time}</span>
                            <button onclick="deleteReport(${item.id})" class="text-slate-400 hover:text-red-500 transition-colors" title="حذف البلاغ">
                                <i class="fa-solid fa-trash-can text-sm"></i>
                            </button>
                        </div>
                    </div>

                    <p class="text-xs sm:text-sm text-slate-700 leading-relaxed font-medium bg-white p-3 rounded-lg border border-slate-100">
                        ${item.details}
                    </p>

                    <div class="flex items-center justify-between text-xs text-slate-500 pt-1">
                        <div>
                            <i class="fa-solid fa-user-pen text-slate-400 ml-1"></i> 
                            <span>صاحب البلاغ / المضيف: </span>
                            <strong class="text-slate-700">${item.hostName}</strong>
                        </div>
                        <div>
                            <i class="fa-solid fa-calendar-day text-slate-400 ml-1"></i> 
                            <strong class="text-slate-700">${item.date}</strong>
                        </div>
                    </div>
                </div>
            `).join('');
        }
    </script>
</body>
</html>
