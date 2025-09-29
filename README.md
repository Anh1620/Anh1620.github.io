<!DOCTYPE html>
<html lang="vi">
<head>
c
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>CMSN</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }

        body {
            background: linear-gradient(135deg, #ff9a9e 0%, #fad0c4 100%);
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            padding: 20px;
            overflow-x: hidden;
        }

        .container {
            max-width: 1200px;
            width: 100%;
            background: rgba(255, 255, 255, 0.9);
            border-radius: 20px;
            box-shadow: 0 15px 30px rgba(0, 0, 0, 0.2);
            overflow: hidden;
            position: relative;
        }

        .password-screen {
            padding: 40px;
            text-align: center;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            min-height: 500px;
        }

        .password-screen h1 {
            color: #ff4081;
            margin-bottom: 20px;
            font-size: 2.5rem;
        }

        .password-screen p {
            color: #666;
            margin-bottom: 30px;
            font-size: 1.1rem;
        }

        .password-input {
            width: 100%;
            max-width: 300px;
            padding: 15px;
            border: 2px solid #ffb6c1;
            border-radius: 10px;
            font-size: 1rem;
            margin-bottom: 20px;
            text-align: center;
            transition: all 0.3s;
        }

        .password-input:focus {
            outline: none;
            border-color: #ff4081;
            box-shadow: 0 0 10px rgba(255, 64, 129, 0.3);
        }

        .submit-btn {
            background: linear-gradient(to right, #ff6b6b, #ff8e8e);
            color: white;
            border: none;
            padding: 15px 30px;
            border-radius: 10px;
            font-size: 1.1rem;
            cursor: pointer;
            transition: transform 0.3s, box-shadow 0.3s;
            width: 100%;
            max-width: 300px;
            margin-bottom: 15px;
        }

        .submit-btn:hover {
            transform: translateY(-3px);
            box-shadow: 0 7px 15px rgba(255, 107, 107, 0.4);
        }

        .error-msg {
            color: #ff4081;
            margin-top: 15px;
            font-weight: bold;
            display: none;
        }

        /* bàn phím số */
        .numeric-keypad {
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 10px;
            max-width: 300px;
            width: 100%;
            margin-top: 15px;
        }

        .keypad-btn {
            background: linear-gradient(to bottom, #ffffff, #f0f0f0);
            border: 1px solid #ddd;
            border-radius: 8px;
            padding: 15px;
            font-size: 1.2rem;
            cursor: pointer;
            transition: all 0.2s;
            box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
        }

        .keypad-btn:hover {
            background: linear-gradient(to bottom, #f0f0f0, #e0e0e0);
            transform: translateY(-2px);
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.15);
        }

        .keypad-btn:active {
            transform: translateY(0);
            box-shadow: 0 1px 3px rgba(0, 0, 0, 0.1);
        }

        .keypad-clear {
            grid-column: span 2;
            background: linear-gradient(to right, #ff6b6b, #ff8e8e);
            color: white;
        }

        .keypad-enter {
            background: linear-gradient(to right, #4ecdc4, #6ae3d9);
            color: white;
        }

        /* trang chọn lựa */
        .selection-screen {
            display: none;
            padding: 40px;
            text-align: center;
            min-height: 500px;
            flex-direction: column;
            justify-content: center;
            align-items: center;
        }

        .selection-screen h1 {
            color: #ff4081;
            margin-bottom: 40px;
            font-size: 2.5rem;
        }

        .selection-container {
            display: flex;
            justify-content: center;
            align-items: center;
            gap: 60px;
            flex-wrap: wrap;
            margin-top: 20px;
        }

        .selection-item {
            display: flex;
            flex-direction: column;
            align-items: center;
            cursor: pointer;
            transition: all 0.5s ease;
            padding: 20px;
            border-radius: 15px;
            background: rgba(255, 255, 255, 0.7);
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1);
        }

        .selection-item:hover {
            transform: translateY(-10px);
            background: rgba(255, 255, 255, 0.9);
            box-shadow: 0 10px 25px rgba(0, 0, 0, 0.2);
        }

        .selection-icon {
            font-size: 5rem;
            margin-bottom: 15px;
            transition: all 0.5s ease;
        }

        .selection-label {
            font-size: 1.3rem;
            color: #ff4081;
            font-weight: bold;
        }

        .selection-item.active {
            transform: scale(1.3);
            z-index: 10;
            background: white;
            box-shadow: 0 15px 30px rgba(0, 0, 0, 0.3);
        }

        /* trang pass */
        .main-content {
            display: none;
            padding: 30px;
            position: relative;
            overflow: hidden;
        }

        .header {
            text-align: center;
            margin-bottom: 30px;
        }

        .header h1 {
            color: #ff4081;
            font-size: 2.8rem;
            margin-bottom: 10px;
            text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.1);
        }

        .header p {
            color: #666;
            font-size: 1.2rem;
        }

        /* Container cho 4 thiệp */
        .books-container {
            display: flex;
            flex-wrap: wrap;
            justify-content: center;
            gap: 30px;
            margin-bottom: 30px;
        }

        .book-container {
            display: flex;
            flex-direction: column;
            align-items: center;
            margin-bottom: 20px;
        }

        .book-title {
            margin-bottom: 10px;
            font-size: 1.2rem;
            color: #ff4081;
            font-weight: bold;
        }

        .book {
            position: relative;
            width: 250px;
            height: 320px;
            perspective: 1200px;
            cursor: pointer;
        }

        .page {
            position: absolute;
            width: 100%;
            height: 100%;
            background: white;
            border-radius: 10px;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.2);
            transform-origin: left center;
            transition: transform 1.5s ease-in-out;
            backface-visibility: hidden;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            padding: 30px;
            text-align: center;
            overflow: hidden;
        }

        .page1 {
            background: linear-gradient(135deg, #ffecd2 0%, #fcb69f 100%);
            z-index: 2;
            font-size: 1.5rem;
            color: #ff4081;
            font-weight: bold;
        }

        .page2 {
            background: repeating-linear-gradient(
                to bottom,
                white 0px,
                white 23px,
                #f0f0f0 24px
            );
            font-size: 1rem;
            color: #333;
            text-align: left;
            z-index: 1;
            line-height: 24px;
            font-family: "Courier New", monospace;
            position: relative;
            padding: 40px 30px;
            word-wrap: break-word;
            word-break: break-word;
            white-space: normal;
            overflow-wrap: break-word;
        }

        .page2 .line {
            min-height: 24px;
            width: 100%;
            word-wrap: break-word;
            word-break: keep-all;
            overflow-wrap: break-word;
            white-space: normal;
            position: relative;
            margin-bottom: 0;
        }

        .book.opened .page1 {
            transform: rotateY(-150deg);
            opacity: 1;
            z-index: 2;
        }

        .controls {
            text-align: center;
            margin-bottom: 30px;
        }

        .btn {
            padding: 12px 25px;
            font-size: 1.1rem;
            border: none;
            border-radius: 8px;
            color: white;
            cursor: pointer;
            transition: transform 0.3s, box-shadow 0.3s;
            margin: 0 10px;
        }

        .next-btn {
            background: linear-gradient(to right, #ff6b6b, #ff8e8e);
        }

        .back-btn {
            background: linear-gradient(to right, #4ecdc4, #6ae3d9);
        }

        .btn:hover {
            transform: translateY(-3px);
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.2);
        }

        /* trang video */
        .video-screen {
            display: none;
            padding: 30px;
            text-align: center;
        }

        .video-container {
            max-width: 800px;
            margin: 0 auto;
        }

        .video-player {
            width: 100%;
            max-width: 700px;
            height: 400px;
            background: #000;
            border-radius: 10px;
            margin: 20px auto;
            display: flex;
            justify-content: center;
            align-items: center;
            color: white;
            font-size: 1.2rem;
            position: relative;
            overflow: hidden;
        }

        .video-player video {
            width: 100%;
            height: 100%;
            object-fit: cover;
        }

        .video-placeholder {
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            width: 100%;
            height: 100%;
            background: linear-gradient(135deg, #ff9a9e 0%, #fad0c4 100%);
        }

        .video-placeholder p {
            margin-bottom: 15px;
        }

        .video-controls {
            margin-top: 15px;
            display: flex;
            justify-content: center;
            gap: 10px;
        }

        /* trang ảnh */
        .gallery-screen {
            display: none;
            padding: 30px;
            text-align: center;
            overflow: hidden;
            position: relative;
            min-height: 600px;
        }

        .gallery-container {
            position: relative;
            width: 100%;
            height: 500px;
            overflow: hidden;
            margin-bottom: 20px;
            border-radius: 10px;
            background: rgba(255, 255, 255, 0.3);
        }

        .gallery-image {
            position: absolute;
            width: 180px;
            height: 180px;
            object-fit: cover;
            border-radius: 10px;
            box-shadow: 0 8px 16px rgba(0, 0, 0, 0.3);
            transition: transform 0.3s, z-index 0.3s;
            cursor: pointer;
            right: -200px; /* tọa độ từ bên phải */
            animation-timing-function: linear;
            animation-iteration-count: infinite;
        }

        .gallery-image:hover {
            transform: scale(1.05);
            z-index: 100;
            animation-play-state: paused; /* tương tác vs ảnh */
        }

        /* Keyframes ảnh di chuyển */
        @keyframes moveLeft {
            0% {
                transform: translateX(0) rotate(0deg);
                right: -200px;
            }
            100% {
                transform: translateX(calc(-100vw - 200px)) rotate(0deg);
                right: calc(100vw + 200px);
            }
        }

        @keyframes moveLeftSlow {
            0% {
                transform: translateX(0) rotate(0deg);
                right: -200px;
            }
            100% {
                transform: translateX(calc(-100vw - 200px)) rotate(0deg); 
                right: calc(100vw + 200px);
            }
        }

        @keyframes moveLeftZigzag {
            0% {
                transform: translateX(0) translateY(0) rotate(0deg);
                right: -200px;
            }
            25% {
                transform: translateX(-25vw) translateY(-50px) rotate(0deg); 
            }
            50% {
                transform: translateX(-50vw) translateY(0) rotate(0deg); 
            }
            75% {
                transform: translateX(-75vw) translateY(50px) rotate(0deg); 
            }
            100% {
                transform: translateX(calc(-100vw - 200px)) translateY(0) rotate(0deg); 
                right: calc(100vw + 200px);
            }
        }

        .confetti {
            position: fixed;
            width: 10px;
            height: 10px;
            background-color: #f00;
            opacity: 0.7;
            z-index: 1000;
        }

        .pen {
            position: absolute;
            font-size: 24px;
            display: none;
            transition: left 0.05s linear, top 0.05s linear;
            z-index: 10;
            pointer-events: none;
        }

        /* hiệu ứng bóng bay */
        .balloon {
            position: absolute;
            width: 40px;
            height: 50px;
            border-radius: 50%;
            z-index: 999;
            pointer-events: none;
            opacity: 0.8;
            animation: floatUp 8s ease-in forwards;
        }

        .balloon::before {
            content: '';
            position: absolute;
            bottom: -15px;
            left: 50%;
            transform: translateX(-50%);
            width: 2px;
            height: 15px;
            background-color: rgba(0, 0, 0, 0.3);
        }

        .balloon::after {
            content: '';
            position: absolute;
            bottom: -20px;
            left: 50%;
            transform: translateX(-50%);
            width: 6px;
            height: 6px;
            border-radius: 50%;
            background-color: rgba(0, 0, 0, 0.2);
        }

        @keyframes floatUp {
            0% {
                transform: translateY(0) rotate(0deg);
                opacity: 0.8;
            }
            100% {
                transform: translateY(-100vh) rotate(10deg);
                opacity: 0;
            }
        }

        @keyframes shake {
            0%, 100% {
                transform: translateX(0);
            }
            10%, 30%, 50%, 70%, 90% {
                transform: translateX(-5px);
            }
            20%, 40%, 60%, 80% {
                transform: translateX(5px);
            }
        }

        .notification {
            position: fixed;
            bottom: 20px;
            left: 50%;
            transform: translateX(-50%);
            background: rgba(0, 0, 0, 0.7);
            color: white;
            padding: 10px 20px;
            border-radius: 5px;
            z-index: 1000;
            display: none;
        }

        /* Ẩn audio player hoàn toàn */
        .audio-player {
            display: none;
        }

        /* hiệu ứng kim tuyến */
        .glitter {
            position: fixed;
            width: 5px;
            height: 5px;
            background-color: gold;
            border-radius: 50%;
            pointer-events: none;
            z-index: 999;
            opacity: 0.8;
            box-shadow: 0 0 10px 2px rgba(255, 215, 0, 0.7);
        }

        @media (max-width: 768px) {
            .container {
                border-radius: 10px;
            }
            
            .header h1 {
                font-size: 2rem;
            }
            
            .book {
                width: 200px;
                height: 260px;
            }
            
            .page1 {
                font-size: 1.2rem;
            }
            
            .page2 {
                font-size: 0.9rem;
                padding: 30px 20px;
            }
            
            .books-container {
                gap: 15px;
            }
            
            .selection-container {
                gap: 30px;
            }
            
            .selection-icon {
                font-size: 4rem;
            }
            
            .video-player {
                height: 250px;
            }
            
            .gallery-image {
                width: 140px;
                height: 140px;
            }
            
            .video-controls {
                flex-direction: column;
                align-items: center;
            }
            
            .gallery-screen {
                min-height: 500px;
            }
            
            .gallery-container {
                height: 400px;
            }
            
            .numeric-keypad {
                max-width: 280px;
            }
            
            .keypad-btn {
                padding: 12px;
                font-size: 1.1rem;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <!-- màn hình nhập mật khẩu -->
        <div class="password-screen" id="passwordScreen">
            <h1>🎂 HAPPY BIRTHDAY 🎉</h1>
            <p>Nhập mật khẩu để mở</p>
            <input type="password" class="password-input" id="passwordInput" placeholder="Nhập mật khẩu" readonly>
            <button class="submit-btn" onclick="checkPassword()">Xác Nhận</button>
            <p class="error-msg" id="errorMsg">Mật khẩu không đúng. Vui lòng thử lại!</p>
            
            <!-- bàn phím số -->
            <div class="numeric-keypad">
                <button class="keypad-btn" data-value="1">1</button>
                <button class="keypad-btn" data-value="2">2</button>
                <button class="keypad-btn" data-value="3">3</button>
                <button class="keypad-btn" data-value="4">4</button>
                <button class="keypad-btn" data-value="5">5</button>
                <button class="keypad-btn" data-value="6">6</button>
                <button class="keypad-btn" data-value="7">7</button>
                <button class="keypad-btn" data-value="8">8</button>
                <button class="keypad-btn" data-value="9">9</button>
                <button class="keypad-btn keypad-clear" onclick="clearPassword()">Xóa</button>
                <button class="keypad-btn" data-value="0">0</button>
            
            </div>
        </div>

        <!-- màn hình chọn lựa -->
        <div class="selection-screen" id="selectionScreen">
            <h1>Chọn một mục để khám phá</h1>
            <div class="selection-container">
                <div class="selection-item" id="videoSelection" onclick="selectItem('video')">
                    <div class="selection-icon">📹</div>
                    <div class="selection-label">Video</div>
                </div>
                
                <div class="selection-item" id="cardSelection" onclick="selectItem('card')">
                    <div class="selection-icon">💌</div>
                    <div class="selection-label">Thiệp</div>
                </div>
                
                <div class="selection-item" id="gallerySelection" onclick="selectItem('gallery')">
                    <div class="selection-icon">📷</div>
                    <div class="selection-label">Ảnh</div>
                </div>
            </div>
        </div>

        <!-- trang thiệp chúc mừng -->
        <div class="main-content" id="mainContent">
            <div class="header">
                <h1>HAPPY BIRTHDAY 🎂</h1>
                <p>Nhấn vào từng cái để mở </p> 
            </div>

            <div class="books-container">
                <div class="book-container">
                    <div class="book-title"></div>
                    <div class="book" id="book1" onclick="openBook(1)">
                        <div class="page page1">
                            <div>HAPPY BIRTHDAY</div>
                            <div style="font-size: 3rem; margin-top: 20px;">🎁</div>
                        </div>
                        <div class="page page2" id="page2-book1">
                            <div id="messageContent1"></div>
                            <span class="pen" id="pen1">✏️</span>
                        </div>
                    </div>
                </div>

                <div class="book-container">
                    <div class="book-title"></div>
                    <div class="book" id="book2" onclick="openBook(2)">
                        <div class="page page1">
                            <div>HAPPY BIRTHDAY</div>
                            <div style="font-size: 3rem; margin-top: 20px;">💌</div>
                        </div>
                        <div class="page page2" id="page2-book2">
                            <div id="messageContent2"></div>
                            <span class="pen" id="pen2">✏️</span>
                        </div>
                    </div>
                </div>

                <div class="book-container">
                    <div class="book-title"></div>
                    <div class="book" id="book3" onclick="openBook(3)">
                        <div class="page page1">
                            <div>HAPPY BIRTHDAY</div>
                            <div style="font-size: 3rem; margin-top: 20px;">🎂</div>
                        </div>
                        <div class="page page2" id="page2-book3">
                            <div id="messageContent3"></div>
                            <span class="pen" id="pen3">✏️</span>
                        </div>
                    </div>
                </div>
                
                <div class="book-container">
                    <div class="book-title"></div>
                    <div class="book" id="book4" onclick="openBook(4)">
                        <div class="page page1">
                            <div>HAPPY BIRTHDAY</div>
                            <div style="font-size: 3rem; margin-top: 20px;">🎉</div>
                        </div>
                        <div class="page page2" id="page2-book4">
                            <div id="messageContent4"></div>
                            <span class="pen" id="pen4">✏️</span>
                        </div>
                    </div>
                </div>
            </div>

            <div class="controls">
                <button class="btn back-btn" onclick="goBackToSelection()">Quay lại</button>
                <button class="btn next-btn" id="nextButton" onclick="showCompletionMessage()">Hoàn thành 🎊</button>
            </div>
        </div>

        <!-- trang video -->
        <div class="video-screen" id="videoScreen">
            <div class="header">
                <h1>Video 🎬</h1>
            </div>
            
            <div class="video-container">
                <div class="video-player" id="videoPlayer">
                   
                </div>
                <!-- nút đk video -->
                <div class="video-controls" id="videoControls">
                    <button class="btn prev-video-btn" style="background: linear-gradient(to right, #4ecdc4, #6ae3d9)">⏮ Video trước</button>
                    <button class="btn next-video-btn" style="background: linear-gradient(to right, #ff6b6b, #ff8e8e)">Video tiếp theo ⏭</button>
                </div>
            </div>
            
            <div class="controls">
                <button class="btn back-btn" onclick="goBackToSelection()">Quay lại</button>
            </div>
        </div>

        <!-- Trang ảnh -->
        <div class="gallery-screen" id="galleryScreen">
            <div class="header">
                <h1>Ảnh 📸</h1>
            </div>
            
            <div class="gallery-container" id="galleryContainer">
               
            </div>
            
            <div class="controls">
                <button class="btn back-btn" onclick="goBackToSelection()">Quay lại</button>
            </div>
        </div>
    </div>

    <div class="notification" id="notification"></div>

    <div class="audio-player" id="audioPlayer"></div>

    <script>
        // PASS
        const PASSWORD = "1";
        
        // thông báo khi mở thiệp 
        const OPEN_MESSAGE_CONFIG = {
            book1: "ANH",
            book2: "DOAN", 
            book3: "QUANG",
            book4: "ANH1628",
            allOpened: "Đã mở tất cả thiệp! 🎉"
        };
        
        // lời chúc
        const bookMessages = [
            "lời chúc 1",
            
            "lời chúc 2",
            
            "lời chúc 3",
            
            "lời chúc 4"
        ];

        // tên thiệp
        const bookTitles = [
           // thêm theo "Thiệp 1",//
    
        ];

        // ảnh
        const localImages = [
            "1.jpg", "2.jpg", "3.jpg", '4.jpg', '5.jpg', '6.jpg', '7.jpg', "8.jpg", "9.jpg", "10.jpg",
            '11.jpg', '12.jpg', '13.jpg', '14.jpg', "15.jpg", "16.jpg", "17.jpg", '18.jpg', '19.jpg', '20.jpg',
            '21.jpg', "22.jpg", "23.jpg", "24.jpg", '25.jpg', '26.jpg', '27.jpg', '28.jpg', "29.jpg", "30.jpg",
            "31.jpg", '32.jpg', '33.jpg', '34.jpg', '35.jpg', "36.jpg", "37.jpg", "38.jpg", '39.jpg', '40.jpg', 
            '41.jpg', '42.jpg', '43.jpg', '44.jpg', '45.jpg', '46.jpg', '47.jpg', '48.jpg', '49.jpg', '50.jpg',
            '51.jpg', '52.jpg', '53.jpg', '54.jpg', '55.jpg', '56.jpg', '57.jpg'
        ];

        //video
        const localVideos = [
    
            "v1.mp4",
            "v2.mp4",
            "v3.mp4",
            "v4.mp4",
            "v5.mp4",
            "v6.mp4",
            "v7.mp4"
            
        ]; 

        // file nhạc
        const MUSIC_FILE = "sn.mp3"; 
        
        // Biến toàn cục
        let glitterInterval;
        let effectsActive = false;
        let openedBooks = 0;
        let selectedItem = null;
        let selectionTimeout;
        let currentVideoIndex = 0;
        let imageInterval;
        let balloonInterval;

        let birthdayAudio = new Audio();
        let isPlaying = false;
        const DEFAULT_VOLUME = 0.7;  // chỉnh âm thanh

        // cập nhật tên thiệp
        function updateBookTitles() {
            const bookTitleElements = document.querySelectorAll('.book-title');
            bookTitleElements.forEach((element, index) => {
                if (bookTitles[index]) {
                    element.textContent = bookTitles[index];
                }
            });
        }

        // tự động phát nhạc
        function playAudioAutomatically() {
            if (birthdayAudio.src) {
                birthdayAudio.play().then(() => {
                    isPlaying = true;
                    console.log("Nhạc đang phát tự động");
                }).catch(error => {
                    console.error("Lỗi tự động phát nhạc:", error);
                    setTimeout(playAudioAutomatically, 1000);
                });
            }
        }

        // chuyển đổi tên file thành đường dẫn ảnh
        function processLocalImages() {
            const processedImages = [];
            
            for (const fileName of localImages) {
                processedImages.push({
                    src: fileName,
                    name: fileName.replace(/\.[^/.]+$/, "")
                });
            }
            
            return processedImages;
        }

        // chuyển đổi tên file thành đường dẫn video
        function processLocalVideos() {
            const processedVideos = [];
            
            for (const fileName of localVideos) {
                processedVideos.push({
                    src: fileName,
                    name: fileName.replace(/\.[^/.]+$/, "")
                });
            }
            
            return processedVideos;
        }

        // Cập nhật gallery ảnh di chuyển liên tục
        function updateImageGallery() {
            const galleryContainer = document.getElementById('galleryContainer');
            if (!galleryContainer) return;
            
            galleryContainer.innerHTML = '';
            
            const processedImages = processLocalImages();
            
            if (processedImages.length > 0) {
                // tạo ảnh với hiệu ứng di chuyển liên tục
                processedImages.forEach((image, index) => {
                    const imgElement = document.createElement('img');
                    imgElement.src = image.src;
                    imgElement.alt = image.name;
                    imgElement.className = 'gallery-image';
                    imgElement.title = image.name;
                    
                    
                    const randomTop = Math.random() * 300; // vị trí 
                    const randomDelay = Math.random() * 2; // độ trễ 
                    const randomDuration = 15 + Math.random() * 15; // thời gian di chuyển
                    const randomZIndex = Math.floor(Math.random() * 6) + 1; // z-index ngẫu nhiên
                    
                    // di chuyển ngẫu nhiên
                    const animationTypes = ['moveLeft', 'moveLeftSlow', 'moveLeftZigzag'];
                    const randomAnimation = animationTypes[Math.floor(Math.random() * animationTypes.length)];
                    
                    imgElement.style.top = randomTop + 'px';
                    imgElement.style.zIndex = randomZIndex;
                    imgElement.style.animationDelay = randomDelay + 's';
                    imgElement.style.animationDuration = randomDuration + 's';
                    imgElement.style.animationName = randomAnimation;
                    
                    imgElement.onerror = function() {
                        console.error(`Không thể tải ảnh: ${image.src}`);
                        this.style.display = 'none';
                    };
                    
                    galleryContainer.appendChild(imgElement);
                });
            } else {
                // thông báo khi ko cs ảnh
                const noImagesMsg = document.createElement('p');
                noImagesMsg.textContent = "Chưa có ảnh kỷ niệm nào";
                noImagesMsg.style.color = "#666";
                noImagesMsg.style.fontSize = "1.2rem";
                noImagesMsg.style.padding = "50px";
                galleryContainer.appendChild(noImagesMsg);
            }
        }

        // Dừng ảnh
        function stopImageMovement() {
            const images = document.querySelectorAll('.gallery-image');
            images.forEach(img => {
                img.style.animation = 'none';
            });
        }

        // Cập nhật phát video
        function updateVideoPlayer() {
            const videoPlayer = document.getElementById('videoPlayer');
            const videoControls = document.getElementById('videoControls');
            
            if (!videoPlayer) return;
            
            videoPlayer.innerHTML = '';
            
            const processedVideos = processLocalVideos();
            
            // Ẩn/hiện điều khiển dựa trên số lượng video
            if (videoControls) {
                videoControls.style.display = processedVideos.length > 1 ? 'flex' : 'none';
            }
            
            if (processedVideos.length > 0) {
                // video
                const videoElement = document.createElement('video');
                videoElement.controls = true;
                videoElement.autoplay = false;
                videoElement.style.width = '100%';
                videoElement.style.height = '100%';
                videoElement.style.objectFit = 'cover';
                
                //nguồn video
                const sourceElement = document.createElement('source');
                sourceElement.src = processedVideos[currentVideoIndex].src;
                sourceElement.type = 'video/mp4';
                
                videoElement.appendChild(sourceElement);
                
                //  thông báo web không hỗ trợ video
                const fallbackText = document.createElement('p');
                fallbackText.textContent = "Trình duyệt không hỗ trợ video.";
                videoElement.appendChild(fallbackText);
                
                // xử lý lỗi tải video
                videoElement.onerror = function() {
                    console.error(`Không thể tải video: ${processedVideos[currentVideoIndex].src}`);
                    showVideoPlaceholder(`Không thể tải video: ${processedVideos[currentVideoIndex].src}`);
                };
                
                videoPlayer.appendChild(videoElement);
            } else {
                // thông báo khi ko cs video, 
                showVideoPlaceholder("Chưa có video nào");
            }
        }

        // Hiển thị placeholder khi ko cs video
        function showVideoPlaceholder(message) {
            const videoPlayer = document.getElementById('videoPlayer');
            if (!videoPlayer) return;
            
            videoPlayer.innerHTML = '';
            
            const placeholder = document.createElement('div');
            placeholder.className = 'video-placeholder';
            
            const icon = document.createElement('div');
            icon.style.fontSize = '4rem';
            icon.textContent = '📹';
            
            const text = document.createElement('p');
            text.textContent = message;
            text.style.fontSize = '1.2rem';
            text.style.marginTop = '15px';
            
            placeholder.appendChild(icon);
            placeholder.appendChild(text);
            
            videoPlayer.appendChild(placeholder);
        }

        // số vào ô mk
        function addToPassword(value) {
            const passwordInput = document.getElementById('passwordInput');
            passwordInput.value += value;
        }

        // xóa mật khẩu
        function clearPassword() {
            const passwordInput = document.getElementById('passwordInput');
            passwordInput.value = '';
        }

        window.onload = function() {
            // thêm sự kiện cho bàn phím số
            document.querySelectorAll('.keypad-btn[data-value]').forEach(button => {
                button.addEventListener('click', function() {
                    addToPassword(this.getAttribute('data-value'));
                });
            });

            // dấu enter trên trang 1
            document.getElementById("passwordInput").addEventListener("keypress", function(event) {
                if (event.key === "Enter") {
                    checkPassword();
                }
            });
            
            updateBookTitles(); // cập nhật tên thiệp
            updateImageGallery(); // cập nhật gallery ảnh
            updateVideoPlayer(); // cập nhật trình phát video

            // gán sự kiện cho nút điều khiển video
            const prevBtn = document.querySelector('.prev-video-btn');
            const nextBtn = document.querySelector('.next-video-btn');
            
            if (prevBtn) {
                prevBtn.onclick = function() {
                    const processedVideos = processLocalVideos();
                    if (processedVideos.length > 0) {
                        currentVideoIndex = (currentVideoIndex - 1 + processedVideos.length) % processedVideos.length;
                        updateVideoPlayer();
                    }
                };
            }
            
            if (nextBtn) {
                nextBtn.onclick = function() {
                    const processedVideos = processLocalVideos();
                    if (processedVideos.length > 0) {
                        currentVideoIndex = (currentVideoIndex + 1) % processedVideos.length;
                        updateVideoPlayer();
                    }
                };
            }
            
            setupAudio();
        };

        // chạy audio
        function setupAudio() {
            if (MUSIC_FILE) {
                birthdayAudio.src = MUSIC_FILE;
                console.log(`Đã chạy file nhạc: ${MUSIC_FILE}`);
            } else {
                console.log("Không có file nhạc ");
            }
            
            birthdayAudio.loop = true;
            birthdayAudio.volume = DEFAULT_VOLUME;

            birthdayAudio.addEventListener('canplaythrough', function() {
                console.log("Nhạc đã sẵn sàng để phát");
            });

            birthdayAudio.addEventListener('error', function() {
                console.error("Không thể tải file nhạc:", MUSIC_FILE);
                showNotification(`Không thể tải nhạc: ${MUSIC_FILE}. Vui lòng kiểm tra file!`);
            });

            birthdayAudio.addEventListener('ended', function() {
                if (birthdayAudio.loop) {
                    birthdayAudio.currentTime = 0;
                    birthdayAudio.play();
                }
            });
        }

        // hiển thị thông báo
        function showNotification(msg) {
            const notification = document.getElementById('notification');
            notification.textContent = msg;
            notification.style.display = 'block';
            
            setTimeout(() => {
                notification.style.display = 'none';
            }, 3000);
        }

        // check mk
        function checkPassword() {
            const input = document.getElementById("passwordInput").value.trim().toLowerCase();
            const errorMsg = document.getElementById("errorMsg");
            
            if (input === PASSWORD) {
                document.getElementById("passwordScreen").style.display = "none";
                document.getElementById("selectionScreen").style.display = "flex";
                createConfetti(30);
                showNotification("Mật khẩu đúng. 🎉");
                
                // chạy kim tuyến 
                startEffects();
                
                // tự động phát nhạc
                setTimeout(() => {
                    if (birthdayAudio.src) {
                        playAudioAutomatically();
                    } else {
                        showNotification("Không có file nhạc để phát");
                    }
                }, 500);
            } else {
                errorMsg.style.display = "block";
                document.getElementById("passwordInput").style.animation = "shake 0.5s";
                setTimeout(() => {
                    document.getElementById("passwordInput").style.animation = "";
                }, 500);
            }
        }

        // chọn một mục từ màn hình
        function selectItem(itemType) {
            // Xóa timeout cũ nếu có
            if (selectionTimeout) {
                clearTimeout(selectionTimeout);
            }
            
            // xóa lớp active khỏi tất cả các mục
            document.querySelectorAll('.selection-item').forEach(item => {
                item.classList.remove('active');
            });
            
            // Thêm lớp active vào mục được chọn
            selectedItem = itemType;
            const selectedElement = document.getElementById(itemType + 'Selection');
            selectedElement.classList.add('active');
            
            // Chuyển hướng sau hiệu ứng phóng to
            selectionTimeout = setTimeout(() => {
                switch(itemType) {
                    case 'video':
                        showVideoScreen();
                        break;
                    case 'card':
                        showCardScreen();
                        break;
                    case 'gallery':
                        showGalleryScreen();
                        // Cập nhật gallery khi vào trang ảnh
                        setTimeout(() => {
                            updateImageGallery();
                        }, 100);
                        break;
                }
            }, 800);
        }

        // Hiển thị màn hình video
        function showVideoScreen() {
            document.getElementById("selectionScreen").style.display = "none";
            document.getElementById("videoScreen").style.display = "block";
            // Cập nhật lại video player khi chuyển đến trang video
            updateVideoPlayer();
        }

        // Hiển thị màn hình thiệp
        function showCardScreen() {
            document.getElementById("selectionScreen").style.display = "none";
            document.getElementById("mainContent").style.display = "block";
            
            // Bắt đầu hiệu ứng bóng bay khi vào trang thiệp
            startBalloonEffect();
        }

        // Hiển thị màn hình ảnh kỷ niệm
        function showGalleryScreen() {
            document.getElementById("selectionScreen").style.display = "none";
            document.getElementById("galleryScreen").style.display = "block";
        }

        // Quay lại màn hình chọn lựa
        function goBackToSelection() {
            document.getElementById("mainContent").style.display = "none";
            document.getElementById("videoScreen").style.display = "none";
            document.getElementById("galleryScreen").style.display = "none";
            document.getElementById("selectionScreen").style.display = "flex";
            
            // Xóa lớp active khỏi các mục
            document.querySelectorAll('.selection-item').forEach(item => {
                item.classList.remove('active');
            });
            
            // Dừng hiệu ứng di chuyển ảnh khi rời khỏi gallery
            stopImageMovement();
            
            // Dừng hiệu ứng bóng bay khi rời khỏi trang thiệp
            stopBalloonEffect();
        }

        // Bắt đầu hiệu ứng kim tuyến
        function startEffects() {
            effectsActive = true;
            
            // Tạo kim tuyến 
            glitterInterval = setInterval(() => {
                if (!effectsActive) return;
                
                const glitter = document.createElement('div');
                glitter.className = 'glitter';
                
                glitter.style.left = Math.random() * 100 + 'vw';
                glitter.style.top = '-10px';
                
                const size = Math.random() * 8 + 3;
                glitter.style.width = size + 'px';
                glitter.style.height = size + 'px';
                
                const colors = ['gold', 'silver', '#ff4081', '#4ecdc4', '#ff6b6b'];
                glitter.style.backgroundColor = colors[Math.floor(Math.random() * colors.length)];
                
                document.body.appendChild(glitter);
                
                const duration = Math.random() * 3 + 2;
                glitter.animate([
                    { transform: 'translateY(0) rotate(0deg)', opacity: 1 },
                    { transform: `translateY(100vh) rotate(${Math.random() * 360}deg)`, opacity: 0 }
                ], {
                    duration: duration * 1000,
                    easing: 'cubic-bezier(0.215, 0.61, 0.355, 1)'
                });
                
                setTimeout(() => {
                    if (glitter.parentNode) {
                        glitter.parentNode.removeChild(glitter);
                    }
                }, duration * 1000);
            }, 100);
        }
        
        // Dừng hiệu ứng kim tuyến
        function stopEffects() {
            effectsActive = false;
            clearInterval(glitterInterval);
            
            const glitters = document.querySelectorAll('.glitter');
            glitters.forEach(glitter => {
                if (glitter.parentNode) {
                    glitter.parentNode.removeChild(glitter);
                }
            });
        }

        // Bắt đầu hiệu ứng bóng bay
        function startBalloonEffect() {
            balloonInterval = setInterval(() => {
                createBalloon();
            }, 100); // thời gian 
        }

        // Dừng hiệu ứng bóng bay
        function stopBalloonEffect() {
            clearInterval(balloonInterval);
            
            // Xóa tất cả bóng bay còn lại
            const balloons = document.querySelectorAll('.balloon');
            balloons.forEach(balloon => {
                if (balloon.parentNode) {
                    balloon.parentNode.removeChild(balloon);
                }
            });
        }

        // Tạo bóng bay
        function createBalloon() {
            const balloon = document.createElement('div');
            balloon.className = 'balloon';
            
            // Màu sắc ngẫu nhiên
            const colors = [
                '#ff4081', '#4ecdc4', '#ff6b6b', '#ffd166', '#06d6a0', 
                '#118ab2', '#ef476f', '#ff9e00', '#7209b7', '#3a86ff'
            ];
            const color = colors[Math.floor(Math.random() * colors.length)];
            balloon.style.backgroundColor = color;
            
            // Vị trí ngẫu nhiên
            const left = Math.random() * 100;
            balloon.style.left = left + '%';
            
            // Kích thước ngẫu nhiên
            const size = Math.random() * 20 + 30;
            balloon.style.width = size + 'px';
            balloon.style.height = size * 1.25 + 'px';
            
            // Thêm bóng bay vào trang thiệp
            const mainContent = document.getElementById('mainContent');
            if (mainContent) {
                mainContent.appendChild(balloon);
            }
            
            // Tự động xóa bóng bay sau khi hiệu ứng kết thúc
            setTimeout(() => {
                if (balloon.parentNode) {
                    balloon.parentNode.removeChild(balloon);
                }
            }, 8000);
        }
        
        // Mở thiệp
        function openBook(bookNumber) {
            const book = document.getElementById(`book${bookNumber}`);
            
            if (!book.classList.contains('opened')) {
                book.classList.add('opened');
                openedBooks++;
                
                // Hiệu ứng âm thanh
                playSoundEffect();
                
                // Hiệu ứng kim tuyến
                createConfetti(10);
                
                // Thông báo mở thiệp 
                let openMessage = "";
                switch(bookNumber) {
                    case 1:
                        openMessage = OPEN_MESSAGE_CONFIG.book1;
                        break;
                    case 2:
                        openMessage = OPEN_MESSAGE_CONFIG.book2;
                        break;
                    case 3:
                        openMessage = OPEN_MESSAGE_CONFIG.book3;
                        break;
                    case 4:
                        openMessage = OPEN_MESSAGE_CONFIG.book4;
                        break;
                    default:
                        openMessage = `Đã mở thiệp ${bookNumber} 🎉`;
                }
                showNotification(openMessage);
                
                // Dừng hiệu ứng bóng bay khi mở thiệp
                stopBalloonEffect();
                
                // Hiệu ứng gõ chữ
                setTimeout(() => {
                    typeMessage(bookMessages[bookNumber-1], bookNumber);
                }, 1000);
                
                // Thông báo khi mở hết thiệp
                if (openedBooks === 4) {
                    showNotification(OPEN_MESSAGE_CONFIG.allOpened);
                }
            }
        }

        // Hiệu ứng gõ chữ với xuống dòng tự động
        function typeMessage(text, bookNumber) {
            const messageEl = document.getElementById(`messageContent${bookNumber}`);
            const pen = document.getElementById(`pen${bookNumber}`);
            const page2 = document.getElementById(`page2-book${bookNumber}`);
            
            messageEl.innerHTML = '';
            pen.style.display = "block";
            
            const canvas = document.createElement('canvas');
            const ctx = canvas.getContext('2d');
            ctx.font = '1rem "Courier New", monospace';
            
            const pageWidth = page2.offsetWidth - 60;
            
            let lines = [];
            let currentLine = '';
            const words = text.split(' ');
            
            for (let i = 0; i < words.length; i++) {
                const word = words[i];
                const testText = currentLine ? currentLine + ' ' + word : word;
                const textWidth = ctx.measureText(testText).width;
                
                if (textWidth > pageWidth && currentLine !== '') {
                    lines.push(currentLine);
                    currentLine = word;
                } else {
                    currentLine = testText;
                }
                
                if (i === words.length - 1) {
                    lines.push(currentLine);
                }
            }
            
            let currentLineIndex = 0;
            let currentCharIndex = 0;
            
            function typeNextChar() {
                if (currentLineIndex >= lines.length) {
                    pen.style.display = "none";
                    createConfetti(10);
                    return;
                }
                
                const currentLineText = lines[currentLineIndex];
                
                if (currentCharIndex < currentLineText.length) {
                    messageEl.innerHTML = '';
                    
                    for (let i = 0; i < currentLineIndex; i++) {
                        const completedLine = document.createElement('div');
                        completedLine.className = 'line';
                        completedLine.textContent = lines[i];
                        messageEl.appendChild(completedLine);
                    }
                    
                    const typingLine = document.createElement('div');
                    typingLine.className = 'line';
                    typingLine.textContent = currentLineText.substring(0, currentCharIndex + 1);
                    messageEl.appendChild(typingLine);
                    
                    updatePenPosition(typingLine, currentCharIndex, bookNumber);
                    
                    currentCharIndex++;
                    setTimeout(typeNextChar, 70);
                } else {
                    currentLineIndex++;
                    currentCharIndex = 0;
                    
                    messageEl.innerHTML = '';
                    for (let i = 0; i < currentLineIndex; i++) {
                        const lineEl = document.createElement('div');
                        lineEl.className = 'line';
                        lineEl.textContent = lines[i];
                        messageEl.appendChild(lineEl);
                    }
                    
                    setTimeout(typeNextChar, 150);
                }
            }
            
            typeNextChar();
        }

        // Cập nhật vị trí bút
        function updatePenPosition(lineEl, charIndex, bookNumber) {
            const pen = document.getElementById(`pen${bookNumber}`);
            const page2 = document.getElementById(`page2-book${bookNumber}`);
            
            const tempSpan = document.createElement('span');
            tempSpan.textContent = lineEl.textContent.substring(0, charIndex + 1);
            tempSpan.style.visibility = 'hidden';
            tempSpan.style.position = 'absolute';
            tempSpan.style.whiteSpace = 'pre';
            tempSpan.style.font = window.getComputedStyle(lineEl).font;
            tempSpan.style.lineHeight = window.getComputedStyle(lineEl).lineHeight;
            
            document.body.appendChild(tempSpan);
            
            const textWidth = tempSpan.offsetWidth;
            
            const lineRect = lineEl.getBoundingClientRect();
            const pageRect = page2.getBoundingClientRect();
            
            const penLeft = lineRect.left - pageRect.left + textWidth + 5;
            const penTop = lineRect.top - pageRect.top - 5;
            
            pen.style.left = penLeft + "px";
            pen.style.top = penTop + "px";
            
            document.body.removeChild(tempSpan);
        }

        // Hiển thị thông báo hoàn thành
        function showCompletionMessage() {
            createConfetti(100);
            showNotification("Chúc mừng sinh nhật! 🎂🎉");
        }

        // Tạo hiệu ứng kim tuyến
        function createConfetti(count) {
            const colors = ['#ff4081', '#4ecdc4', '#ff6b6b', '#ffd166', '#06d6a0'];
            
            for (let i = 0; i < count; i++) {
                const confetti = document.createElement('div');
                confetti.className = 'confetti';
                confetti.style.left = Math.random() * 100 + 'vw';
                confetti.style.backgroundColor = colors[Math.floor(Math.random() * colors.length)];
                confetti.style.width = Math.random() * 10 + 5 + 'px';
                confetti.style.height = Math.random() * 10 + 5 + 'px';
                confetti.style.borderRadius = Math.random() > 0.5 ? '50%' : '0';
                
                document.body.appendChild(confetti);
                
                confetti.animate([
                    { transform: 'translateY(-100vh) rotate(0deg)', opacity: 1 },
                    { transform: `translateY(100vh) rotate(${Math.random() * 360}deg)`, opacity: 0 }
                ], {
                    duration: Math.random() * 3000 + 2000,
                    easing: 'cubic-bezier(0.215, 0.61, 0.355, 1)'
                });
                
                setTimeout(() => {
                    confetti.remove();
                }, 5000);
            }
        }
        
        function playSoundEffect() {
            console.log("🎵 Phát âm thanh hiệu ứng");
        }

        // Điều chỉnh âm lượng bên ngoài
        function setVolume(volume) {
            if (volume >= 0 && volume <= 1) {
                birthdayAudio.volume = volume;
                console.log(`Âm lượng đã được đặt thành: ${volume * 100}%`);
            }
        }

        // Tắt/bật nhạc bên ngoài
        function toggleMusic() {
            if (isPlaying) {
                birthdayAudio.pause();
                isPlaying = false;
                console.log("Nhạc đã tắt");
            } else {
                birthdayAudio.play();
                isPlaying = true;
                console.log("Nhạc đã bật");
            }
        }
    </script>
</body>
</html>
