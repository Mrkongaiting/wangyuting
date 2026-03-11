# wangyuting
<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>我们的恋爱回忆录 ❤️</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Microsoft YaHei', sans-serif;
        }

        /* 爱心背景样式 */
        body {
            background-color: #fdf2f8;
            overflow-x: hidden;
            position: relative;
            min-height: 100vh;
        }

        .heart-bg {
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
            background: rgba(255, 255, 255, 0.95);
            padding: 15px 0;
            box-shadow: 0 2px 10px rgba(236, 72, 153, 0.2);
            z-index: 100;
        }

        .nav-links {
            display: flex;
            justify-content: center;
            gap: 30px;
            flex-wrap: wrap;
        }

        .nav-links a {
            text-decoration: none;
            color: #e87ea1;
            font-size: 18px;
            font-weight: 600;
            padding: 8px 15px;
            border-radius: 20px;
            transition: all 0.3s ease;
        }

        .nav-links a:hover {
            background-color: #fce7f3;
            color: #ec4899;
            transform: translateY(-2px);
        }

        /* 主容器 */
        .container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 30px 20px;
            position: relative;
            z-index: 10;
        }

        /* 标题样式 */
        .title-section {
            text-align: center;
            margin-bottom: 40px;
            color: #be185d;
        }

        .title-section h1 {
            font-size: 36px;
            margin-bottom: 10px;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.1);
        }

        .title-section p {
            font-size: 18px;
            color: #9d174d;
        }

        /* 图片上传区域 */
        .upload-section {
            background: white;
            border-radius: 15px;
            padding: 30px;
            margin-bottom: 40px;
            box-shadow: 0 5px 15px rgba(236, 72, 153, 0.1);
            text-align: center;
        }

        .upload-section h2 {
            color: #db2777;
            margin-bottom: 20px;
            font-size: 24px;
        }

        .upload-btn {
            display: inline-block;
            background: #ec4899;
            color: white;
            padding: 12px 30px;
            border-radius: 30px;
            cursor: pointer;
            transition: all 0.3s ease;
            margin-bottom: 15px;
        }

        .upload-btn:hover {
            background: #db2777;
            transform: scale(1.05);
        }

        #file-input {
            display: none;
        }

        .upload-tips {
            color: #666;
            font-size: 14px;
        }

        /* 轮播区域 */
        .carousel-section {
            background: white;
            border-radius: 15px;
            padding: 30px;
            box-shadow: 0 5px 15px rgba(236, 72, 153, 0.1);
            margin-bottom: 40px;
        }

        .carousel-section h2 {
            color: #db2777;
            margin-bottom: 20px;
            text-align: center;
            font-size: 24px;
        }

        .carousel-container {
            position: relative;
            max-width: 800px;
            margin: 0 auto;
            overflow: hidden;
            border-radius: 10px;
        }

        .carousel-slides {
            display: flex;
            transition: transform 0.5s ease;
        }

        .carousel-slide {
            min-width: 100%;
            height: 500px;
            display: flex;
            justify-content: center;
            align-items: center;
        }

        .carousel-slide img {
            max-width: 100%;
            max-height: 100%;
            object-fit: contain;
            border-radius: 8px;
            box-shadow: 0 4px 8px rgba(0,0,0,0.1);
        }

        .carousel-nav {
            position: absolute;
            top: 50%;
            width: 100%;
            display: flex;
            justify-content: space-between;
            transform: translateY(-50%);
            padding: 0 20px;
        }

        .carousel-btn {
            width: 40px;
            height: 40px;
            border-radius: 50%;
            background: rgba(236, 72, 153, 0.8);
            color: white;
            border: none;
            cursor: pointer;
            display: flex;
            justify-content: center;
            align-items: center;
            font-size: 20px;
            transition: all 0.3s ease;
        }

        .carousel-btn:hover {
            background: #ec4899;
            transform: scale(1.1);
        }

        .carousel-indicators {
            position: absolute;
            bottom: 20px;
            left: 50%;
            transform: translateX(-50%);
            display: flex;
            gap: 10px;
        }

        .indicator {
            width: 12px;
            height: 12px;
            border-radius: 50%;
            background: rgba(255, 255, 255, 0.7);
            cursor: pointer;
            transition: all 0.3s ease;
        }

        .indicator.active {
            background: #ec4899;
            transform: scale(1.2);
        }

        /* 回忆章节区域 */
        .memories-section {
            background: white;
            border-radius: 15px;
            padding: 30px;
            box-shadow: 0 5px 15px rgba(236, 72, 153, 0.1);
        }

        .memories-section h2 {
            color: #db2777;
            margin-bottom: 20px;
            text-align: center;
            font-size: 24px;
        }

        .memory-card {
            margin-bottom: 30px;
            padding: 20px;
            border-left: 4px solid #ec4899;
            background: #fef7fb;
            border-radius: 8px;
        }

        .memory-card h3 {
            color: #be185d;
            margin-bottom: 10px;
            font-size: 20px;
        }

        .memory-card p {
            color: #333;
            line-height: 1.6;
        }

        /* 音乐控制 */
        .music-control {
            position: fixed;
            bottom: 30px;
            right: 30px;
            z-index: 100;
            background: rgba(236, 72, 153, 0.9);
            width: 60px;
            height: 60px;
            border-radius: 50%;
            display: flex;
            justify-content: center;
            align-items: center;
            color: white;
            cursor: pointer;
            box-shadow: 0 4px 12px rgba(236, 72, 153, 0.3);
            transition: all 0.3s ease;
        }

        .music-control:hover {
            transform: scale(1.1);
            background: #db2777;
        }

        /* 响应式适配 */
        @media (max-width: 768px) {
            .carousel-slide {
                height: 300px;
            }
            
            .title-section h1 {
                font-size: 28px;
            }
            
            .nav-links {
                gap: 15px;
            }
            
            .nav-links a {
                font-size: 16px;
            }
        }
    </style>
