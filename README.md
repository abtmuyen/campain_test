# campain_test
<!DOCTYPE html>
<html lang="vi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Trắc Nghiệm Tết: Bạn Là "Hệ" Gì?</title>
    <style>
        :root {
            --primary-red: #d32f2f;
            --gold: #ffd700;
            --bg: #fff5f5;
        }
        body { font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif; background: var(--bg); display: flex; justify-content: center; align-items: center; min-height: 100vh; margin: 0; }
        #quiz-container { background: white; width: 90%; max-width: 500px; padding: 20px; border-radius: 20px; box-shadow: 0 10px 30px rgba(0,0,0,0.1); border: 2px solid var(--primary-red); }
        .question { font-size: 1.2rem; font-weight: bold; margin-bottom: 20px; color: var(--primary-red); }
        .options button { display: block; width: 100%; padding: 15px; margin-bottom: 10px; border: 1px solid #ddd; border-radius: 10px; background: white; cursor: pointer; transition: 0.3s; text-align: left; }
        .options button:hover { background: var(--primary-red); color: white; }
        #result { display: none; text-align: center; }
        .result-card { background: linear-gradient(135deg, var(--primary-red), #b71c1c); color: white; padding: 20px; border-radius: 15px; margin-top: 20px; }
        .hidden { display: none; }
    </style>
</head>
<body>

<div id="quiz-container">
    <div id="start-screen">
        <h2 style="color: var(--primary-red);">Tết Này Bạn Là "Hệ" Gì?</h2>
        <p>Khám phá bản thân để nhận "lì xì" phù hợp từ dự án!</p>
        <button onclick="startQuiz()" style="background: var(--primary-red); color: white; padding: 15px 30px; border: none; border-radius: 50px; cursor: pointer; font-weight: bold;">BẮT ĐẦU TEST</button>
    </div>

    <div id="quiz-screen" class="hidden">
        <div id="progress" style="font-size: 0.8rem; color: gray; margin-bottom: 10px;"></div>
        <div class="question" id="question-text"></div>
        <div class="options" id="options-container"></div>
    </div>

    <div id="result">
        <h2>Kết quả của bạn là...</h2>
        <div class="result-card">
            <h1 id="character-name"></h1>
            <p id="character-desc"></p>
        </div>
        <button onclick="location.reload()" style="margin-top: 20px; border: none; background: none; color: var(--primary-red); cursor: pointer; text-decoration: underline;">Làm lại bài test</button>
    </div>
</div>

<script>
    const questions = [
        {
            q: "Sáng mùng 1, việc đầu tiên bạn làm là gì?",
            options: [
                { text: "Mở app kiểm tra đơn hàng/tin nhắn", type: "Seller" },
                { text: "Ngủ tiếp, deadline tính sau", type: "Student_Chill" },
                { text: "Lên đồ đi chụp ảnh sống ảo", type: "Student_GenZ" }
            ]
        },
        {
            q: "Thấy trend 'Ăn nho gầm bàn', bạn nghĩ gì?",
            options: [
                { text: "Chui xuống gầm bàn livestream bán nho", type: "Seller" },
                { text: "Chui xuống cầu hết nợ môn", type: "Student_Chill" },
                { text: "Quay TikTok bắt trend ngay và luôn", type: "Student_GenZ" }
            ]
        }
    ];

    let currentIdx = 0;
    let scores = { Seller: 0, Student_Chill: 0, Student_GenZ: 0 };

    function startQuiz() {
        document.getElementById('start-screen').classList.add('hidden');
        document.getElementById('quiz-screen').classList.remove('hidden');
        showQuestion();
    }

    function showQuestion() {
        const q = questions[currentIdx];
        document.getElementById('progress').innerText = `Câu hỏi ${currentIdx + 1}/${questions.length}`;
        document.getElementById('question-text').innerText = q.q;
        const container = document.getElementById('options-container');
        container.innerHTML = '';
        q.options.forEach(opt => {
            const btn = document.createElement('button');
            btn.innerText = opt.text;
            btn.onclick = () => nextQuestion(opt.type);
            container.appendChild(btn);
        });
    }

    function nextQuestion(type) {
        scores[type]++;
        currentIdx++;
        if (currentIdx < questions.length) {
            showQuestion();
        } else {
            showResult();
        }
    }

    function showResult() {
        document.getElementById('quiz-screen').classList.add('hidden');
        document.getElementById('result').style.display = 'block';
        
        const winner = Object.keys(scores).reduce((a, b) => scores[a] > scores[b] ? a : b);
        
        const data = {
            Seller: { name: "Hệ CHIẾN THẦN CHỐT ĐƠN", desc: "Bạn sinh ra để làm chủ! Tết này lộc lá đầy nhà, đơn đi tấp nập." },
            Student_Chill: { name: "Hệ TẾT THẢNH THƠI", desc: "Không deadline, không áp lực. Bạn tận hưởng Tết đúng nghĩa 'chill' nhất." },
            Student_GenZ: { name: "Hệ GƯƠNG MẶT ĐẠI DIỆN", desc: "Tết là phải rực rỡ! Bạn là trung tâm của mọi cuộc vui và các trend mới nhất." }
        };

        document.getElementById('character-name').innerText = data[winner].name;
        document.getElementById('character-desc').innerText = data[winner].desc;
    }
</script>

</body>
</html>