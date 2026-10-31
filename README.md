<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>تقرير مضيف أهل العباء - البلاد القديم</title>
  
  <!-- Tailwind CSS CDN -->
  <script src="https://cdn.tailwindcss.com"></script>
  <!-- Google Fonts: Cairo -->
  <link href="https://fonts.googleapis.com/css2?family=Cairo:wght@400;600;700;800;900&display=swap" rel="stylesheet">
  <!-- FontAwesome Icons -->
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">

  <script>
    tailwind.config = {
      theme: {
        extend: {
          fontFamily: {
            cairo: ['Cairo', 'sans-serif'],
          },
          colors: {
            maroon: {
              50: '#fdf2f2',
              100: '#fde8e8',
              700: '#800000',
              800: '#660000',
              900: '#4a0000',
            },
            gold: {
              400: '#fbbf24',
              500: '#d97706',
              600: '#b45309',
            }
          }
        }
      }
    }
  </script>

  <style>
    body {
      font-family: 'Cairo', sans-serif;
      background-color: #f3f4f6;
    }
    
    /* الشعار في خلفية الورقة بنسبة وضوح 50% */
    .watermark-bg {
      position: relative;
    }
    .watermark-bg::before {
      content: "";
      position: absolute;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
      width: 75%;
      height: 75%;
      background-image: url('image_be668db9-removebg-preview.png');
      background-repeat: no-repeat;
      background-position: center;
      background-size: contain;
      opacity: 0.50;
      pointer-events: none;
      z-index: 0;
    }

    .print-content {
      position: relative;
      z-index: 10;
    }

    @media print {
      .no-print {
        display: none !important;
      }
      body {
        background-color: white !important;
        padding: 0 !important;
        margin: 0 !important;
      }
      .print-container {
        box-shadow: none !important;
        border: none !important;
        width: 100% !important;
        max-width: 100% !important;
        padding: 0 !important;
      }
      .watermark-bg::before {
        opacity: 0.30 !important;
        -webkit-print-color-adjust: exact;
        print-color-adjust: exact;
      }
      textarea, input, select {
        border: none !important;
        background: transparent !important;
        appearance: none !important;
      }
    }
  </style>
