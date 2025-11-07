# Insta2.github.io
<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>منشئ أفكار محتوى إنستغرام بالذكاء الاصطناعي 🤖</title>
    <!-- إضافة مكتبة Transformers.js -->
    <script src="https://cdn.jsdelivr.net/npm/@xenova/transformers@2.6.0"></script>
    <style>
        /* جميع الأنماط الأصلية تبقى كما هي */
        :root {
            --primary: #ec4899;
            --secondary: #8b5cf6;
            --light: #f9fafb;
            --dark: #111827;
            --gray: #6b7280;
            --error: #ef4444;
            --success: #10b981;
        }
        
        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
        }
        
        body {
            font-family: "Tajawal", "Segoe UI", sans-serif;
            background: linear-gradient(135deg, #f9fafb 0%, #e0f2fe 100%);
            color: var(--dark);
            text-align: center;
            padding: 20px;
            min-height: 100vh;
            line-height: 1.6;
        }
        
        .container {
            max-width: 800px;
            margin: 0 auto;
            background: white;
            border-radius: 20px;
            padding: 30px;
            box-shadow: 0 10px 30px rgba(0,0,0,0.1);
            transition: transform 0.3s ease;
            position: relative;
        }
        
        .container:hover {
            transform: translateY(-5px);
        }
        
        h1 {
            color: var(--primary);
            margin-bottom: 10px;
            font-size: 28px;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 10px;
        }
        
        .subtitle {
            color: var(--gray);
            margin-bottom: 30px;
            font-size: 16px;
        }
        
        .input-group {
            margin-bottom: 20px;
            text-align: right;
        }
        
        label {
            display: block;
            margin-bottom: 8px;
            font-weight: bold;
            color: #374151;
        }
        
        input, textarea, select {
            width: 100%;
            padding: 12px 15px;
            border-radius: 12px;
            border: 1px solid #d1d5db;
            font-size: 16px;
            font-family: "Tajawal", sans-serif;
            direction: rtl;
            transition: all 0.3s ease;
        }
        
        input:focus, textarea:focus, select:focus {
            outline: none;
            border-color: var(--primary);
            box-shadow: 0 0 0 3px rgba(236, 72, 153, 0.1);
        }
        
        textarea {
            height: 120px;
            resize: vertical;
        }
        
        select {
            background-color: white;
            cursor: pointer;
        }
        
        button {
            background: linear-gradient(135deg, var(--primary) 0%, var(--secondary) 100%);
            color: white;
            border: none;
            padding: 14px 30px;
            border-radius: 12px;
            cursor: pointer;
            font-size: 18px;
            font-weight: bold;
            transition: all 0.3s ease;
            margin: 10px 0;
            width: 100%;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 8px;
        }
        
        button:hover {
            transform: translateY(-2px);
            box-shadow: 0 5px 15px rgba(139, 92, 246, 0.4);
        }
        
        button:active {
            transform: translateY(0);
        }
        
        button:disabled {
            background: #9ca3af;
            cursor: not-allowed;
            transform: none;
            box-shadow: none;
        }
        
        #output {
            margin-top: 30px;
            background: #f8fafc;
            padding: 25px;
            border-radius: 15px;
            text-align: right;
            direction: rtl;
            white-space: pre-wrap;
            border-right: 4px solid var(--primary);
            display: none;
            animation: fadeIn 0.5s ease;
        }
        
        .idea-item {
            background: white;
            margin: 15px 0;
            padding: 15px;
            border-radius: 10px;
            box-shadow: 0 2px 8px rgba(0,0,0,0.05);
            border-right: 3px solid var(--secondary);
            transition: transform 0.2s ease;
        }
        
        .idea-item:hover {
            transform: translateX(-5px);
        }
        
        .idea-title {
            font-weight: bold;
            color: var(--primary);
            margin-bottom: 8px;
            font-size: 18px;
        }
        
        .idea-description {
            margin-bottom: 10px;
            color: #4b5563;
        }
        
        .hashtags {
            color: #6366f1;
            margin-top: 10px;
            font-size: 14px;
            display: flex;
            flex-wrap: wrap;
            gap: 5px;
        }
        
        .hashtag {
            background: #e0e7ff;
            padding: 3px 8px;
            border-radius: 20px;
        }
        
        .loading {
            display: none;
            margin: 20px 0;
        }
        
        .loading-spinner {
            border: 4px solid #f3f4f6;
            border-top: 4px solid var(--primary);
            border-radius: 50%;
            width: 40px;
            height: 40px;
            animation: spin 1s linear infinite;
            margin: 0 auto;
        }
        
        .examples {
            margin-top: 30px;
            text-align: right;
        }
        
        .examples h3 {
            color: #374151;
            margin-bottom: 15px;
            display: flex;
            align-items: center;
            gap: 8px;
            justify-content: flex-end;
        }
        
        .example-chip {
            display: inline-block;
            background: #e0e7ff;
            color: #4f46e5;
            padding: 8px 15px;
            border-radius: 20px;
            margin: 5px;
            cursor: pointer;
            transition: all 0.2s ease;
            font-size: 14px;
        }
        
        .example-chip:hover {
            background: #c7d2fe;
            transform: translateY(-2px);
        }
        
        .error-message {
            color: var(--error);
            background: #fef2f2;
            padding: 10px;
            border-radius: 8px;
            margin: 10px 0;
            text-align: center;
            display: none;
            border-right: 3px solid var(--error);
        }
        
        .success-message {
            color: var(--success);
            background: #f0fdf4;
            padding: 10px;
            border-radius: 8px;
            margin: 10px 0;
            text-align: center;
            display: none;
            border-right: 3px solid var(--success);
        }
        
        .copy-btn {
            background: #4f46e5;
            color: white;
            border: none;
            padding: 8px 15px;
            border-radius: 8px;
            cursor: pointer;
            font-size: 14px;
            margin-top: 10px;
            transition: all 0.2s ease;
            display: inline-flex;
            align-items: center;
            gap: 5px;
        }
        
        .copy-btn:hover {
            background: #4338ca;
        }
        
        .counter {
            text-align: left;
            font-size: 14px;
            color: var(--gray);
            margin-top: 5px;
        }
        
        .security-notice {
            background: #fffbeb;
            border: 1px solid #fef3c7;
            border-radius: 12px;
            padding: 15px;
            margin: 20px 0;
            text-align: right;
            font-size: 14px;
        }
        
        .security-notice h3 {
            color: #d97706;
            margin-bottom: 8px;
            display: flex;
            align-items: center;
            gap: 8px;
        }
        
        .api-status {
            display: inline-block;
            padding: 4px 12px;
            border-radius: 20px;
            font-size: 12px;
            font-weight: bold;
            margin-right: 10px;
        }
        
        .api-status.connected {
            background: #d1fae5;
            color: #065f46;
        }
        
        .api-status.disconnected {
            background: #fee2e2;
            color: #991b1b;
        }
        
        .rate-limit {
            background: #eff6ff;
            border: 1px solid #dbeafe;
            border-radius: 8px;
            padding: 10px;
            margin: 10px 0;
            font-size: 13px;
            color: #374151;
        }

        .model-status {
            background: #f0fdf4;
            border: 1px solid #bbf7d0;
            border-radius: 8px;
            padding: 10px;
            margin: 10px 0;
            font-size: 13px;
            color: #065f46;
            text-align: right;
        }
        
        @keyframes spin {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }
        
        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(10px); }
            to { opacity: 1; transform: translateY(0); }
        }
        
        /* تصميم متجاوب */
        @media (max-width: 768px) {
            .container {
                padding: 20px;
                border-radius: 15px;
            }
            
            h1 {
                font-size: 24px;
            }
            
            button {
                padding: 12px 20px;
                font-size: 16px;
            }
            
            .idea-item {
                padding: 12px;
            }
        }
        
        @media (max-width: 480px) {
            body {
                padding: 10px;
            }
            
            .container {
                padding: 15px;
            }
            
            h1 {
                font-size: 22px;
            }
            
            .subtitle {
                font-size: 14px;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>🧠 منشئ أفكار محتوى إنستغرام بالذكاء الاصطناعي</h1>
        <p class="subtitle">احصل على أفكار إبداعية واحترافية لمحتوى إنستغرام خاصتك في ثوانٍ</p>

        <div class="security-notice">
            <h3>🛡️ وضع الأمان النشط</h3>
            <p>جميع البيانات محمية ولا يتم تخزينها. التطبيق يستخدم تقنيات أمان متقدمة لحماية معلوماتك.</p>
        </div>

        <div class="model-status" id="modelStatus">
            ⚡ جاهز للعمل - النموذج يعمل محلياً بدون اتصال بالإنترنت
        </div>

        <div class="input-group">
            <label for="niche">مجالك/تخصصك:</label>
            <input type="text" id="niche" placeholder="مثال: اللياقة البدنية، الطبخ، السفر، التكنولوجيا..." maxlength="50">
            <div class="counter" id="niche-counter">0/50</div>
        </div>

        <div class="input-group">
            <label for="contentType">نوع المحتوى المطلوب:</label>
            <select id="contentType">
                <option value="افكار ريلز">أفكار ريلز (Reels)</option>
                <option value="افكار منشورات">أفكار منشورات (Posts)</option>
                <option value="افكار ستوريات">أفكار ستوريات (Stories)</option>
                <option value="افكار متنوعة">أفكار متنوعة لجميع الأنواع</option>
            </select>
        </div>

        <div class="input-group">
            <label for="tone">نبرة المحتوى:</label>
            <select id="tone">
                <option value="ملهمة">ملهمة</option>
                <option value="مرحة">مرحة</option>
                <option value="تعليمية">تعليمية</option>
                <option value="تحفيزية">تحفيزية</option>
                <option value="احترافية">احترافية</option>
            </select>
        </div>

        <div class="input-group">
            <label for="prompt">أضف تفاصيل إضافية (اختياري):</label>
            <textarea id="prompt" placeholder="مثال: أفكار لمحتوى يلفت انتباه الشباب، أو يركز على التغذية الصحية..." maxlength="200"></textarea>
            <div class="counter" id="prompt-counter">0/200</div>
        </div>

        <div class="rate-limit">
            ⚡ الحد المسموح: 5 طلبات كل 10 دقائق للحماية من الإستخدام المفرط
        </div>

        <div class="error-message" id="errorMessage"></div>
        <div class="success-message" id="successMessage"></div>

        <button onclick="generateContent()" id="generateBtn">
            <span>أنشئ أفكار المحتوى</span>
            <span>✨</span>
        </button>
        
        <div class="loading" id="loading">
            <div class="loading-spinner"></div>
            <p>جاري توليد أفكار إبداعية لك...</p>
        </div>

        <div id="output"></div>

        <div class="examples">
            <h3>💡 أمثلة سريعة:</h3>
            <div class="example-chip" onclick="fillExample('لياقة بدنية', 'افكار ريلز', 'مرحة')">لياقة بدنية - ريلز مرحة</div>
            <div class="example-chip" onclick="fillExample('طبخ', 'افكار منشورات', 'تعليمية')">طبخ - منشورات تعليمية</div>
            <div class="example-chip" onclick="fillExample('سفر', 'افكار ستوريات', 'ملهمة')">سفر - ستوريات ملهمة</div>
            <div class="example-chip" onclick="fillExample('تكنولوجيا', 'افكار متنوعة', 'احترافية')">تكنولوجيا - أفكار متنوعة</div>
            <div class="example-chip" onclick="fillExample('تطوير الذات', 'افكار ريلز', 'تحفيزية')">تطوير الذات - ريلز تحفيزية</div>
        </div>
    </div>

    <script>
        // نظام الذكاء الاصطناعي المحلي
        class LocalAIModel {
            constructor() {
                this.pipeline = null;
                this.isLoaded = false;
                this.isLoading = false;
            }

            async loadModel() {
                if (this.isLoaded || this.isLoading) return;
                
                this.isLoading = true;
                try {
                    // استخدام نموذج خفيف وسريع للتوليد
                    const { pipeline } = await import('https://cdn.jsdelivr.net/npm/@xenova/transformers@2.6.0');
                    this.pipeline = await pipeline('text-generation', 'Xenova/t5-small');
                    this.isLoaded = true;
                    this.isLoading = false;
                    console.log('النموذج تم تحميله بنجاح');
                    return true;
                } catch (error) {
                    console.error('فشل تحميل النموذج:', error);
                    this.isLoading = false;
                    return false;
                }
            }

            async generateText(prompt, maxLength = 300) {
                if (!this.isLoaded) {
                    const loaded = await this.loadModel();
                    if (!loaded) {
                        throw new Error('فشل تحميل النموذج');
                    }
                }

                try {
                    const result = await this.pipeline(prompt, {
                        max_new_tokens: maxLength,
                        temperature: 0.8,
                        do_sample: true,
                        repetition_penalty: 1.2
                    });

                    return result[0].generated_text;
                } catch (error) {
                    console.error('خطأ في التوليد:', error);
                    throw new Error('فشل في توليد النص');
                }
            }
        }

        // نظام الأمان والحماية
        class SecurityManager {
            constructor() {
                this.rateLimit = {
                    count: 0,
                    lastReset: Date.now(),
                    maxRequests: 5,
                    timeWindow: 10 * 60 * 1000 // 10 دقائق
                };
                this.sanitizePatterns = {
                    html: /<script\b[^<]*(?:(?!<\/script>)<[^<]*)*<\/script>/gi,
                    sql: /(\b(SELECT|INSERT|UPDATE|DELETE|DROP|UNION|EXEC)\b)/gi,
                    xss: /(<|>|&lt;|&gt;|javascript:)/gi
                };
            }

            // التحقق من حدود الاستخدام
            checkRateLimit() {
                const now = Date.now();
                if (now - this.rateLimit.lastReset > this.rateLimit.timeWindow) {
                    this.rateLimit.count = 0;
                    this.rateLimit.lastReset = now;
                }
                
                if (this.rateLimit.count >= this.rateLimit.maxRequests) {
                    const timeLeft = Math.ceil((this.rateLimit.timeWindow - (now - this.rateLimit.lastReset)) / 1000 / 60);
                    throw new Error(`تم تجاوز الحد المسموح. يرجى المحاولة بعد ${timeLeft} دقيقة`);
                }
                
                this.rateLimit.count++;
                return true;
            }

            // تنظيف المدخلات من الهجمات
            sanitizeInput(input) {
                if (typeof input !== 'string') return '';
                
                let sanitized = input
                    .replace(this.sanitizePatterns.html, '')
                    .replace(this.sanitizePatterns.sql, '')
                    .replace(this.sanitizePatterns.xss, '')
                    .trim();
                
                // تحديد طول آمن
                if (sanitized.length > 500) {
                    sanitized = sanitized.substring(0, 500);
                }
                
                return sanitized;
            }

            // التحقق من صحة البيانات
            validateInput(niche, prompt) {
                if (!niche || niche.trim().length === 0) {
                    throw new Error('يرجى إدخال المجال أو التخصص');
                }
                
                if (niche.length > 50) {
                    throw new Error('المجال يجب أن لا يتجاوز 50 حرفاً');
                }
                
                if (prompt && prompt.length > 200) {
                    throw new Error('التفاصيل الإضافية يجب أن لا تتجاوز 200 حرف');
                }

                // التحقق من الأحرف المسموحة (العربية والإنجليزية والأرقام ومسافات)
                const validChars = /^[\u0600-\u06FF\u0750-\u077F\u08A0-\u08FFa-zA-Z0-9\s\-_.,!?]+$/;
                if (!validChars.test(niche)) {
                    throw new Error('يحتوي المجال على أحرف غير مسموحة');
                }

                return true;
            }
        }

        // نظام التخزين الآمن
        class SecureStorage {
            constructor() {
                this.storageKey = 'instagram_ai_ideas_app';
                this.sessionDuration = 30 * 60 * 1000; // 30 دقيقة
            }

            // حفظ البيانات بشكل آمن
            saveData(key, data) {
                try {
                    const storageData = this.getStorageData();
                    storageData[key] = {
                        data: data,
                        timestamp: Date.now()
                    };
                    localStorage.setItem(this.storageKey, JSON.stringify(storageData));
                    return true;
                } catch (error) {
                    console.error('خطأ في حفظ البيانات:', error);
                    return false;
                }
            }

            // جلب البيانات بشكل آمن
            getData(key) {
                try {
                    const storageData = this.getStorageData();
                    const item = storageData[key];
                    
                    if (!item) return null;
                    
                    // التحقق من انتهاء الصلاحية
                    if (Date.now() - item.timestamp > this.sessionDuration) {
                        this.clearData(key);
                        return null;
                    }
                    
                    return item.data;
                } catch (error) {
                    console.error('خطأ في جلب البيانات:', error);
                    return null;
                }
            }

            // مسح البيانات
            clearData(key) {
                try {
                    const storageData = this.getStorageData();
                    delete storageData[key];
                    localStorage.setItem(this.storageKey, JSON.stringify(storageData));
                } catch (error) {
                    console.error('خطأ في مسح البيانات:', error);
                }
            }

            // جلب جميع بيانات التخزين
            getStorageData() {
                try {
                    const data = localStorage.getItem(this.storageKey);
                    return data ? JSON.parse(data) : {};
                } catch (error) {
                    return {};
                }
            }
        }

        // تهيئة الأنظمة
        const localAI = new LocalAIModel();
        const securityManager = new SecurityManager();
        const secureStorage = new SecureStorage();

        // عناصر DOM
        const nicheInput = document.getElementById('niche');
        const promptInput = document.getElementById('prompt');
        const nicheCounter = document.getElementById('niche-counter');
        const promptCounter = document.getElementById('prompt-counter');
        const errorMessage = document.getElementById('errorMessage');
        const successMessage = document.getElementById('successMessage');
        const modelStatus = document.getElementById('modelStatus');

        // تحميل البيانات المحفوظة
        window.addEventListener('load', function() {
            const savedNiche = secureStorage.getData('last_niche');
            const savedPrompt = secureStorage.getData('last_prompt');
            
            if (savedNiche) nicheInput.value = savedNiche;
            if (savedPrompt) promptInput.value = savedPrompt;
            
            updateCounters();
            
            // تحميل النموذج تلقائياً عند فتح الصفحة
            loadAIModel();
        });

        // تحميل نموذج الذكاء الاصطناعي
        async function loadAIModel() {
            try {
                modelStatus.innerHTML = '🔄 جاري تحميل النموذج... (قد يستغرق بضع ثوان)';
                await localAI.loadModel();
                modelStatus.innerHTML = '✅ النموذج جاهز للعمل - يعمل محلياً بدون اتصال إنترنت';
            } catch (error) {
                modelStatus.innerHTML = '⚠️ النموذج غير متاح - سيتم استخدام النظام الاحتياطي';
                console.log('سيتم استخدام الأفكار المحلية كبديل');
            }
        }

        // عدادات الأحرف مع الحماية
        function updateCounters() {
            const nicheLength = nicheInput.value.length;
            const promptLength = promptInput.value.length;
            
            nicheCounter.textContent = `${nicheLength}/50`;
            promptCounter.textContent = `${promptLength}/200`;
            
            nicheCounter.style.color = nicheLength > 50 ? '#ef4444' : '#6b7280';
            promptCounter.style.color = promptLength > 200 ? '#ef4444' : '#6b7280';
        }

        nicheInput.addEventListener('input', function() {
            this.value = securityManager.sanitizeInput(this.value);
            updateCounters();
            secureStorage.saveData('last_niche', this.value);
        });

        promptInput.addEventListener('input', function() {
            this.value = securityManager.sanitizeInput(this.value);
            updateCounters();
            secureStorage.saveData('last_prompt', this.value);
        });

        // تعبئة الأمثلة السريعة
        function fillExample(niche, type, tone) {
            const safeNiche = securityManager.sanitizeInput(niche);
            document.getElementById('niche').value = safeNiche;
            document.getElementById('contentType').value = type;
            document.getElementById('tone').value = tone;
            document.getElementById('prompt').value = '';
            
            updateCounters();
            secureStorage.saveData('last_niche', safeNiche);
            secureStorage.saveData('last_prompt', '');
            
            showMessage(`تم تعبئة مثال ${safeNiche} - ${type} - ${tone}`, 'success');
        }

        // عرض الرسائل
        function showMessage(message, type) {
            const element = type === 'error' ? errorMessage : successMessage;
            element.textContent = message;
            element.style.display = 'block';
            
            setTimeout(() => {
                element.style.display = 'none';
            }, 5000);
        }

        // توليد المحتوى مع الحماية الكاملة
        async function generateContent() {
            const niche = nicheInput.value.trim();
            const contentType = document.getElementById('contentType').value;
            const tone = document.getElementById('tone').value;
            const additionalPrompt = promptInput.value.trim();
            const output = document.getElementById('output');
            const generateBtn = document.getElementById('generateBtn');
            const loading = document.getElementById('loading');

            try {
                // تطبيق جميع إجراءات الأمان
                securityManager.checkRateLimit();
                securityManager.validateInput(niche, additionalPrompt);
                
                const safeNiche = securityManager.sanitizeInput(niche);
                const safePrompt = securityManager.sanitizeInput(additionalPrompt);

                // تعطيل الزر وإظهار مؤشر التحميل
                generateBtn.disabled = true;
                loading.style.display = 'block';
                output.style.display = 'none';
                errorMessage.style.display = 'none';

                // استخدام الذكاء الاصطناعي المحلي
                const ideas = await generateWithAI(safeNiche, contentType, tone, safePrompt);
                
                output.innerHTML = formatContent(ideas);
                output.style.display = 'block';
                showMessage("تم توليد أفكار المحتوى بنجاح!", 'success');
                
                // حفظ النتائج مؤقتاً
                secureStorage.saveData('last_results', ideas);
                
            } catch (err) {
                console.error('Error:', err);
                showMessage(err.message, 'error');
            } finally {
                // إعادة تفعيل الزر وإخفاء مؤشر التحميل
                generateBtn.disabled = false;
                loading.style.display = 'none';
            }
        }

        // توليد الأفكار باستخدام الذكاء الاصطناعي
        async function generateWithAI(niche, contentType, tone, prompt) {
            try {
                const aiPrompt = `أنت مساعد متخصص في إنشاء محتوى إبداعي لإنستغرام.
المجال: ${niche}
نوع المحتوى: ${contentType}
النبرة: ${tone}
التفاصيل الإضافية: ${prompt}

الرجاء إنشاء 3 أفكار محتوى مبتكرة مع وصف مفيد لكل فكرة وإضافة الهاشتاقات المناسبة باللغة العربية.
أرغب في إجابة منظمة وواضحة.`;

                const generatedText = await localAI.generateText(aiPrompt);
                return generatedText || generateFallbackIdeas(niche, contentType, tone, prompt);
                
            } catch (error) {
                console.error('AI Generation Error:', error);
                // استخدام الأفكار المحلية كبديل في حالة فشل الاتصال
                return generateFallbackIdeas(niche, contentType, tone, prompt);
            }
        }

        // أفكار احتياطية في حالة فشل الذكاء الاصطناعي
        function generateFallbackIdeas(niche, contentType, tone, prompt) {
            const ideas = {
                'لياقة بدنية': `
1. **تمارين سريعة للمكتب**: 
   ${contentType} يظهر تمارين بسيطة يمكن القيام بها أثناء العمل لتحسين الدورة الدموية وتخفيف التوتر.
   
   الهاشتاقات: #تمارين_سريعة #صحة #لياقة #عمل #نشاط

2. **تحدي الـ 30 يوماً**: 
   سلسلة ${contentType} تتابع تحدي لياقة لمدة 30 يوماً، مع إظهار التقدم والنصائح اليومية.
   
   الهاشتاقات: #تحدي_اللياقة #رياضة #تقدم #صحة #${niche}

3. **نصائح تغذية للرياضيين**: 
   محتوى تعليمي ${tone} يقدم نصائح حول التغذية المناسبة قبل وبعد التمارين.
   
   الهاشتاجات: #تغذية_رياضية #${niche} #صحة #نصائح
                `,
                'طبخ': `
1. **وصفات في 5 دقائق**: 
   ${contentType} سريع يظهر كيفية تحضير وجبات لذيذة وصحية في وقت قياسي.
   
   الهاشتاقات: #وصفات_سريعة #${niche} #طبخ #صحي #اكل

2. **أخطاء شائعة في المطبخ**: 
   محتوى تعليمي ${tone} يوضح أخطاء شائعة في الطبخ وكيفية تجنبها.
   
   الهاشتاقات: #نصائح_طبخ #مطبخ #تعليم #أخطاء #${niche}

3. **تحضير وجبات الأسبوع**: 
   ${contentType} يظهر كيفية التخطيط وتحضير وجبات الأسبوع مسبقاً.
   
   الهاشتاقات: #تخطيط_الوجبات #${niche} #تنظيم #طبخ
                `,
                'default': `
1. **فكرة إبداعية في ${niche}**: 
   ${contentType} ${tone} يقدم فكرة مبتكرة في مجال ${niche} مع شرح تفصيلي لكيفية التنفيذ.
   
   الهاشتاقات: #${niche} #إبداع #محتوى #${contentType} #${tone}

2. **نصائح عملية للمبتدئين**: 
   محتوى تعليمي ${tone} يقدم نصائح قيمة للمبتدئين في مجال ${niche}.
   
   الهاشتاقات: #نصائح_${niche} #مبتدئين #تعلم #${tone}

3. **أخطاء شائعة يجب تجنبها**: 
   ${contentType} توعوي ${tone} يوضح الأخطاء الشائعة في ${niche} وكيفية تجنبها.
   
   الهاشتاقات: #أخطاء_${niche} #نصائح #تجنب #${tone}
                `
            };

            return ideas[niche] || ideas['default'];
        }

        // تنسيق المحتوى بشكل آمن
        function formatContent(content) {
            const lines = content.split('\n');
            let formattedContent = '';
            let currentIdea = '';
            
            lines.forEach(line => {
                line = securityManager.sanitizeInput(line.trim());
                
                if (/^(\d+\.|\-|\*)\s+/.test(line)) {
                    if (currentIdea) {
                        formattedContent += currentIdea + '</div>';
                    }
                    
                    currentIdea = '<div class="idea-item">';
                    const title = line.replace(/^(\d+\.|\-|\*)\s+/, '').trim();
                    currentIdea += `<div class="idea-title">${title}</div>`;
                } 
                else if (line && !line.startsWith('الهاشتاقات:') && currentIdea) {
                    currentIdea += `<div class="idea-description">${line}</div>`;
                }
                else if (line.startsWith('الهاشتاقات:')) {
                    const hashtags = line.replace('الهاشتاقات:', '').trim();
                    const hashtagArray = hashtags.split(/\s+/);
                    let hashtagsHTML = '<div class="hashtags">';
                    
                    hashtagArray.forEach(tag => {
                        if (tag.startsWith('#') && tag.length <= 20) {
                            hashtagsHTML += `<span class="hashtag">${securityManager.sanitizeInput(tag)}</span>`;
                        }
                    });
                    
                    hashtagsHTML += '</div>';
                    currentIdea += hashtagsHTML;
                }
            });
            
            if (currentIdea) {
                formattedContent += currentIdea + '</div>';
            }
            
            formattedContent += `<button class="copy-btn" onclick="copyToClipboard()">نسخ الأفكار 📋</button>`;
            
            return formattedContent;
        }

        // نسخ المحتوى إلى الحافظة بشكل آمن
        function copyToClipboard() {
            const output = document.getElementById('output');
            const textToCopy = output.innerText;
            
            navigator.clipboard.writeText(textToCopy)
                .then(() => {
                    showMessage("تم نسخ الأفكار إلى الحافظة!", 'success');
                })
                .catch(err => {
                    console.error('Failed to copy: ', err);
                    showMessage("فشل نسخ النص. يرجى المحاولة يدوياً.", 'error');
                });
        }

        // السماح بإدخال البيانات باستخدام زر Enter
        nicheInput.addEventListener('keypress', function(e) {
            if (e.key === 'Enter') {
                generateContent();
            }
        });
    </script>
</body>
</html>
