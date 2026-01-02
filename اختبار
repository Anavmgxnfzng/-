<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>اختبار العلوم والمراجعة الشاملة</title>
    <style>
        body { font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif; background-color: #f0f2f5; margin: 0; padding: 20px; }
        .container { max-width: 800px; margin: auto; background: white; padding: 30px; border-radius: 15px; box-shadow: 0 4px 15px rgba(0,0,0,0.1); }
        h1 { text-align: center; color: #2c3e50; border-bottom: 2px solid #3498db; padding-bottom: 10px; }
        .question-block { margin-bottom: 25px; padding: 15px; border-bottom: 1px solid #eee; }
        .question-text { font-weight: bold; font-size: 1.1em; margin-bottom: 10px; color: #34495e; }
        .options { display: flex; flex-direction: column; gap: 8px; }
        .option { padding: 10px; border: 1px solid #ddd; border-radius: 5px; cursor: pointer; transition: 0.3s; }
        .option:hover { background-color: #f8f9fa; }
        input[type="radio"] { margin-left: 10px; }
        
        button#submit-btn { width: 100%; padding: 15px; background-color: #27ae60; color: white; border: none; border-radius: 8px; font-size: 1.2em; cursor: pointer; margin-top: 20px; }
        button#submit-btn:hover { background-color: #219150; }
        
        #result { margin-top: 30px; display: none; padding: 20px; border-radius: 10px; text-align: center; font-size: 1.5em; }
        
        /* ألوان التصحيح */
        .correct-answer { background-color: #d4edda !important; border-color: #28a745 !important; color: #155724; font-weight: bold; }
        .wrong-answer { background-color: #f8d7da !important; border-color: #dc3545 !important; color: #721c24; }
    </style>
</head>
<body>

<div class="container">
    <h1>اختبار المراجعة الشاملة (40 سؤال)</h1>
    <form id="quiz-form">
        <div id="questions-container"></div>
        <button type="button" id="submit-btn" onclick="checkAnswers()">إرسال ومعرفة النتيجة</button>
    </form>

    <div id="result"></div>
</div>

<script>
    const quizData = [
        { q: "الكون هو ذلك الفضاء الشاسع الذي يحتوي على أعداد ضخمة من المجرات.", options: ["المجموعة الشمسية", "الكون", "الثقب الأسود"], correct: 1 },
        { q: "علم الفلك هو ذلك العلم الذي يهتم بدراسة الأجرام السماوية.", options: ["علم الفلك", "علم الجيولوجيا", "علم الأحياء"], correct: 0 },
        { q: "علم الفيزياء الفلكية هو العلم الذي يستخدم قوانين الفيزياء مثل الجاذبية والمسافة.", options: ["الكيمياء الكونية", "علم الفيزياء الفلكية", "الأرصاد الجوية"], correct: 1 },
        { q: "من مراحل تطور الكون المرحلة الأولى حيث القوى الطبيعية متحدة.", options: ["مراحل تطور الكون الأولى", "مرحلة الانفجار العظيم", "مرحلة تشكل النجوم"], correct: 0 },
        { q: "العالم الذي اكتشف أن الكون ليس ثابتاً وإنما يتمدد ببطء.", options: ["نيوتن", "أينشتاين", "إدوين هابل"], correct: 2 },
        { q: "الطاقة المظلمة هي طاقة خفية مجهولة المصدر تشكل حوالي 65% من الكون.", options: ["الطاقة الشمسية", "الطاقة المظلمة", "الطاقة الحركية"], correct: 1 },
        { q: "توازن قوة الضغط والجاذبية ليصبح النجم مستقراً.", options: ["الانصهار النووي", "التوازن الهيدروستاتيكي", "الثقالة"], correct: 1 },
        { q: "إذا كان لون النجم (أحمر) فهذا يدل على أن النجم...", options: ["أكثر سخونة", "أقل سخونة", "متوسط الحرارة"], correct: 1 },
        { q: "النجم عبارة عن جسم غازي متألق تتولد الطاقة في باطنه ويشع منه الضوء.", options: ["الكوكب", "القوة", "النجم"], correct: 2 },
        { q: "النجوم المزدوجة عبارة عن نجمين مرتبطين مع بعضهما بفعل الجاذبية.", options: ["النجوم المزدوجة", "المجرات الحلزونية", "النيازك"], correct: 0 },
        { q: "المستعر الأعظم هو انفجار نجمي يحدث في نهاية حياة النجم.", options: ["السديم", "المستعر الأعظم", "الشهاب"], correct: 1 },
        { q: "المجرة عبارة عن مجموعة هائلة من النجوم والغاز والغبار مرتبطة مع بعض.", options: ["المجموعة الشمسية", "الكويكبات", "المجرة"], correct: 2 },
        { q: "توجد (مجرة درب التبانة) من بين المجرات...", options: ["البيضاوية", "الحلزونية", "غير المنتظمة"], correct: 1 },
        { q: "المجرات البيضاوية تكون على شكل كروي أو بيضاوي وتكثر بها النجوم القديمة.", options: ["المجرات البيضاوية", "المجرات الحلزونية", "المجرات القزمة"], correct: 0 },
        { q: "المركبات الفضائية هي أنظمة مصممة ومبنية في الفضاء الخارجي.", options: ["الكواكب الصناعية", "المركبات الفضائية", "التلسكوبات"], correct: 1 },
        { q: "المدار الأرضي المنخفض هو مدار قريب من سطح الأرض ويقع على ارتفاع أقل من 2000 كم.", options: ["المدار العالي", "المدار المتوسط", "المدار الأرضي المنخفض"], correct: 2 },
        { q: "جميع الأقمار الصناعية تستخدم في الاتصالات، والقنوات الفضائية، ومراقبة الخرائط.", options: ["الرادارات", "الأقمار الصناعية", "الطائرات"], correct: 1 },
        { q: "المركبات الفضائية المأهولة هي مركبات يقودها رواد الفضاء للتجارب والعودة للأرض.", options: ["المسبار الفضائي", "المركبات الفضائية المأهولة", "الصواريخ"], correct: 1 },
        { q: "أول رائد فضاء عربي مسلم هو الأمير سلطان بن سلمان.", options: ["عباس بن فرناس", "الأمير سلطان بن سلمان", "هزاع المنصوري"], correct: 1 },
        { q: "أول رائدة فضاء سعودية هي الأستاذة ريانة برناوي.", options: ["ريانة برناوي", "مشاعل الشميمري", "هنادي هندي"], correct: 0 },
        // الجزء الثاني من الصور
        { q: "المعدن هو عنصر أو مركب كيميائي موجود في الأرض، وفي حالة صلبة وشكل بلوري ثابت.", options: ["الصخر", "المعدن", "الزجاج"], correct: 1 },
        { q: "يوجد في القشرة الأرضية حوالي كم معدن؟", options: ["1000 معدن", "2000 معدن", "3000 معدن"], correct: 2 },
        { q: "البلورة هي بناء هندسي صلب تترتب فيه الذرات بشكل متكرر ومنتظم.", options: ["البلورة", "السبيكة", "الذرة"], correct: 0 },
        { q: "صلابة المعدن هي قدرة المعدن على مقاومة الخدش.", options: ["اللمعان", "صلابة المعدن", "اللون"], correct: 1 },
        { q: "اللمعان في المعدن هو انعكاس الضوء على سطح المعدن.", options: ["القساوة", "اللمعان", "الانكسار"], correct: 1 },
        { q: "اليورانيوم من المعادن المهمة في إنتاج الطاقة النووية.", options: ["الحديد", "اليورانيوم", "الذهب"], correct: 1 },
        { q: "الصخور النارية هي التي تكونت نتيجة تبريد الصهارة وتصلبها.", options: ["الصخور النارية", "الصخور الرسوبية", "الصخور المتحولة"], correct: 0 },
        { q: "الصهارة عبارة عن صخور وغازات مذابة ومصهورة تحت سطح الأرض.", options: ["اللابة", "الصهارة", "البراكين"], correct: 1 },
        { q: "من مميزات الصخور النارية أنها صلبة وقوية ولا تحتوي على...", options: ["معادن", "بلورات", "أحافير"], correct: 2 },
        { q: "الصخور الرسوبية هي التي تكونت من تراكم وترسيب فتات الصخور وتماسكها.", options: ["الصخور الرسوبية", "الصخور النارية", "الصخور الرخامية"], correct: 0 },
        { q: "من مميزات الصخور الرسوبية أنها تحتوي على النفط والغاز و...", options: ["الذهب", "الأحافير", "اليورانيوم"], correct: 1 },
        { q: "العالم (ألفريد فاجنر) هو أول من اقترح فكرة حركة القارات.", options: ["إدوين هابل", "ألفريد فاجنر", "نيوتن"], correct: 1 },
        { q: "كانت القارات مجتمعة في كتلة واحدة تسمى (بانجيا) قبل كم سنة؟", options: ["100 مليون", "200 مليون", "500 مليون"], correct: 1 },
        { q: "(السونار) هو جهاز يستخدم الموجات الصوتية لتحديد المسافة والعمق.", options: ["الرادار", "السونار", "المجهر"], correct: 1 },
        { q: "(ظهر المحيط) هو أطول سلسلة جبلية على كوكب الأرض وتكون تحت الماء.", options: ["جبال الأنديز", "جبال الهيمالايا", "ظهر المحيط"], correct: 2 },
        { q: "(البركان) هو جميع العمليات المصاحبة لخروج الصهارة والسوائل والغازات.", options: ["الزلزال", "البركان", "التعرية"], correct: 1 },
        { q: "(قناة البركان) هو تركيب يشبه الأنبوب لدفع الصهارة من حجرة الصهير.", options: ["الفوهة", "قناة البركان", "المدخنة"], correct: 1 },
        { q: "(البراكين الدرعية) يكون حجمها ضخم وثوراتها هادئة وشكلها قليل الانحدار.", options: ["البراكين الدرعية", "البراكين المخروطية", "البراكين المركبة"], correct: 0 },
        { q: "(البراكين المخروطية) يكون حجمها صغير وثوراتها عنيفة وشكلها شديد الانحدار.", options: ["البراكين الدرعية", "البراكين المخروطية", "البراكين الخامدة"], correct: 1 },
        { q: "إذا كانت السيليكا واللزوجة والغازات (عالية) كان الانفجار...", options: ["ضعيفاً", "شديداً وقوياً", "معدوماً"], correct: 1 }
    ];

    const container = document.getElementById('questions-container');

    quizData.forEach((data, index) => {
        const div = document.createElement('div');
        div.className = 'question-block';
        div.innerHTML = `
            <div class="question-text">${index + 1}. ${data.q}</div>
            <div class="options">
                ${data.options.map((opt, i) => `
                    <label class="option" id="q${index}o${i}">
                        <input type="radio" name="q${index}" value="${i}"> ${opt}
                    </label>
                `).join('')}
            </div>
        `;
        container.appendChild(div);
    });

    function checkAnswers() {
        let score = 0;
        quizData.forEach((data, index) => {
            const selected = document.querySelector(`input[name="q${index}"]:checked`);
            const correctOptionId = `q${index}o${data.correct}`;
            
            // تلوين الإجابة الصحيحة دائماً بالأخضر
            document.getElementById(correctOptionId).classList.add('correct-answer');

            if (selected) {
                const selectedValue = parseInt(selected.value);
                if (selectedValue === data.correct) {
                    score++;
                } else {
                    // تلوين الإجابة الخاطئة المحددة بالأحمر
                    document.getElementById(`q${index}o${selectedValue}`).classList.add('wrong-answer');
                }
            }
        });

        const resultDiv = document.getElementById('result');
        resultDiv.style.display = 'block';
        resultDiv.innerHTML = `درجتك هي: ${score} من 40 <br> <small>تم تحديد الإجابات الصحيحة بالأخضر والخاطئة بالأحمر</small>`;
        resultDiv.style.backgroundColor = score >= 20 ? '#d4edda' : '#f8d7da';
        resultDiv.style.color = score >= 20 ? '#155724' : '#721c24';
        
        window.scrollTo(0, document.body.scrollHeight);
    }
</script>

</body>
</html>