</head>
<body>
    <!-- 动态爱心背景 -->
    <div class="heart-bg" id="heartContainer"></div>

    <!-- 导航栏（组块跳转） -->
    <div class="nav-container">
        <div class="nav-links">
            <a href="#upload">上传照片</a>
            <a href="#carousel">甜蜜轮播</a>
            <a href="#memories">恋爱回忆</a>
        </div>
    </div>

    <!-- 主容器 -->
    <div class="container">
        <!-- 标题区域 -->
        <div class="title-section">
            <h1>我们的恋爱回忆录 ❤️</h1>
            <p>记录每一个心动的瞬间</p>
        </div>

        <!-- 图片上传区域 -->
        <div class="upload-section" id="upload">
            <h2>上传我们的甜蜜照片</h2>
            <label for="file-input" class="upload-btn">
                选择照片
            </label>
            <input type="file" id="file-input" accept="image/*" multiple>
            <p class="upload-tips">支持上传多张图片，格式为jpg、png等</p>
            <div id="preview-container" style="margin-top: 20px; display: flex; flex-wrap: wrap; gap: 10px; justify-content: center;"></div>
        </div>

        <!-- 轮播展示区域 -->
        <div class="carousel-section" id="carousel">
            <h2>我们的美好瞬间</h2>
            <div class="carousel-container">
                <div class="carousel-slides" id="carouselSlides">
                    <!-- 初始默认图片 -->
                    <div class="carousel-slide">
                        <img src="https://picsum.photos/800/500?random=1" alt="恋爱回忆">
                    </div>
                </div>
                <div class="carousel-nav">
                    <button class="carousel-btn" id="prevBtn">❮</button>
                    <button class="carousel-btn" id="nextBtn">❯</button>
                </div>
                <div class="carousel-indicators" id="carouselIndicators">
                    <div class="indicator active"></div>
                </div>
            </div>
        </div>

        <!-- 回忆章节区域 -->
        <div class="memories-section" id="memories">
            <h2>我们的恋爱故事</h2>
            <div class="memory-card">
                <h3>第一次相遇 💘</h3>
                <p>还记得我们第一次见面的场景吗？那一刻，时间仿佛静止，我的心跳开始加速，知道你就是我要找的那个人。</p>
            </div>
            <div class="memory-card">
                <h3>第一次约会 🥂</h3>
                <p>我们一起去了那家温馨的小店，聊着天，分享着彼此的故事，那一刻的美好至今难忘。</p>
            </div>
            <div class="memory-card">
                <h3>确定关系 💞</h3>
                <p>在那个浪漫的夜晚，我们确认了对彼此的心意，从此，我的世界多了一个你，也多了一份温暖。</p>
            </div>
        </div>
    </div>

    <!-- 音乐控制 -->
    <div class="music-control" id="musicBtn">
        🎵
    </div>

    <!-- 背景音乐元素 -->
    <audio id="backgroundMusic" loop>
        <!-- 这里替换成你喜欢的背景音乐URL -->
        <source src="https://music.163.com/song/media/outer/url?id=186016.mp3" type="audio/mpeg">
    </audio>

    <script>
        // 1. 动态爱心背景生成
        function createHearts() {
            const container = document.getElementById('heartContainer');
            setInterval(() => {
                const heart = document.createElement('div');
                // 随机大小
                const size = Math.random() * 20 + 10;
                // 随机位置
                const left = Math.random() * 100;
                // 随机颜色
                const colors = ['#ec4899', '#db2777', '#be185d', '#f472b6', '#fb7185'];
                const color = colors[Math.floor(Math.random() * colors.length)];
                
                heart.style.cssText = `
                    position: absolute;
                    left: ${left}%;
                    bottom: -${size}px;
                    font-size: ${size}px;
                    color: ${color};
                    opacity: ${Math.random() * 0.8 + 0.2};
                    transform: rotate(${Math.random() * 360}deg);
                    pointer-events: none;
                    animation: floatUp linear ${Math.random() * 10 + 10}s forwards;
                `;
                
                heart.innerHTML = '❤️';
                container.appendChild(heart);
                
                // 动画结束后移除元素
                setTimeout(() => {
                    heart.remove();
                }, 20000);
            }, 300);
        }

        // 添加爱心上浮动画
        const style = document.createElement('style');
        style.textContent = `
            @keyframes floatUp {
                0% {
                    bottom: -20px;
                    opacity: 0.8;
                }
                100% {
                    bottom: 100%;
                    opacity: 0;
                }
            }
        `;
        document.head.appendChild(style);

        // 2. 图片上传和预览功能
        const fileInput = document.getElementById('file-input');
        const previewContainer = document.getElementById('preview-container');
        const carouselSlides = document.getElementById('carouselSlides');
        const carouselIndicators = document.getElementById('carouselIndicators');
        let uploadedImages = [];

        fileInput.addEventListener('change', function(e) {
            const files = e.target.files;
            if (files.length === 0) return;

            // 清空原有预览（保留轮播）
            previewContainer.innerHTML = '';

            // 处理每个文件
            for (let i = 0; i < files.length; i++) {
                const file = files[i];
                if (!file.type.startsWith('image/')) continue;

                const reader = new FileReader();
                reader.onload = function(event) {
                    // 保存图片URL
                    uploadedImages.push(event.target.result);
                    
                    // 创建预览缩略图
                    const previewImg = document.createElement('img');
                    previewImg.src = event.target.result;
                    previewImg.style.width = '100px';
                    previewImg.style.height = '100px';
                    previewImg.style.objectFit = 'cover';
                    previewImg.style.borderRadius = '8px';
                    previewContainer.appendChild(previewImg);

                    // 更新轮播
                    updateCarousel();
                };
                reader.readAsDataURL(file);
            }
        });

        // 更新轮播函数
        function updateCarousel() {
            if (uploadedImages.length === 0) return;

            // 清空原有轮播
            carouselSlides.innerHTML = '';
            carouselIndicators.innerHTML = '';

            // 添加新图片到轮播
            uploadedImages.forEach((imgSrc, index) => {
                // 创建轮播项
                const slide = document.createElement('div');
                slide.className = 'carousel-slide';
                slide.innerHTML = `<img src="${imgSrc}" alt="我们的回忆 ${index + 1}">`;
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
        }

        // 3. 轮播控制
        let currentSlide = 0;

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
                indicator.classList.toggle('active', i === currentSlide);
            });
        }

        // 下一张/上一张按钮
        document.getElementById('nextBtn').addEventListener('click', () => {
            showSlide(currentSlide + 1);
        });

        document.getElementById('prevBtn').addEventListener('click', () => {
            showSlide(currentSlide - 1);
        });

        // 自动轮播
        setInterval(() => {
            showSlide(currentSlide + 1);
        }, 5000);

        // 4. 背景音乐控制
        const musicBtn = document.getElementById('musicBtn');
        const backgroundMusic = document.getElementById('backgroundMusic');
        let isMusicPlaying = false;

        musicBtn.addEventListener('click', function() {
            if (isMusicPlaying) {
                backgroundMusic.pause();
                musicBtn.innerHTML = '🎵';
            } else {
                backgroundMusic.play().catch(err => {
                    alert('请点击页面任意位置后再尝试播放音乐（浏览器自动播放限制）');
                });
                musicBtn.innerHTML = '⏸️';
            }
            isMusicPlaying = !isMusicPlaying;
        });

        // 页面加载完成后初始化
        window.addEventListener('load', function() {
            createHearts();
            showSlide(0);
            
            // 平滑滚动（组块跳转）
            document.querySelectorAll('a[href^="#"]').forEach(anchor => {
                anchor.addEventListener('click', function (e) {
                    e.preventDefault();
                    document.querySelector(this.getAttribute('href')).scrollIntoView({
                        behavior: 'smooth'
                    });
                });
            });
        });
    </script>
</body>
</html>