</head>
<body class="bg-gray-100 min-h-screen p-3 md:p-6 text-gray-800">

  <div class="max-w-4xl mx-auto mb-20">
    
    <!-- ورقة التقرير -->
    <div class="print-container watermark-bg bg-white rounded-xl shadow-lg border border-gray-200 p-6 md:p-10 relative overflow-hidden">
      
      <div class="print-content">

        <!-- الترويسة الهيدر الرسمية -->
        <header class="border-b-2 border-maroon-700 pb-6 mb-6">
          <div class="flex flex-col md:flex-row justify-between items-center gap-4 text-center md:text-right">
            
            <!-- الشعار مع الاسم الكامل للمواقف والرعاية -->
            <div class="flex items-center gap-4">
              <img src="image_be668db9-removebg-preview.png" alt="مضيف أهل العباء" class="h-20 w-auto object-contain">
              <div>
                <h1 class="text-2xl md:text-3xl font-black text-maroon-800 tracking-wide">مضيف أهل العباء</h1>
                <p class="text-xs md:text-sm text-gold-600 font-bold mt-1">
                  <i class="fa-solid fa-location-dot ml-1"></i> البلاد القديم — مملكة البحرين
                </p>
                <p class="text-[11px] text-gray-400 font-semibold mt-0.5">نظام إرسال وتوثيق التقارير اليومية</p>
              </div>
            </div>

            <!-- اليوم والتاريخ والساعة الحية -->
            <div class="bg-maroon-50/90 backdrop-blur-sm border border-maroon-100 rounded-lg p-3 text-center md:text-left min-w-[210px]">
              <div id="liveDay" class="text-maroon-800 font-black text-sm">--</div>
              <div id="liveDate" class="text-gray-600 text-xs font-semibold my-0.5">--/--/----</div>
              <div id="liveTime" class="text-gold-600 font-black text-sm dir-ltr">--:--:-- --</div>
            </div>

          </div>
        </header>

        <!-- تنبيه الخطأ عند ترك الحقول الفارغة -->
        <div id="alertMessage" class="hidden mb-6 bg-red-100 border-r-4 border-red-600 text-red-700 p-4 rounded-lg text-sm font-bold flex items-center gap-2 shadow-sm">
          <i class="fa-solid fa-circle-exclamation text-lg"></i>
          <span>الرجاء ملء اسم الكريم وتفاصيل التقرير أولاً.</span>
        </div>

        <!-- تنبيه النجاح عند الإرسال -->
        <div id="successMessage" class="hidden mb-6 bg-green-100 border-r-4 border-green-600 text-green-700 p-4 rounded-lg text-sm font-bold flex items-center gap-2 shadow-sm">
          <i class="fa-solid fa-circle-check text-lg"></i>
          <span>تم إرسال وحفظ التقرير بنجاح!</span>
        </div>

        <!-- نموذج كتابة التقرير -->
        <form id="reportForm" class="space-y-6">
          
          <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
            
            <!-- حقل اسم الكريم -->
            <div class="bg-white/80 p-2 rounded-lg">
              <label class="block text-sm font-bold text-gray-700 mb-2">
                <i class="fa-solid fa-user text-maroon-700 ml-1"></i> اسم الكريم <span class="text-red-500">*</span>
              </label>
              <input 
                type="text" 
                id="reporterName" 
                placeholder="اكتب اسم الكريم الكامل..."
                class="w-full border border-gray-300 rounded-lg px-4 py-2.5 bg-white/95 focus:ring-2 focus:ring-maroon-700 focus:border-maroon-700 outline-none transition text-sm font-medium"
              />
            </div>

            <!-- حقل رقم الهاتف مع رمـز الدولة -->
            <div class="bg-white/80 p-2 rounded-lg">
              <label class="block text-sm font-bold text-gray-700 mb-2">
                <i class="fa-solid fa-phone text-maroon-700 ml-1"></i> رقم الهاتف
              </label>
              <div class="flex gap-2 dir-ltr">
                <select id="countryCode" class="border border-gray-300 rounded-lg px-2 py-2.5 bg-gray-50 text-xs md:text-sm font-bold text-gray-700 focus:ring-2 focus:ring-maroon-700 outline-none">
                  <option value="+973" selected>🇧🇭 +973</option>
                  <option value="+966">🇸🇦 +966</option>
                  <option value="+964">🇮🇶 +964</option>
                  <option value="+965">🇰🇼 +965</option>
                  <option value="+971">🇦🇪 +971</option>
                  <option value="+968">🇴🇲 +968</option>
                  <option value="+974">🇶🇦 +974</option>
                </select>
                <input 
                  type="tel" 
                  id="phoneNumber" 
                  placeholder="3XXXXXXXX"
                  class="w-full border border-gray-300 rounded-lg px-4 py-2.5 bg-white/95 focus:ring-2 focus:ring-maroon-700 focus:border-maroon-700 outline-none transition text-sm font-medium text-left dir-ltr"
                />
              </div>
            </div>

          </div>

          <!-- حقل تفاصيل التقرير -->
          <div class="bg-white/80 p-2 rounded-lg">
            <label class="block text-sm font-bold text-gray-700 mb-2">
              <i class="fa-solid fa-align-right text-maroon-700 ml-1"></i> تفاصيل التقرير <span class="text-red-500">*</span>
            </label>
            <textarea 
              id="reportDetails" 
              rows="12" 
              placeholder="اكتب تفاصيل وملاحظات التقرير هنا..."
              class="w-full border border-gray-300 rounded-lg p-4 bg-white/95 focus:ring-2 focus:ring-maroon-700 focus:border-maroon-700 outline-none transition text-sm font-medium leading-relaxed"
            ></textarea>
          </div>

        </form>

        <!-- الترويسة السفلية للطباعة -->
        <footer class="mt-8 pt-4 border-t border-gray-200 text-center text-xs text-gray-500 hidden print:block font-bold">
          مضيف أهل العباء — البلاد القديم (مملكة البحرين)
        </footer>

      </div>

    </div>

  </div>

  <!-- الشريط السفلي الثابت للأزرار -->
  <div class="no-print fixed bottom-0 left-0 right-0 bg-white/95 backdrop-blur-md border-t border-gray-200 py-3 px-4 shadow-2xl z-50">
    <div class="max-w-4xl mx-auto flex flex-wrap items-center justify-between gap-3">
      
      <div class="text-xs text-gray-600 font-bold hidden md:flex items-center gap-2">
        <img src="image_be668db9-removebg-preview.png" alt="شعار" class="h-6 w-auto inline">
        مضيف أهل العباء - البلاد القديم
      </div>

      <div class="flex items-center gap-3 w-full md:w-auto justify-end">
        
        <!-- زر التفريغ -->
        <button 
          type="button" 
          onclick="clearForm()"
          class="flex-1 md:flex-none px-4 py-2.5 bg-gray-100 hover:bg-gray-200 text-gray-700 rounded-lg font-bold text-sm transition flex items-center justify-center gap-2"
        >
          <i class="fa-solid fa-trash-can text-red-500"></i> تفريغ الحقول
        </button>

        <!-- زر الإرسال / الحفظ -->
        <button 
          type="button" 
          onclick="submitReport()"
          class="flex-1 md:flex-none px-5 py-2.5 bg-maroon-700 hover:bg-maroon-800 text-white rounded-lg font-bold text-sm transition shadow-md flex items-center justify-center gap-2"
        >
          <i class="fa-solid fa-paper-plane text-gold-400"></i> إرسال التقرير
        </button>

        <!-- زر الطباعة -->
        <button 
          type="button" 
          onclick="printReport()"
          class="flex-1 md:flex-none px-5 py-2.5 bg-gold-500 hover:bg-gold-600 text-white rounded-lg font-bold text-sm transition shadow-md flex items-center justify-center gap-2"
        >
          <i class="fa-solid fa-print"></i> طباعة / PDF
        </button>

      </div>

    </div>
  </div>

  <script>
    // 1. التوقيت والتاريخ التلقائي الحي
    function updateLiveDateTime() {
      const now = new Date();
      const days = ['الأحد', 'الإثنين', 'الثلاثاء', 'الأربعاء', 'الخميس', 'الجمعة', 'السبت'];
      const dayName = days[now.getDay()];

      const day = String(now.getDate()).padStart(2, '0');
      const month = String(now.getMonth() + 1).padStart(2, '0');
      const year = now.getFullYear();

      let hours = now.getHours();
      const minutes = String(now.getMinutes()).padStart(2, '0');
      const seconds = String(now.getSeconds()).padStart(2, '0');
      const ampm = hours >= 12 ? 'م' : 'ص';
      hours = hours % 12 || 12;

      document.getElementById('liveDay').textContent = dayName;
      document.getElementById('liveDate').textContent = `${year}/${month}/${day}`;
      document.getElementById('liveTime').textContent = `${hours}:${minutes}:${seconds} ${ampm}`;
    }

    setInterval(updateLiveDateTime, 1000);
    updateLiveDateTime();

    // 2. التحقق من ملء اسم الكريم وتفاصيل التقرير
    function validateForm() {
      const reporterName = document.getElementById('reporterName');
      const reportDetails = document.getElementById('reportDetails');
      const alertMessage = document.getElementById('alertMessage');
      
      let isValid = true;

      alertMessage.classList.add('hidden');
      reporterName.classList.remove('border-red-500', 'bg-red-50');
      reportDetails.classList.remove('border-red-500', 'bg-red-50');

      if (!reporterName.value.trim()) {
        reporterName.classList.add('border-red-500', 'bg-red-50');
        isValid = false;
      }

      if (!reportDetails.value.trim()) {
        reportDetails.classList.add('border-red-500', 'bg-red-50');
        isValid = false;
      }

      if (!isValid) {
        alertMessage.classList.remove('hidden');
        window.scrollTo({ top: 0, behavior: 'smooth' });
      }

      return isValid;
    }

    // 3. دالة إرسال التقرير
    function submitReport() {
      if (!validateForm()) return;

      const data = {
        name: document.getElementById('reporterName').value,
        countryCode: document.getElementById('countryCode').value,
        phone: document.getElementById('phoneNumber').value,
        details: document.getElementById('reportDetails').value,
        location: 'البلاد القديم - مملكة البحرين',
        date: document.getElementById('liveDate').textContent,
        time: document.getElementById('liveTime').textContent
      };

      localStorage.setItem('ahl_alabaa_bh_report', JSON.stringify(data));
      
      const successMessage = document.getElementById('successMessage');
      successMessage.classList.remove('hidden');
      setTimeout(() => successMessage.classList.add('hidden'), 4000);
    }

    // 4. دالة الطباعة وتصدير PDF
    function printReport() {
      if (!validateForm()) return;
      window.print();
    }

    // 5. دالة التفريغ
    function clearForm() {
      if (confirm('هل أنت متأكد من تفريغ كافة حقول التقرير؟')) {
        document.getElementById('reportForm').reset();
        document.getElementById('alertMessage').classList.add('hidden');
        document.getElementById('reporterName').classList.remove('border-red-500', 'bg-red-50');
        document.getElementById('reportDetails').classList.remove('border-red-500', 'bg-red-50');
      }
    }
  </script>
</body>
</html>
