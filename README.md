<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>我们的全家福回忆录 🏡</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Microsoft YaHei', 'PingFang SC', sans-serif;
        }

        /* 动态温馨背景 */
        body {
            background: linear-gradient(120deg, #f9f6f0, #f5f0e6);
            overflow-x: hidden;
            position: relative;
            min-height: 100vh;
        }

        .bg-particles {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            pointer-events: none;
            z-index: 0;
        }

        /* 顶部导航/组块跳转 */
        .nav-container {
            position: sticky;
            top: 0;
            background: rgba(255, 255, 255, 0.98);
            padding: 18px 0;
            box-shadow: 0 2px 15px rgba(201, 174, 122, 0.15);
            z-index: 100;
        }

        .nav-links {
            display: flex;
            justify-content: center;
            gap: 40px;
            flex-wrap: wrap;
        }

        .nav-links a {
            text-decoration: none;
            color: #8b6e3c;
            font-size: 18px;
            font-weight: 600;
            padding: 10px 20px;
            border-radius: 25px;
            transition: all 0.4s ease;
            position: relative;
        }

        .nav-links a::after {
            content: '';
            position: absolute;
            bottom: 5px;
            left: 50%;
            transform: translateX(-50%);
            width: 0;
            height: 2px;
            background: #d4b16a;
            transition: width 0.4s ease;
        }

        .nav-links a:hover {
            color: #d4b16a;
            background-color: rgba(212, 177, 106, 0.08);
        }

        .nav-links a:hover::after {
            width: 80%;
        }

        /* 主容器 */
        .container {
            max-width: 1280px;
            margin: 0 auto;
            padding: 40px 25px;
            position: relative;
            z-index: 10;
        }

        /* 标题样式 */
        .title-section {
            text-align: center;
            margin-bottom: 60px;
            color: #7a5c29;
            position: relative;
        }

        .title-section::after {
            content: '';
            display: block;
            width: 120px;
            height: 3px;
            background: linear-gradient(to right, #d4b16a, #8b6e3c);
            margin: 20px auto 0;
            border-radius: 3px;
        }

        .title-section h1 {
            font-size: 42px;
            margin-bottom: 15px;
            font-weight: 700;
            letter-spacing: 2px;
            text-shadow: 1px 1px 3px rgba(0,0,0,0.05);
        }

        .title-section p {
            font-size: 20px;
            color: #9d7c41;
            line-height: 1.8;
        }

        /* 图片上传区域 */
        .upload-section {
            background: white;
            border-radius: 20px;
            padding: 40px;
            margin-bottom: 60px;
            box-shadow: 0 8px 25px rgba(201, 174, 122, 0.1);
            text-align: center;
            border: 1px solid rgba(212, 177, 106, 0.15);
        }

        .upload-section h2 {
            color: #7a5c29;
            margin-bottom: 25px;
            font-size: 28px;
            font-weight: 600;
        }

        .upload-btn {
            display: inline-block;
            background: linear-gradient(to right, #d4b16a, #b9944d);
            color: white;
            padding: 15px 40px;
            border-radius: 35px;
            cursor: pointer;
            transition: all 0.4s ease;
            margin-bottom: 20px;
            font-size: 18px;
            font-weight: 600;
            box-shadow: 0 5px 15px rgba(212, 177, 106, 0.25);
        }

        .upload-btn:hover {
            transform: translateY(-3px);
            box-shadow: 0 8px 20px rgba(212, 177, 106, 0.35);
        }

        #file-input {
            display: none;
        }

        .upload-tips {
            color: #777;
            font-size: 15px;
            line-height: 1.6;
        }

        #preview-container {
            margin-top: 25px;
            display: flex;
            flex-wrap: wrap;
            gap: 15px;
            justify-content: center;
            padding: 15px;
        }

        #preview-container img {
            width: 110px;
            height: 110px;
            object-fit: cover;
            border-radius: 12px;
            box-shadow: 0 4px 10px rgba(0,0,0,0.08);
            transition: transform 0.3s ease;
        }

        #preview-container img:hover {
            transform: scale(1.05);
        }

        /* 轮播区域 */
        .carousel-section {
            background: white;
            border-radius: 20px;
            padding: 40px;
            box-shadow: 0 8px 25px rgba(201, 174, 122, 0.1);
            margin-bottom: 60px;
            border: 1px solid rgba(212, 177, 106, 0.15);
        }

        .carousel-section h2 {
            color: #7a5c29;
            margin-bottom: 30px;
            text-align: center;
            font-size: 28px;
            font-weight: 600;
        }

        .carousel-container {
            position: relative;
            max-width: 900px;
            margin: 0 auto;
            overflow: hidden;
            border-radius: 15px;
            box-shadow: 0 10px 30px rgba(0,0,0,0.1);
        }

        .carousel-slides {
            display: flex;
            transition: transform 0.6s ease-in-out;
        }

        .carousel-slide {
            min-width: 100%;
            height: 550px;
            display: flex;
            justify-content: center;
            align-items: center;
            background: #f9f6f0;
            padding: 20px;
        }

        .carousel-slide img {
            max-width: 100%;
            max-height: 100%;
            object-fit: contain;
            border-radius: 10px;
            box-shadow: 0 8px 20px rgba(0,0,0,0.12);
        }

        .carousel-slide .empty-tip {
            color: #9d7c41;
            font-size: 22px;
            text-align: center;
            padding: 20px;
            line-height: 1.8;
        }

        .carousel-nav {
            position: absolute;
            top: 50%;
            width: 100%;
            display: flex;
            justify-content: space-between;
            transform: translateY(-50%);
            padding: 0 25px;
        }

        .carousel-btn {
            width: 50px;
            height: 50px;
            border-radius: 50%;
            background: rgba(255, 255, 255, 0.9);
            color: #8b6e3c;
            border: none;
            cursor: pointer;
            display: flex;
            justify-content: center;
            align-items: center;
            font-size: 24px;
            transition: all 0.4s ease;
            box-shadow: 0 4px 12px rgba(0,0,0,0.1);
        }

        .carousel-btn:hover {
            background: #d4b16a;
            color: white;
            transform: scale(1.1);
        }

        .carousel-indicators {
            position: absolute;
            bottom: 25px;
            left: 50%;
            transform: translateX(-50%);
            display: flex;
            gap: 12px;
        }

        .indicator {
            width: 14px;
            height: 14px;
            border-radius: 50%;
            background: rgba(255, 255, 255, 0.75);
            cursor: pointer;
            transition: all 0.4s ease;
            border: 2px solid transparent;
        }

        .indicator.active {
            background: #d4b16a;
            transform: scale(1.2);
            border-color: white;
        }

        /* 家庭回忆区域 */
        .memories-section {
            background: white;
            border-radius: 20px;
            padding: 40px;
            box-shadow: 0 8px 25px rgba(201, 174, 122, 0.1);
            border: 1px solid rgba(212, 177, 106, 0.15);
        }

        .memories-section h2 {
            color: #7a5c29;
            margin-bottom: 30px;
            text-align: center;
            font-size: 28px;
            font-weight: 600;
        }

        .memory-card {
            margin-bottom: 35px;
            padding: 25px;
            border-left: 4px solid #d4b16a;
            background: #f9f6f0;
            border-radius: 10px;
            transition: transform 0.3s ease;
        }

        .memory-card:hover {
            transform: translateY(-5px);
            box-shadow: 0 8px 15px rgba(212, 177, 106, 0.1);
        }

        .memory-card h3 {
            color: #7a5c29;
            margin-bottom: 12px;
            font-size: 22px;
            font-weight: 600;
        }

        .memory-card p {
            color: #555;
            line-height: 1.8;
            font-size: 16px;
        }

        /* 音乐控制 */
        .music-control {
            position: fixed;
            bottom: 40px;
            right: 40px;
            z-index: 100;
            background: linear-gradient(to right, #d4b16a, #b9944d);
            width: 70px;
            height: 70px;
            border-radius: 50%;
            display: flex;
            justify-content: center;
            align-items: center;
            color: white;
            cursor: pointer;
            box-shadow: 0 8px 20px rgba(212, 177, 106, 0.4);
            transition: all 0.4s ease;
        }

        .music-control:hover {
            transform: scale(1.1);
            box-shadow: 0 10px 25px rgba(212, 177, 106, 0.5);
        }

        /* 响应式适配 */
        @media (max-width: 992px) {
            .carousel-slide {
                height: 450px;
            }
            .title-section h1 {
                font-size: 36px;
            }
        }

        @media (max-width: 768px) {
            .carousel-slide {
                height: 350px;
            }
            .title-section h1 {
                font-size: 30px;
            }
            .nav-links {
                gap: 20px;
            }
            .nav-links a {
                font-size: 16px;
                padding: 8px 15px;
            }
            .container {
                padding: 30px 15px;
            }
            .upload-section, .carousel-section, .memories-section {
                padding: 30px 20px;
            }
            .music-control {
                width: 60px;
                height: 60px;
                bottom: 25px;
                right: 25px;
            }
        }

        @media (max-width: 576px) {
            .carousel-slide {
                height: 280px;
            }
            .title-section h1 {
                font-size: 26px;
            }
            #preview-container img {
                width: 90px;
                height: 90px;
            }
        }
    </style>
