#<!DOCTYPE html>
<html lang="ja">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>仮想会社メーカー</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;600;700&display=swap" rel="stylesheet">
    <style>
        body {
            font-family: 'Inter', sans-serif;
            background-color: #f0f4f8; /* Light blue-gray background */
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            margin: 0;
            padding: 20px;
            box-sizing: border-box;
        }
        .container {
            background-color: #ffffff;
            border-radius: 20px;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.1);
            padding: 30px;
            max-width: 900px;
            width: 100%;
            text-align: center;
            border: 1px solid #e2e8f0; /* Light border */
        }
        h1 {
            color: #2c3e50; /* Dark blue-gray for heading */
            margin-bottom: 20px;
            font-size: 2.25rem; /* text-4xl */
            font-weight: 700; /* font-bold */
        }
        label {
            display: block;
            margin-bottom: 8px;
            color: #4a5568; /* Gray for labels */
            font-weight: 600; /* font-semibold */
            text-align: left;
        }
        input[type="text"], textarea {
            width: 100%;
            padding: 12px;
            margin-bottom: 15px;
            border: 1px solid #cbd5e0; /* Light gray border */
            border-radius: 10px;
            font-size: 1rem;
            color: #2d3748; /* Darker gray for text */
            box-sizing: border-box;
            transition: border-color 0.3s ease;
        }
        input[type="text"]:focus, textarea:focus {
            outline: none;
            border-color: #63b3ed; /* Blue on focus */
            box-shadow: 0 0 0 3px rgba(99, 179, 237, 0.5);
        }
        button {
            background-image: linear-gradient(to right, #4CAF50, #8BC34A); /* Green gradient */
            color: white;
            padding: 14px 28px;
            border: none;
            border-radius: 12px;
            cursor: pointer;
            font-size: 1.1rem;
            font-weight: 700; /* font-bold */
            transition: all 0.3s ease;
            box-shadow: 0 5px 15px rgba(76, 175, 80, 0.4);
            margin-top: 20px;
        }
        button:hover {
            transform: translateY(-2px);
            box-shadow: 0 8px 20px rgba(76, 175, 80, 0.6);
        }
        .output-section {
            background-color: #edf2f7; /* Lighter blue-gray for output */
            border-radius: 15px;
            padding: 25px;
            margin-top: 30px;
            text-align: left;
            border: 1px solid #d4dee8; /* Even lighter border */
        }
        .output-section h2 {
            color: #2c3e50;
            font-size: 1.75rem; /* text-3xl */
            font-weight: 700;
            margin-bottom: 15px;
            border-bottom: 2px solid #a0aec0; /* Light border under heading */
            padding-bottom: 10px;
        }
        .output-section h3 {
            color: #2c3e50;
            font-size: 1.25rem; /* text-xl */
            font-weight: 700;
            margin-top: 20px;
            margin-bottom: 10px;
        }
        .output-section p {
            color: #4a5568;
            line-height: 1.6;
            margin-bottom: 10px;
        }
        .output-section p strong {
            color: #2c3e50;
        }
        .output-section ul {
            list-style: disc;
            margin-left: 20px;
            color: #4a5568;
        }
        .output-section ul li {
            margin-bottom: 8px;
        }
        .loading-spinner {
            border: 6px solid #f3f3f3;
            border-top: 6px solid #3498db;
            border-radius: 50%;
            width: 40px;
            height: 40px;
            animation: spin 1s linear infinite;
            margin: 20px auto;
            display: none; /* Hidden by default */
        }

        @keyframes spin {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }

        /* Responsive adjustments */
        @media (max-width: 768px) {
            .container {
                padding: 20px;
            }
            h1 {
                font-size: 1.8rem;
            }
            .output-section h2 {
                font-size: 1.5rem;
            }
            button {
                padding: 12px 24px;
                font-size: 1rem;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>🚀 仮想会社メーカー 🚀</h1>
        <p class="text-gray-600 mb-6">
            キミの大切なことや得意なことを教えてね！AIが最高の会社アイデアを提案するよ！
        </p>

        <div class="input-group mb-5">
            <label for="value1">大切にしたい価値観 1:</label>
            <input type="text" id="value1" placeholder="例: 創造性、挑戦">
            <label for="value2">大切にしたい価値観 2:</label>
            <input type="text" id="value2" placeholder="例: 協力、思いやり">
            <label for="value3">大切にしたい価値観 3:</label>
            <input type="text" id="value3" placeholder="例: 楽しさ、学び">
        </div>

        <div class="input-group mb-5">
            <label for="skill1">得意なこと・好きなことキーワード 1:</label>
            <input type="text" id="skill1" placeholder="例: 絵を描く、ゲーム">
            <label for="skill2">得意なこと・好きなことキーワード 2:</label>
            <input type="text" id="skill2" placeholder="例: プログラミング、読書">
            <label for="skill3">得意なこと・好きなことキーワード 3:</label>
            <input type="text" id="skill3" placeholder="例: スポーツ、音楽">
        </div>

        <button id="generateButton">会社を生成！</button>

        <div id="loadingSpinner" class="loading-spinner"></div>

        <div id="output" class="output-section hidden">
            <h2>💡 キミの会社はこれだ！</h2>
            <p><strong>会社の仮名称:</strong> <span id="outputCompanyName"></span></p>
            <p><strong>会社ってどんな感じ？:</strong> <span id="companyDescription"></span></p>
            <p><strong>どんな人に、どんなハッピーを届ける？:</strong> <span id="targetAudience"></span></p>
            <p><strong>大事な考え方や合言葉:</strong> <span id="slogan"></span></p>
            <p><strong>SDGsで世界を良くするアイデア:</strong> <span id="sdgsImpact"></span></p>

            <h3 class="text-xl font-bold mt-8 mb-4 text-gray-700">もっとアイデアを広げる質問！</h3>
            <ul>
                <li><span id="question1"></span></li>
                <li><span id="question2"></span></li>
                <li><span id="question3"></span></li>
            </ul>

            <h3 class="text-xl font-bold mt-8 mb-4 text-gray-700">もっとユニークにするヒント！</h3>
            <p><span id="originalityComment"></span></p>
        </div>
    </div>

    <script type="module">
        // Firebase AuthとFirestoreのインポート
        import { initializeApp } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-app.js";
        import { getAuth, signInAnonymously, signInWithCustomToken, onAuthStateChanged } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-auth.js";
        import { getFirestore, doc, setDoc, getDoc } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-firestore.js";

        // グローバル変数として提供されるアプリIDとFirebase設定
        const appId = typeof __app_id !== 'undefined' ? __app_id : 'default-app-id';
        const firebaseConfig = typeof __firebase_config !== 'undefined' ? JSON.parse(__firebase_config) : {};
        const initialAuthToken = typeof __initial_auth_token !== 'undefined' ? __initial_auth_token : null;

        // Firebaseの初期化
        const app = initializeApp(firebaseConfig);
        const db = getFirestore(app);
        const auth = getAuth(app);

        let userId = null; // ユーザーIDを保持する変数

        // 認証状態の変更をリッスン
        onAuthStateChanged(auth, async (user) => {
            if (user) {
                // ユーザーがサインイン済み
                userId = user.uid;
                console.log("Firebase user signed in:", userId);
                // 認証完了後に必要なFirestore操作があればここに追加
            } else {
                // ユーザーがサインアウト済み、またはまだサインインしていない
                // 匿名サインインを試みる
                try {
                    if (initialAuthToken) {
                        await signInWithCustomToken(auth, initialAuthToken);
                        console.log("Signed in with custom token.");
                    } else {
                        await signInAnonymously(auth);
                        console.log("Signed in anonymously.");
                    }
                } catch (error) {
                    console.error("Firebase authentication error:", error);
                }
            }
        });


        const generateButton = document.getElementById('generateButton');
        const loadingSpinner = document.getElementById('loadingSpinner');
        const outputDiv = document.getElementById('output');
        const outputCompanyNameSpan = document.getElementById('outputCompanyName');
        const companyDescriptionSpan = document.getElementById('companyDescription');
        const targetAudienceSpan = document.getElementById('targetAudience');
        const sloganSpan = document.getElementById('slogan');
        const sdgsImpactSpan = document.getElementById('sdgsImpact');
        const question1Span = document.getElementById('question1');
        const question2Span = document.getElementById('question2');
        const question3Span = document.getElementById('question3');
        const originalityCommentSpan = document.getElementById('originalityComment'); // オリジナリティコメントは1つに集約

        generateButton.addEventListener('click', async () => {
            const values = [
                document.getElementById('value1').value,
                document.getElementById('value2').value,
                document.getElementById('value3').value
            ].filter(v => v.trim() !== '');

            const skills = [
                document.getElementById('skill1').value,
                document.getElementById('skill2').value,
                document.getElementById('skill3').value
            ].filter(s => s.trim() !== '');

            if (values.length === 0 && skills.length === 0) {
                alert('大切な価値観と得意なこと・好きなことのキーワードを少なくとも1つずつ入力してね！');
                return;
            }

            loadingSpinner.style.display = 'block'; // スピナーを表示
            outputDiv.classList.add('hidden'); // 結果を非表示

            const prompt = `
            中学生が仮想の会社を作るための、ワクワクするようなアイデアを提案してね！
            以下の情報をもとに、会社について、どんな人にどんなことを届けるか、大事な考え方やスローガン、そしてSDGsにどう貢献できるかを教えてほしいな。
            さらに、その会社をもっとユニークにするための「とっておきのヒント」を1つ教えてね！

            大切にしたい価値観: ${values.join(', ') || '特に指定なし'}
            得意なこと・好きなことのキーワード: ${skills.join(', ') || '特に指定なし'}

            以下の形式でJSONを返してください:
            {
                "companyName": "会社の仮名称（例：未来クリエイト、夢実現ラボ）",
                "companyDescription": "会社について（例：どんな種類の会社で、何を目指しているか）",
                "targetAudience": "どんな人に、どんなことを届けるか（具体的な顧客層と提供価値）",
                "slogan": "大事にしている考え方やスローガン",
                "sdgsImpact": "SDGsのターゲットに合わせた社会へのインパクト（例：目標4 質の高い教育をみんなに - オンライン学習コンテンツの提供）",
                "question1": "アイデアを具体的にするための質問1",
                "question2": "アイデアを具体的にするための質問2",
                "question3": "アイデアを具体的にするための質問3",
                "originalityComment": "オリジナリティを高めるためのとっておきのヒント"
            }
            `;

            let chatHistory = [];
            chatHistory.push({ role: "user", parts: [{ text: prompt }] });

            const payload = {
                contents: chatHistory,
                generationConfig: {
                    responseMimeType: "application/json",
                    responseSchema: {
                        type: "OBJECT",
                        properties: {
                            "companyName": { "type": "STRING" },
                            "companyDescription": { "type": "STRING" },
                            "targetAudience": { "type": "STRING" },
                            "slogan": { "type": "STRING" },
                            "sdgsImpact": { "type": "STRING" },
                            "question1": { "type": "STRING" },
                            "question2": { "type": "STRING" },
                            "question3": { "type": "STRING" },
                            "originalityComment": { "type": "STRING" }
                        },
                        "propertyOrdering": ["companyName", "companyDescription", "targetAudience", "slogan", "sdgsImpact", "question1", "question2", "question3", "originalityComment"]
                    }
                }
            };

            const apiKey = ""; // APIキーはCanvasによって自動的に提供されます
            const apiUrl = `https://generativelanguage.googleapis.com/v1beta/models/gemini-2.0-flash:generateContent?key=${apiKey}`;

            try {
                const response = await fetch(apiUrl, {
                    method: 'POST',
                    headers: { 'Content-Type': 'application/json' },
                    body: JSON.stringify(payload)
                });

                const result = await response.json();
                console.log("LLM response:", result);

                if (result.candidates && result.candidates.length > 0 &&
                    result.candidates[0].content && result.candidates[0].content.parts &&
                    result.candidates[0].content.parts.length > 0) {
                    const jsonString = result.candidates[0].content.parts[0].text;
                    const parsedJson = JSON.parse(jsonString);

                    // 中学生が楽しめるような言い回しに調整
                    outputCompanyNameSpan.textContent = parsedJson.companyName;
                    companyDescriptionSpan.textContent = parsedJson.companyDescription;
                    targetAudienceSpan.textContent = parsedJson.targetAudience;
                    sloganSpan.textContent = parsedJson.slogan;
                    sdgsImpactSpan.textContent = parsedJson.sdgsImpact;
                    question1Span.textContent = parsedJson.question1;
                    question2Span.textContent = parsedJson.question2;
                    question3Span.textContent = parsedJson.question3;
                    originalityCommentSpan.textContent = parsedJson.originalityComment;
                    outputDiv.classList.remove('hidden'); // 結果を表示
                } else {
                    console.error("Unexpected response structure or content missing:", result);
                    alert('ごめんね、アイデアを考えるのに失敗しちゃったみたい。もう一度試してみてね！');
                }
            } catch (error) {
                console.error("Error calling LLM:", error);
                alert('あれれ？アイデアを考える途中でエラーが起きちゃったみたい。インターネットにつながっているか確認して、もう一度試してみてね！');
            } finally {
                loadingSpinner.style.display = 'none'; // スピナーを非表示
            }
        });
    </script>
</body>
</html>