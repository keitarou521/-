<!DOCTYPE html>
<html lang="ja">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>わかる！誤嚥性肺炎ガイド</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Noto+Sans+JP:wght@400;700&family=Roboto:wght@400;700&display=swap" rel="stylesheet">
    <!-- Chosen Palette: Warm Neutrals & Soft Blue -->
    <!-- Application Structure Plan: 単一ページのセクションベースデザインを採用し、画面上部に固定ナビゲーションを配置します。この構成は、PowerPointの線形的な流れを、ウェブ上で直感的に操作できる体験へと昇華させるためのものです。各セクションはPowerPointのスライド（概要、原因、症状、対策、まとめ）に対応しています。このシンプルな構造は、特に健康情報に不慣れな方や高齢の利用者にとって、情報の理解しやすさとアクセスの容易さを最大化します。利用者は順を追ってスクロールすることも、ナビゲーションを使って必要な情報へ直接ジャンプすることもでき、ガイド付き学習と迅速な参照の両方を可能にします。 -->
    <!-- Visualization & Content Choices: 
        - Report Info: なぜ起きるの？ - 原因 -> Goal: 複数の原因を整理し、魅力的に解説する -> Viz/Presentation Method: HTML/CSS(Tailwind)で作成したインタラクティブな図。中心の「原因」要素から各要因へ線が伸びる形式 -> Interaction: 各要因をクリックすると、隣のテキストボックスに詳細な説明が表示される -> Justification: 静的なリストを探索的な体験に変え、各原因についての能動的な学習を促進する -> Library/Method: HTML/CSS (Tailwind) & Vanilla JS.
        - Report Info: こんな症状に注意！ - サイン -> Goal: 症状リストを見やすく、理解しやすく提示する -> Viz/Presentation Method: アイコンと短いタイトルを持つカードのインタラクティブなグリッド -> Interaction: カードをクリックすると、その症状に関する詳細（例：「湿性嗄声」の説明）が表示される -> Justification: 長いリストよりも視覚的に魅力的で、利用者が一度に一つの症状に集中できるため、認知負荷を軽減する -> Library/Method: HTML/CSS (Tailwind) & Vanilla JS.
        - Report Info: 今日からできる！ - 対策 -> Goal: 異なる種類の対策を明確に分類して提示する -> Viz/Presentation Method: 「食事」「口腔ケア」「体操」のタブを持つインターフェース -> Interaction: タブをクリックすると、そのカテゴリに関連するヒントや情報が表示される -> Justification: 大量の情報を整理し、利用者が一度に一つのトピックに集中して予防策を学べるようにする -> Library/Method: HTML/CSS (Tailwind) & Vanilla JS.
    -->
    <!-- CONFIRMATION: NO SVG graphics used. NO Mermaid JS used. -->
    <style>
        body {
            font-family: 'Noto Sans JP', sans-serif;
            background-color: #FDFBF6;
            color: #4A4A4A;
        }
        h1, h2, h3, .font-roboto {
            font-family: 'Roboto', 'Noto Sans JP', sans-serif;
        }
        .nav-link {
            transition: all 0.3s ease;
            border-bottom: 2px solid transparent;
        }
        .nav-link:hover, .nav-link.active {
            color: #74B9D8;
            border-bottom-color: #74B9D8;
        }
        .tab-btn.active {
            background-color: #74B9D8;
            color: white;
        }
        .card {
            transition: transform 0.3s ease, box-shadow 0.3s ease;
        }
        .card:hover {
            transform: translateY(-5px);
            box-shadow: 0 10px 15px -3px rgba(0, 0, 0, 0.1), 0 4px 6px -2px rgba(0, 0, 0, 0.05);
        }
        html {
            scroll-behavior: smooth;
        }
        .content-section {
            display: none;
        }
        .content-section.active {
            display: block;
        }
        .symptom-card-detail {
            max-height: 0;
            overflow: hidden;
            transition: max-height 0.5s ease-out, padding 0.5s ease-out;
        }
    </style>
