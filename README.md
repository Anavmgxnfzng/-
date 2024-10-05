<!DOCTYPE html>
<html lang="ar">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>صفحة تريليون كلمة أنا</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 20px;
            line-height: 1.8;
            text-align: justify;
        }

        h1 {
            text-align: center;
        }

        .content {
            margin: 20px auto;
            width: 90%;
            max-width: 1000px;
            background-color: #f4f4f4;
            padding: 20px;
            border-radius: 8px;
            box-shadow: 0px 0px 10px rgba(0, 0, 0, 0.1);
            height: 500px;
            overflow-y: scroll;
        }
    </style>
</head>
<body>

    <h1>تريليون كلمة "أنا"</h1>

    <div class="content" id="content">
        <!-- الكلمات ستظهر هنا مع التمرير -->
    </div>

    <script>
        // التكرار الأولي للكلمات
        let contentDiv = document.getElementById('content');
        let word = "أنا ";
        let batchSize = 10000; // عدد الكلمات التي يتم إضافتها في كل مرة
        let batch = word.repeat(batchSize);

        // إضافة الكلمات الأولى
        contentDiv.innerText = batch;

        // وظيفة لإضافة المزيد من الكلمات عند التمرير
        contentDiv.addEventListener('scroll', function() {
            if (contentDiv.scrollTop + contentDiv.clientHeight >= contentDiv.scrollHeight) {
                contentDiv.innerText += batch; // إضافة دفعة جديدة من الكلمات
            }
        });
    </script>

</body>
</html>