</head>
<body>
    <!-- 动态温馨背景 -->
    <div class="bg-particles" id="particleContainer"></div>

    <!-- 导航栏（组块跳转） -->
    <div class="nav-container">
        <div class="nav-links">
            <a href="#upload">上传全家福</a>
            <a href="#carousel">幸福瞬间</a>
            <a href="#memories">家庭回忆</a>
        </div>
    </div>

    <!-- 主容器 -->
    <div class="container">
        <!-- 标题区域 -->
        <div class="title-section">
            <h1>我们的全家福回忆录 🏡</h1>
            <p>记录阖家欢乐的美好时光，珍藏每一份温暖与幸福</p>
        </div>

        <!-- 图片上传区域 -->
        <div class="upload-section" id="upload">
            <h2>上传我们的幸福全家福</h2>
            <label for="file-input" class="upload-btn">
                选择照片
            </label>
            <input type="file" id="file-input" accept="image/*" multiple>
            <p class="upload-tips">支持上传多张图片，格式为jpg、png等 | 上传后自动展示在幸福瞬间轮播区</p>
            <div id="preview-container"></div>
        </div>

        <!-- 轮播展示区域 -->
        <div class="carousel-section" id="carousel">
            <h2>阖家欢乐的幸福瞬间</h2>
            <div class="carousel-container">
                <div class="carousel-slides" id="carouselSlides">
                    <!-- 初始空状态 -->
                    <div class="carousel-slide">
                        <div class="empty-tip">🏡 上传全家福照片后<br>这里将展示我们温馨的幸福瞬间 🏡</div>
                    </div>
                </div>
                <div class="carousel-nav">
                    <button class="carousel-btn" id="prevBtn">◀</button>
                    <button class="carousel-btn" id="nextBtn">▶</button>
                </div>
                <div class="carousel-indicators" id="carouselIndicators">
                    <div class="indicator active"></div>
                </div>
            </div>
        </div>

        <!-- 家庭回忆区域 -->
        <div class="memories-section" id="memories">
            <h2>我们的家庭温馨回忆</h2>
            <div class="memory-card">
                <h3>团圆的年夜饭 🥢</h3>
                <p>每到除夕，一家人围坐在一起，张罗着丰盛的年夜饭，欢声笑语中，感受着最朴实的幸福。饭菜的香气，家人的笑脸，都是刻在心底最温暖的记忆。</p>
            </div>
            <div class="memory-card">
                <h3>温馨的家庭旅行 ✈️</h3>
                <p>一起走过的山川湖海，看过的日出日落，每一段旅程都因为有家人的陪伴而格外珍贵。那些在路上的欢声笑语，成为了我们共同的美好回忆。</p>
            </div>
            <div class="memory-card">
                <h3>日常的小美好 ☀️</h3>
                <p>清晨的一碗热粥，傍晚的一句问候，饭后的散步聊天，平凡日子里的点点滴滴，汇聚成最珍贵的家庭温暖。简单的幸福，就是一家人整整齐齐，和和美美。</p>
            </div>
            <div class="memory-card">
                <h3>重要的人生时刻 🎉</h3>
                <p>生日的祝福，节日的庆祝，人生中的每一个重要节点，都有家人的陪伴与见证。这些温馨的时刻，串联起我们家庭的幸福轨迹，成为永恒的珍藏。</p>
            </div>
        </div>
    </div>

    <!-- 音乐控制 -->
    <div class="music-control" id="musicBtn">
        🎵
    </div>

    <!-- 背景音乐元素 - 温馨家庭风音乐 -->
    <audio id="backgroundMusic" loop>
        <!-- 温馨纯音乐：《卡农》钢琴版 -->
        <source src="https://music.163.com/song/media/outer/url?id=181909.mp3" type="audio/mpeg">
    </audio>

    <script>
        // 1. 动态温馨背景粒子
        function createParticles() {
            const container = document.getElementById('particleContainer');
            setInterval(() => {
                const particle = document.createElement('div');
                // 随机大小
                const size = Math.random() * 15 + 8;
                // 随机位置
                const left = Math.random() * 100;
                // 温馨色系
                const colors = ['#d4b16a', '#e6c785', '#f0d9a0', '#e9cd8e', '#dbb978'];
                const color = colors[Math.floor(Math.random() * colors.length)];
                
                particle.style.cssText = `
                    position: absolute;
                    left: ${left}%;
                    bottom: -${size}px;
                    width: ${size}px;
                    height: ${size}px;
                    background: ${color};
                    border-radius: ${Math.random() > 0.5 ? '50%' : '10px'};
                    opacity: ${Math.random() * 0.6 + 0.3};
                    pointer-events: none;
                    animation: floatUp linear ${Math.random() * 15 + 10}s forwards;
                `;
                
                container.appendChild(particle);
                
                // 动画结束后移除元素
                setTimeout(() => {
                    particle.remove();
                }, 25000);
            }, 500);
        }

        // 添加粒子上浮动画
        const style = document.createElement('style');
        style.textContent = `
            @keyframes floatUp {
                0% {
                    bottom: -20px;
                    opacity: 0.8;
                    transform: translateX(0);
                }
                50% {
                    transform: translateX(Math.random() * 40 - 20px);
                }
                100% {
                    bottom: 100%;
                    opacity: 0;
                    transform: translateX(0);
                }
            }
        `;
        document.head.appendChild(style);

        // 2. 图片上传核心功能（彻底修复轮播问题）
        const fileInput = document.getElementById('file-input');
        const previewContainer = document.getElementById('preview-container');
        const carouselSlides = document.getElementById('carouselSlides');
        const carouselIndicators = document.getElementById('carouselIndicators');
        let uploadedImages = [];
        let currentSlide = 0;
        let carouselInterval = null;

        // 初始化空轮播
        function initEmptyCarousel() {
            carouselSlides.innerHTML = `
                <div class="carousel-slide">
                    <div class="empty-tip">🏡 上传全家福照片后<br>这里将展示我们温馨的幸福瞬间 🏡</div>
                </div>
            `;
            carouselIndicators.innerHTML = `<div class="indicator active"></div>`;
            currentSlide = 0;
            
            // 清除自动轮播
            if (carouselInterval) clearInterval(carouselInterval);
        }

        // 绑定文件上传事件（核心修复）
        fileInput.addEventListener('change', async function(e) {
            const files = Array.from(e.target.files);
            if (files.length === 0) return;

            // 清空原有数据
            previewContainer.innerHTML = '';
            uploadedImages = [];
            currentSlide = 0;

            // 处理所有上传文件
            for (const file of files) {
                if (!file.type.startsWith('image/')) continue;
                
                // 使用Promise确保文件读取完成
                const imgUrl = await new Promise((resolve) => {
                    const reader = new FileReader();
                    reader.onload = (event) => resolve(event.target.result);
                    reader.readAsDataURL(file);
                });

                // 保存图片URL
                uploadedImages.push(imgUrl);
                
                // 创建预览图
                const previewImg = document.createElement('img');
                previewImg.src = imgUrl;
                previewImg.alt = `全家福${uploadedImages.length}`;
                previewContainer.appendChild(previewImg);
            }

            // 所有图片处理完成后更新轮播
            updateCarousel();
        });

        // 更新轮播函数（100%修复版）
        function updateCarousel() {
            // 空数据处理
            if (uploadedImages.length === 0) {
                initEmptyCarousel();
                return;
            }

            // 清空轮播容器
            carouselSlides.innerHTML = '';
            carouselIndicators.innerHTML = '';

            // 添加所有上传图片到轮播
            uploadedImages.forEach((imgSrc, index) => {
                // 创建轮播项
                const slide = document.createElement('div');
                slide.className = 'carousel-slide';
                slide.innerHTML = `<img src="${imgSrc}" alt="我们的全家福 ${index + 1}">`;
                carouselSlides.appendChild(slide);

                // 创建指示器
                const indicator = document.createElement('div');
                indicator.className = `indicator ${index === 0 ? 'active' : ''}`;
                indicator.dataset.index = index;
                carouselIndicators.appendChild(indicator);

                // 指示器点击事件
                indicator.addEventListener('click', function() {
                    currentSlide = parseInt(this.dataset.index);
                    showSlide(currentSlide);
                });
            });

            // 显示第一张
            showSlide(0);

            // 启动自动轮播
            if (carouselInterval) clearInterval(carouselInterval);
            carouselInterval = setInterval(() => {
                showSlide(currentSlide + 1);
            }, 6000);
        }

        // 轮播切换函数
        function showSlide(index) {
            const slides = document.querySelectorAll('.carousel-slide');
            const indicators = document.querySelectorAll('.indicator');
            
            // 边界处理
            if (index >= slides.length) currentSlide = 0;
            if (index < 0) currentSlide = slides.length - 1;
            else currentSlide = index;

            // 移动轮播
            carouselSlides.style.transform = `translateX(-${currentSlide * 100}%)`;

            // 更新指示器
            indicators.forEach((indicator, i) => {
                if (i === currentSlide) {
                    indicator.classList.add('active');
                } else {
                    indicator.classList.remove('active');
                }
            });
        }

        // 轮播按钮事件
        document.getElementById('nextBtn').addEventListener('click', () => {
            showSlide(currentSlide + 1);
        });

        document.getElementById('prevBtn').addEventListener('click', () => {
            showSlide(currentSlide - 1);
        });

        // 3. 背景音乐控制
        const musicBtn = document.getElementById('musicBtn');
        const backgroundMusic = document.getElementById('backgroundMusic');
        let isMusicPlaying = false;

        musicBtn.addEventListener('click', function() {
            if (isMusicPlaying) {
                backgroundMusic.pause();
                musicBtn.innerHTML = '🎵';
            } else {
                // 处理浏览器自动播放限制
                backgroundMusic.play().catch(err => {
                    alert('温馨提示：请点击页面任意位置后再尝试播放音乐（浏览器自动播放限制）');
                });
                musicBtn.innerHTML = '⏸️';
            }
            isMusicPlaying = !isMusicPlaying;
        });

        // 页面加载初始化
        window.addEventListener('load', function() {
            // 初始化背景粒子
            createParticles();
            // 初始化空轮播
            initEmptyCarousel();
            
            // 平滑滚动
            document.querySelectorAll('a[href^="#"]').forEach(anchor => {
                anchor.addEventListener('click', function (e) {
                    e.preventDefault();
                    document.querySelector(this.getAttribute('href')).scrollIntoView({
                        behavior: 'smooth'
                    });
                });
            });

            // 点击页面任意位置可播放音乐（解决自动播放限制）
            document.addEventListener('click', () => {
                if (!isMusicPlaying && backgroundMusic.paused) {
                    backgroundMusic.play().catch(() => {});
                }
            }, { once: true });
        });
    </script>
</body>
</html>