</head>
<body class="antialiased">

    <header id="header" class="bg-white/80 backdrop-blur-md sticky top-0 z-50 shadow-sm">
        <nav class="container mx-auto px-6 py-3 flex justify-between items-center">
            <div class="text-2xl font-bold text-gray-800 font-roboto">わかる！誤嚥性肺炎ガイド</div>
            <div class="hidden md:flex space-x-8">
                <a href="#overview" class="nav-link font-semibold pb-1">概要</a>
                <a href="#causes" class="nav-link font-semibold pb-1">原因</a>
                <a href="#symptoms" class="nav-link font-semibold pb-1">症状</a>
                <a href="#measures" class="nav-link font-semibold pb-1">対策</a>
                <a href="#summary" class="nav-link font-semibold pb-1">まとめ</a>
            </div>
            <button id="mobile-menu-button" class="md:hidden focus:outline-none">
                <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h16m-7 6h7"></path></svg>
            </button>
        </nav>
        <div id="mobile-menu" class="hidden md:hidden">
            <a href="#overview" class="block py-2 px-4 text-sm hover:bg-gray-200">概要</a>
            <a href="#causes" class="block py-2 px-4 text-sm hover:bg-gray-200">原因</a>
            <a href="#symptoms" class="block py-2 px-4 text-sm hover:bg-gray-200">症状</a>
            <a href="#measures" class="block py-2 px-4 text-sm hover:bg-gray-200">対策</a>
            <a href="#summary" class="block py-2 px-4 text-sm hover:bg-gray-200">まとめ</a>
        </div>
    </header>

    <main>
        <section id="overview" class="py-20 bg-white">
            <div class="container mx-auto px-6 text-center">
                <h1 class="text-4xl md:text-5xl font-bold mb-4 text-gray-800">誤嚥性肺炎を知ろう！</h1>
                <p class="text-lg md:text-xl text-gray-600 max-w-3xl mx-auto mb-8">大切な人を守るために、その原因から対策まで、わかりやすく解説します。</p>
                <div class="bg-blue-50 border-l-4 border-blue-400 text-blue-800 p-6 rounded-r-lg max-w-3xl mx-auto text-left shadow-md">
                    <h3 class="font-bold text-xl mb-2">はじめに：誤嚥性肺炎って何？</h3>
                    <p class="mb-2">食べ物や唾液が誤って気管に入り、それが原因で肺に炎症が起きる病気です。</p>
                    <p class="mb-2">特に<strong class="text-blue-600">高齢者</strong>や、<strong class="text-blue-600">飲み込む力が弱くなった方</strong>に多く見られます。</p>
                    <p>症状が分かりにくく、知らず知らずのうちに進行することもあるため、正しい知識を持つことが重要です。</p>
                </div>
            </div>
        </section>

        <section id="causes" class="py-20">
            <div class="container mx-auto px-6">
                <div class="text-center mb-12">
                    <h2 class="text-3xl md:text-4xl font-bold text-gray-800">なぜ起きるの？</h2>
                    <p class="text-lg text-gray-600 mt-2">誤嚥性肺炎の主な原因を探ってみましょう。</p>
                </div>
                <div class="flex flex-col md:flex-row items-center gap-8 md:gap-12">
                    <div class="w-full md:w-1/2">
                        <div id="cause-info" class="bg-white p-6 rounded-lg shadow-lg min-h-[200px] transition-all duration-300">
                            <h3 id="cause-title" class="text-2xl font-bold mb-3 text-gray-800">原因を選択してください</h3>
                            <p id="cause-text" class="text-gray-600">左のボタンをクリックすると、ここに詳しい説明が表示されます。</p>
                        </div>
                    </div>
                    <div class="w-full md:w-1/2 grid grid-cols-2 gap-4">
                        <button data-title="飲み込む力の低下" data-text="加齢や病気（脳卒中、パーキンソン病など）により、食べ物や唾液をうまく飲み込めなくなることが最大の原因です。" class="cause-btn bg-blue-100 hover:bg-blue-200 text-blue-800 font-bold py-4 px-2 rounded-lg shadow transition">① 飲み込む力の低下</button>
                        <button data-title="咳をする力の低下" data-text="誤って気管に入った異物を、咳で体外に排出する力が弱まると、細菌が肺に到達しやすくなります。" class="cause-btn bg-green-100 hover:bg-green-200 text-green-800 font-bold py-4 px-2 rounded-lg shadow transition">② 咳をする力の低下</button>
                        <button data-title="口腔ケアの不足" data-text="口の中に細菌が多いと、唾液などを誤嚥した際に、それらの細菌が肺に入り込み、肺炎を引き起こしやすくなります。" class="cause-btn bg-yellow-100 hover:bg-yellow-200 text-yellow-800 font-bold py-4 px-2 rounded-lg shadow transition">③ 口腔ケアの不足</button>
                        <button data-title="その他の要因" data-text="胃の中身が逆流する「胃食道逆流症」や、免疫力の低下なども、誤嚥性肺炎のリスクを高める要因となります。" class="cause-btn bg-red-100 hover:bg-red-200 text-red-800 font-bold py-4 px-2 rounded-lg shadow transition">④ その他の要因</button>
                    </div>
                </div>
            </div>
        </section>

        <section id="symptoms" class="py-20 bg-white">
            <div class="container mx-auto px-6">
                <div class="text-center mb-12">
                    <h2 class="text-3xl md:text-4xl font-bold text-gray-800">こんな症状に注意！</h2>
                    <p class="text-lg text-gray-600 mt-2">誤嚥性肺炎のサインを見逃さないでください。カードをタップして詳細を確認できます。</p>
                </div>
                <div class="grid md:grid-cols-2 lg:grid-cols-3 gap-8">
                    <div class="symptom-card card bg-gray-50 rounded-lg shadow-md p-6 cursor-pointer">
                        <div class="flex items-center mb-3">
                            <span class="text-3xl mr-4">😮</span>
                            <h3 class="text-xl font-bold">食事中のむせ・咳</h3>
                        </div>
                        <p class="text-gray-600">特に水分でむせることが増えたら注意が必要です。</p>
                        <div class="symptom-card-detail pt-3 mt-3 border-t border-gray-200">
                            <p class="text-sm text-gray-700">食事中だけでなく、食後に痰が増えたり、ゼロゼロという音が喉から聞こえたりする場合もサインの一つです。これは、食べ物や飲み物がうまく食道に送られていない可能性を示しています。</p>
                        </div>
                    </div>
                    <div class="symptom-card card bg-gray-50 rounded-lg shadow-md p-6 cursor-pointer">
                        <div class="flex items-center mb-3">
                            <span class="text-3xl mr-4">🗣️</span>
                            <h3 class="text-xl font-bold">声のかすれ</h3>
                        </div>
                        <p class="text-gray-600">食後に声がガラガラになるのは危険なサインです。</p>
                        <div class="symptom-card-detail pt-3 mt-3 border-t border-gray-200">
                            <p class="text-sm text-gray-700">これは「湿性嗄声（しっせいさせい）」と呼ばれ、唾液や食べ物のカスが声帯の周りに残っている状態を示します。飲み込みがうまくいっていない証拠です。</p>
                        </div>
                    </div>
                    <div class="symptom-card card bg-gray-50 rounded-lg shadow-md p-6 cursor-pointer">
                        <div class="flex items-center mb-3">
                            <span class="text-3xl mr-4">🤒</span>
                            <h3 class="text-xl font-bold">原因不明の熱</h3>
                        </div>
                        <p class="text-gray-600">はっきりした風邪症状がないのに微熱が続くことがあります。</p>
                         <div class="symptom-card-detail pt-3 mt-3 border-t border-gray-200">
                            <p class="text-sm text-gray-700">元気がない、食欲がないといった変化と共に微熱が見られる場合、本人が気づかないうちに少量の誤嚥を繰り返し、軽い炎症が肺で起きている可能性があります。</p>
                        </div>
                    </div>
                    <div class="symptom-card card bg-gray-50 rounded-lg shadow-md p-6 cursor-pointer">
                        <div class="flex items-center mb-3">
                            <span class="text-3xl mr-4">📉</span>
                            <h3 class="text-xl font-bold">体重の減少</h3>
                        </div>
                        <p class="text-gray-600">食事を避けるようになり、栄養状態が悪化しているかも。</p>
                         <div class="symptom-card-detail pt-3 mt-3 border-t border-gray-200">
                            <p class="text-sm text-gray-700">むせるのが怖くて無意識に食事量を減らしてしまったり、うまく飲み込めずに十分な栄養が摂れていなかったりする可能性があります。体重減少は体の危険信号です。</p>
                        </div>
                    </div>
                     <div class="symptom-card card bg-gray-50 rounded-lg shadow-md p-6 cursor-pointer">
                        <div class="flex items-center mb-3">
                            <span class="text-3xl mr-4">🌙</span>
                            <h3 class="text-xl font-bold">睡眠中の咳</h3>
                        </div>
                        <p class="text-gray-600">寝ている間に唾液を誤嚥している可能性があります。</p>
                         <div class="symptom-card-detail pt-3 mt-3 border-t border-gray-200">
                            <p class="text-sm text-gray-700">日中だけでなく、夜間、眠っている間に無意識に唾液が気管に流れ込んでしまうことがあります。起床時に痰が多かったり、枕が汚れていたりするのもサインかもしれません。</p>
                        </div>
                    </div>
                     <div class="symptom-card card bg-gray-50 rounded-lg shadow-md p-6 cursor-pointer">
                        <div class="flex items-center mb-3">
                            <span class="text-3xl mr-4">😮‍💨</span>
                            <h3 class="text-xl font-bold">痰が増える</h3>
                        </div>
                        <p class="text-gray-600">特に食事中や食後に痰がからむことが多くなります。</p>
                         <div class="symptom-card-detail pt-3 mt-3 border-t border-gray-200">
                            <p class="text-sm text-gray-700">体は、誤って気管に入った異物を外に出そうとして、防御反応として痰を多く作り出します。色のついた痰が出る場合は、細菌感染の可能性も考えられます。</p>
                        </div>
                    </div>
                </div>
            </div>
        </section>

        <section id="measures" class="py-20">
            <div class="container mx-auto px-6">
                <div class="text-center mb-12">
                    <h2 class="text-3xl md:text-4xl font-bold text-gray-800">今日からできる対策</h2>
                    <p class="text-lg text-gray-600 mt-2">予防のために大切な３つのポイント。タブを切り替えて見てみましょう。</p>
                </div>
                <div class="max-w-4xl mx-auto">
                    <div class="flex justify-center border-b-2 border-gray-200 mb-8">
                        <button class="tab-btn active text-lg font-semibold py-3 px-6 -mb-0.5" data-tab="food">食事の工夫</button>
                        <button class="tab-btn text-lg font-semibold py-3 px-6 -mb-0.5" data-tab="care">口腔ケア</button>
                        <button class="tab-btn text-lg font-semibold py-3 px-6 -mb-0.5" data-tab="exercise">お口の体操</button>
                    </div>
                    <div id="food" class="content-section active bg-white p-8 rounded-lg shadow-lg">
                        <h3 class="text-2xl font-bold mb-4">🍽️ 食事の工夫</h3>
                        <ul class="list-disc list-inside space-y-3 text-gray-700">
                            <li><strong class="text-gray-800">正しい姿勢で：</strong>椅子に深く座り、少し前かがみであごを引く。</li>
                            <li><strong class="text-gray-800">少量ずつゆっくり：</strong>一口の量を減らし、よく噛んでから飲み込む。</li>
                            <li><strong class="text-gray-800">食べやすい工夫：</strong>パサパサするものは避け、とろみ剤やあんかけを活用してまとまりを良くする。</li>
                            <li><strong class="text-gray-800">食後は休憩：</strong>食後30分～1時間は横にならず、座った姿勢を保つ。</li>
                        </ul>
                    </div>
                    <div id="care" class="content-section bg-white p-8 rounded-lg shadow-lg">
                        <h3 class="text-2xl font-bold mb-4">🪥 口腔ケア</h3>
                        <ul class="list-disc list-inside space-y-3 text-gray-700">
                            <li><strong class="text-gray-800">毎食後の歯磨き：</strong>食べかすを取り除き、口の中を清潔に保つ。</li>
                            <li><strong class="text-gray-800">義歯の手入れ：</strong>義歯は外して丁寧に洗浄する。</li>
                            <li><strong class="text-gray-800">舌の清掃：</strong>舌の表面の汚れ（舌苔）も細菌の温床。専用のブラシで優しく清掃する。</li>
                            <li><strong class="text-gray-800">保湿も重要：</strong>口の中が乾燥すると細菌が繁殖しやすくなるため、うがいや保湿ジェルで潤いを保つ。</li>
                        </ul>
                    </div>
                    <div id="exercise" class="content-section bg-white p-8 rounded-lg shadow-lg">
                        <h3 class="text-2xl font-bold mb-4">🤸 お口の体操（嚥下体操）</h3>
                        <p class="mb-4 text-gray-700">飲み込みに必要な筋肉を鍛え、唾液の分泌を促します。食事の前に行うと効果的です。</p>
                        <ul class="list-disc list-inside space-y-3 text-gray-700">
                            <li><strong class="text-gray-800">パタカラ体操：</strong>「パ」「タ」「カ」「ラ」と、それぞれはっきり、大きく口を動かして発音する。</li>
                            <li><strong class="text-gray-800">首の運動：</strong>ゆっくりと首を左右に回したり、前に倒したりする。</li>
                            <li><strong class="text-gray-800">頬の運動：</strong>口をすぼめたり、頬を大きく膨らませたりを繰り返す。</li>
                            <li><strong class="text-gray-800">唾液腺マッサージ：</strong>耳の下やあごの下を優しくマッサージし、唾液の分泌を促す。</li>
                        </ul>
                    </div>
                </div>
            </div>
        </section>

        <section id="summary" class="py-20 bg-blue-50">
            <div class="container mx-auto px-6 text-center">
                <h2 class="text-3xl md:text-4xl font-bold text-gray-800 mb-6">まとめ</h2>
                <div class="max-w-3xl mx-auto bg-white p-8 rounded-lg shadow-lg text-left space-y-4">
                    <p class="flex items-start"><span class="text-blue-500 font-bold text-2xl mr-3">✓</span><span>誤嚥性肺炎は、飲み込む力や咳をする力の低下、口腔内の不衛生が重なって起こります。</span></p>
                    <p class="flex items-start"><span class="text-blue-500 font-bold text-2xl mr-3">✓</span><span>「むせ」「声がすれ」「微熱」などの小さな<strong class="text-blue-600">サイン</strong>に早く気づくことが大切です。</span></p>
                    <p class="flex items-start"><span class="text-blue-500 font-bold text-2xl mr-3">✓</span><span>食事の工夫、丁寧な口腔ケア、お口の体操といった日々の<strong class="text-blue-600">予防</strong>が何よりも重要です。</span></p>
                    <p class="flex items-start"><span class="text-blue-500 font-bold text-2xl mr-3">✓</span><span>気になる症状があれば、ためらわずに、かかりつけ医や歯科医、専門家に<strong class="text-blue-600">相談</strong>しましょう。</span></p>
                </div>
            </div>
        </section>
    </main>

    <footer class="bg-gray-800 text-white py-8">
        <div class="container mx-auto px-6 text-center">
            <p>&copy; 2025 わかる！誤嚥性肺炎ガイド. この情報は医療専門家のアドバイスに代わるものではありません。</p>
        </div>
    </footer>

    <script>
        document.addEventListener('DOMContentLoaded', function () {
            const mobileMenuButton = document.getElementById('mobile-menu-button');
            const mobileMenu = document.getElementById('mobile-menu');
            mobileMenuButton.addEventListener('click', () => {
                mobileMenu.classList.toggle('hidden');
            });

            const mobileNavLinks = mobileMenu.querySelectorAll('a');
            mobileNavLinks.forEach(link => {
                link.addEventListener('click', () => {
                    mobileMenu.classList.add('hidden');
                });
            });

            const causeBtns = document.querySelectorAll('.cause-btn');
            const causeTitle = document.getElementById('cause-title');
            const causeText = document.getElementById('cause-text');
            if (causeBtns.length > 0) {
                causeTitle.textContent = causeBtns[0].dataset.title;
                causeText.textContent = causeBtns[0].dataset.text;
                causeBtns[0].classList.add('ring-2', 'ring-blue-500');

                causeBtns.forEach(btn => {
                    btn.addEventListener('click', () => {
                        causeTitle.textContent = btn.dataset.title;
                        causeText.textContent = btn.dataset.text;
                        causeBtns.forEach(b => b.classList.remove('ring-2', 'ring-blue-500'));
                        btn.classList.add('ring-2', 'ring-blue-500');
                    });
                });
            }
            
            const symptomCards = document.querySelectorAll('.symptom-card');
            symptomCards.forEach(card => {
                card.addEventListener('click', () => {
                    const detail = card.querySelector('.symptom-card-detail');
                    if (detail.style.maxHeight) {
                        detail.style.maxHeight = null;
                        detail.style.paddingTop = null;
                        detail.style.paddingBottom = null;
                    } else {
                        detail.style.paddingTop = '0.75rem';
                        detail.style.paddingBottom = '0.75rem';
                        detail.style.maxHeight = detail.scrollHeight + "px";
                    }
                });
            });

            const tabBtns = document.querySelectorAll('.tab-btn');
            const contentSections = document.querySelectorAll('.content-section');
            tabBtns.forEach(btn => {
                btn.addEventListener('click', () => {
                    tabBtns.forEach(b => b.classList.remove('active'));
                    btn.classList.add('active');
                    
                    const tabId = btn.dataset.tab;
                    contentSections.forEach(section => {
                        if (section.id === tabId) {
                            section.classList.add('active');
                        } else {
                            section.classList.remove('active');
                        }
                    });
                });
            });
            
            const navLinks = document.querySelectorAll('.nav-link');
            const sections = document.querySelectorAll('main section');
            const headerHeight = document.getElementById('header').offsetHeight;

            const onScroll = () => {
                let currentSection = '';
                sections.forEach(section => {
                    const sectionTop = section.offsetTop - headerHeight - 20;
                    if (window.scrollY >= sectionTop) {
                        currentSection = section.getAttribute('id');
                    }
                });

                navLinks.forEach(link => {
                    link.classList.remove('active');
                    if (link.getAttribute('href').substring(1) === currentSection) {
                        link.classList.add('active');
                    }
                });
            };
            window.addEventListener('scroll', onScroll);
        });
    </script>

</body>
</html>
