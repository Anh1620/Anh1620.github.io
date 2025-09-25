<html lang="vi">
<head>
    <meta charset="UTF-8">
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

        .main-content {
            display: none;
            padding: 30px;
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

        .btn:hover {
            transform: translateY(-3px);
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.2);
        }

        .gallery {
            margin-top: 30px;
            text-align: center;
            display: none;
        }

        .gallery h2 {
            color: #ff4081;
            margin-bottom: 20px;
        }

        .gallery-container {
            display: flex;
            flex-wrap: wrap;
            gap: 15px;
            justify-content: center;
            max-height: 300px;
            overflow-y: auto;
            padding: 15px;
            background: rgba(255, 255, 255, 0.7);
            border-radius: 10px;
            margin-bottom: 20px;
        }

        .gallery-image {
            width: 100px;
            height: 100px;
            object-fit: cover;
            border-radius: 8px;
            cursor: pointer;
            transition: transform 0.3s;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
        }

        .gallery-image:hover {
            transform: scale(1.1);
        }

        .slideshow {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0, 0, 0, 0.9);
            z-index: 1000;
            overflow: hidden;
        }

        .slideshow-content {
            position: relative;
            width: 100%;
            height: 100%;
        }

        .close-slideshow {
            position: absolute;
            top: 20px;
            right: 20px;
            background: rgba(255, 255, 255, 0.2);
            border: none;
            color: white;
            font-size: 2rem;
            width: 50px;
            height: 50px;
            border-radius: 50%;
            cursor: pointer;
            z-index: 1001;
            display: flex;
            align-items: center;
            justify-content: center;
        }

        .close-slideshow:hover {
            background: rgba(255, 255, 255, 0.3);
        }

        .slideshow img {
            position: absolute;
            height: 180px;
            border-radius: 12px;
            box-shadow: 0 4px 12px rgba(0, 0, 0, 0.4);
            object-fit: cover;
            width: auto;
            aspect-ratio: 1/1;
        }

        @keyframes flyLeft {
            0% {
                left: 100%;
                opacity: 1;
                transform: rotate(10deg) scale(0.8);
            }
            100% {
                left: -250px;
                opacity: 1;
                transform: rotate(-10deg) scale(0.8);
            }
        }

        @keyframes flyLeft2 {
            0% {
                left: 100%;
                opacity: 1;
                transform: rotate(5deg) scale(0.9);
            }
            100% {
                left: -250px;
                opacity: 1;
                transform: rotate(-5deg) scale(0.9);
            }
        }

        @keyframes flyLeft3 {
            0% {
                left: 100%;
                opacity: 1;
                transform: rotate(0deg) scale(0.85);
            }
            100% {
                left: -250px;
                opacity: 1;
                transform: rotate(0deg) scale(0.85);
            }
        }

        @keyframes flyLeft4 {
            0% {
                left: 100%;
                opacity: 1;
                transform: rotate(15deg) scale(0.75);
            }
            100% {
                left: -250px;
                opacity: 1;
                transform: rotate(-15deg) scale(0.75);
            }
        }

        @keyframes flyLeft5 {
            0% {
                left: 100%;
                opacity: 1;
                transform: rotate(-5deg) scale(0.95);
            }
            100% {
                left: -250px;
                opacity: 1;
                transform: rotate(5deg) scale(0.95);
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

        /* Hiệu ứng kim tuyến */
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

        .balloon::before {
            content: '';
            position: absolute;
            bottom: -15px;
            left: 50%;
            transform: translateX(-50%);
            width: 2px;
            height: 15px;
            background: linear-gradient(to bottom, #ff4081, #ff6b6b);
        }

        @keyframes fall {
            0% {
                transform: translateY(-100px) rotate(0deg);
                opacity: 0;
            }
            10% {
                opacity: 1;
            }
            90% {
                opacity: 1;
            }
            100% {
                transform: translateY(100vh) rotate(360deg);
                opacity: 0;
            }
        }

        @keyframes rise {
            0% {
                transform: translateY(100vh) rotate(0deg);
                opacity: 0;
            }
            10% {
                opacity: 1;
            }
            90% {
                opacity: 1;
            }
            100% {
                transform: translateY(-100px) rotate(360deg);
                opacity: 0;
            }
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
            
            .gallery-image {
                width: 80px;
                height: 80px;
            }
            
            .slideshow img {
                height: 150px;
            }
            
            .books-container {
                gap: 15px;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="password-screen" id="passwordScreen">
            <h1>🎂 HAPPY BIRTHDAY 🎉</h1>
            <p>Nhập mật khẩu để mở</p>
            <input type="password" class="password-input" id="passwordInput" placeholder="Nhập mật khẩu">
            <button class="submit-btn" onclick="checkPassword()">Xác Nhận</button>
            <p class="error-msg" id="errorMsg">Mật khẩu không đúng. Vui lòng thử lại!</p>
        </div>

        <div class="main-content" id="mainContent">
            <div class="header">
                <h1>HAPPY BIRTHDAY 🎂</h1>
                <p>Nhấn vào từng cái để mở thiệp</p> 
            </div>

            <!-- thiệp -->
            <!-- gán tên trên thiệp -->
            <div class="books-container">
                <div class="book-container">
                    <div class="book-title"></div>  <!-- gán tên trên thiệp -->
                    <div class="book" id="book1" onclick="openBook(1)">
                        <div class="page page1">
                            <div>HAPPY BIRTHDAY</div>    <!-- nd hiện trên thiệp -->
                            <div style="font-size: 3rem; margin-top: 20px;">🎁</div>
                        </div>
                        <div class="page page2" id="page2-book1">
                            <div id="messageContent1"></div>
                            <span class="pen" id="pen1">✏️</span>
                        </div>
                    </div>
                </div>

                <!-- thiệp 2 -->
                <div class="book-container">
                    <div class="book-title"></div>   <!-- gán tên trên thiệp -->
                    <div class="book" id="book2" onclick="openBook(2)">
                        <div class="page page1">
                            <div>HAPPY BIRTHDAY</div>    <!-- nd hiện trên thiệp -->
                            <div style="font-size: 3rem; margin-top: 20px;">💌</div>
                        </div>
                        <div class="page page2" id="page2-book2">
                            <div id="messageContent2"></div>
                            <span class="pen" id="pen2">✏️</span>
                        </div>
                    </div>
                </div>

                <!-- thiệp 3 -->
                <div class="book-container">
                    <div class="book-title"></div>  <!-- gán tên trên thiệp -->
                    <div class="book" id="book3" onclick="openBook(3)">
                        <div class="page page1">
                            <div>HAPPY BIRTHDAY</div>   <!-- nd hiện trên thiệp -->
                            <div style="font-size: 3rem; margin-top: 20px;">🎂</div>
                        </div>
                        <div class="page page2" id="page2-book3">
                            <div id="messageContent3"></div>
                            <span class="pen" id="pen3">✏️</span>
                        </div>
                    </div>
                </div>
                
                <!-- thiệp 4 -->
                <div class="book-container">
                    <div class="book-title"></div>    <!-- gán tên trên thiệp -->
                    <div class="book" id="book4" onclick="openBook(4)">  <!-- tên thiệp -->
                        <div class="page page1">
                            <div>HAPPY BIRTHDAY</div>     <!-- nd hiện trên thiệp -->
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
                <button class="btn next-btn" id="nextButton" onclick="showSlideshow()">Tiếp theo ➡️</button>
            </div>

            <div class="gallery" id="imageGallery">
                    <!-- Ảnh sẽ được thêm tự động -->
                </div>
            </div>
        </div>
    

    <div class="slideshow" id="slideshow">
        <div class="slideshow-content">
            <button class="close-slideshow" onclick="closeSlideshow()">×</button>
        </div>
    </div>

    <div class="notification" id="notification"></div>

    <div class="audio-player" id="audioPlayer"></div>

    <script>

        
        // PASS
        const PASSWORD = "a";
        
        //  thông báo khi mở từng thiệp 
        const OPEN_MESSAGE_CONFIG = {
            book1: "ANH",
            book2: "DOAN", 
            book3: "QUANG",
            book4: "ANH1628",
            allOpened: "Đã mở tất cả thiệp📸"
        };
        
        //  lời chúc trong từng thiệp 
        const bookMessages = [
            "lời chúc 1",
            
            "lời chúc 2",
            
            "lời chúc 3",
            
            "lời chúc 4"
        ];

        //Tên hiển thị cho từng thiệp
        const bookTitles = [
            
        ];

        // tên file ảnh
        const localImages = [
            "1.jpg", "2.jpg", "3.jpg", '4.jpg', '5.jpg', '6.jpg', '7.jpg', "8.jpg", "9.jpg", "10.jpg",'41.jpg', '42.jpg',"23.jpg", "24.jpg",
            '11.jpg', '12.jpg', '13.jpg', '14.jpg', "15.jpg", "16.jpg", "17.jpg", '18.jpg', '19.jpg', '20.jpg',"43.jpg",'32.jpg', '33.jpg', '34.jpg',
            '21.jpg', "22.jpg", "23.jpg", "24.jpg", '25.jpg', '26.jpg', '27.jpg', '28.jpg', "29.jpg", "30.jpg","3.jpg", '4.jpg', '5.jpg',
            "31.jpg", '32.jpg', '33.jpg', '34.jpg', '35.jpg', "36.jpg", "37.jpg", "38.jpg", '39.jpg', '40.jpg', "43.jpg", "44.jpg",'27.jpg', '28.jpg', "29.jpg"
        ];

        // file nhạc
        const MUSIC_FILE = "sn.mp3"; 
        
        // Biến toàn cục
        let slideshowInterval;
        let activeImages = 0;
        let uploadedImages = [];
        let glitterInterval;
        let balloonInterval;
        let effectsActive = false;
        let lastImagePosition = 0;
        let openedBooks = 0;

        let birthdayAudio = new Audio();
        let isPlaying = false;
        const DEFAULT_VOLUME = 0.7;

        // cập nhật tên thiệp khi trang load
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

        // Chuyển đổi tên file thành đường dẫn ảnh
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

        // chạy tất cả ảnh
        uploadedImages = [...processLocalImages()];

        window.onload = function() {
            document.getElementById("passwordInput").addEventListener("keypress", function(event) {
                if (event.key === "Enter") {
                    checkPassword();
                }
            });
            
            updateImageGallery();
            updateBookTitles(); // cập nhật tên thiệp
            
            if (localImages.length > 0) {
                console.log(`Đã tải ${localImages.length} ảnh từ thư mục`);
            }

            // audio với file nhạc đã chỉ định
            setupAudio();
        };

        // Chạy audio
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

        // Gallery ảnh
        function updateImageGallery() {
            const galleryContainer = document.getElementById('galleryContainer');
            if (!galleryContainer) return;
            
            galleryContainer.innerHTML = '';
            
            if (uploadedImages.length > 0) {
                document.getElementById('imageGallery').style.display = 'block';
                
                uploadedImages.forEach((image, index) => {
                    const imgElement = document.createElement('img');
                    imgElement.src = image.src;
                    imgElement.alt = image.name;
                    imgElement.className = 'gallery-image';
                    imgElement.title = image.name;
                    imgElement.onclick = () => viewImageInSlideshow(index);
                    
                    imgElement.onerror = function() {
                        console.error(`Không thể tải ảnh: ${image.src}`);
                        this.style.display = 'none';
                    };
                    
                    galleryContainer.appendChild(imgElement);
                });
            } else {
                document.getElementById('imageGallery').style.display = 'none';
            }
        }

        // xem ảnh lớn trong slideshow
        function viewImageInSlideshow(index) {
            showSlideshow();
            
            setTimeout(() => {
                const slideshow = document.getElementById("slideshow");
                slideshow.innerHTML = '<button class="close-slideshow" onclick="closeSlideshow()">×</button>';
                
                const img = document.createElement("img");
                img.src = uploadedImages[index].src;
                img.alt = uploadedImages[index].name;
                img.style.top = "50%";
                img.style.left = "50%";
                img.style.transform = "translate(-50%, -50%)";
                img.style.height = "70vh";
                img.style.width = "auto";
                img.style.maxWidth = "90vw";
                img.style.animation = "none";
                img.style.borderRadius = "15px";
                img.style.boxShadow = "0 10px 30px rgba(0,0,0,0.5)";
                
                img.onerror = function() {
                    console.error(`Không thể tải ảnh: ${uploadedImages[index].src}`);
                    showNotification("Không thể tải ảnh. Vui lòng kiểm tra đường dẫn!");
                    closeSlideshow();
                };
                
                slideshow.appendChild(img);
            }, 100);
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

        // check pass
        function checkPassword() {
            const input = document.getElementById("passwordInput").value.trim().toLowerCase();
            const errorMsg = document.getElementById("errorMsg");
            
            if (input === PASSWORD) {
                document.getElementById("passwordScreen").style.display = "none";
                document.getElementById("mainContent").style.display = "block";
                createConfetti(50);
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

        // bắt đầu hiệu ứng kim tuyến
        function startEffects() {
            effectsActive = true;
            
            // tạo kim tuyến 
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
        
        // dừng hiệu ứng kim tuyến
        function stopEffects() {
            effectsActive = false;
            clearInterval(glitterInterval);
            clearInterval(balloonInterval);
            
            const glitters = document.querySelectorAll('.glitter');
            glitters.forEach(glitter => {
                if (glitter.parentNode) {
                    glitter.parentNode.removeChild(glitter);
                }
            });
            
            const balloons = document.querySelectorAll('.balloon');
            balloons.forEach(balloon => {
                if (balloon.parentNode) {
                    balloon.parentNode.removeChild(balloon);
                }
            });
        }

        // mở thiệp
        function openBook(bookNumber) {
            const book = document.getElementById(`book${bookNumber}`);
            
            
            if (!book.classList.contains('opened')) {
                book.classList.add('opened');
                openedBooks++;
                
                // tiệu ứng âm thanh
                playSoundEffect();
                
                // tiệu ứng kim tuyến
                createConfetti(10);
                
                // thông báo mở thiệp 
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
                
                // hiệu ứng gõ chữ
                setTimeout(() => {
                    typeMessage(bookMessages[bookNumber-1], bookNumber);
                }, 1000);
                
                // thông báo khi mở hết thiệp
                if (openedBooks === 4) {
                    document.getElementById('imageGallery').style.display = 'block';
                    showNotification(OPEN_MESSAGE_CONFIG.allOpened);
                }
            }
        }

 // hiệu ứng gõ chữ với xuống dòng tự động
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

        // cập nhật vị trí bút
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

        // hiển thị slideshow ảnh bay 
        function showSlideshow() {
            document.querySelector(".books-container").style.display = "none";
            document.getElementById("nextButton").style.display = "none";
            document.getElementById("imageGallery").style.display = "none";

            stopEffects();

            const slideshow = document.getElementById("slideshow");
            slideshow.style.display = "block";
            slideshow.innerHTML = '<button class="close-slideshow" onclick="closeSlideshow()">×</button>';

            // reset vị trí ảnh cuối cùng
            lastImagePosition = 0;

            // tạo ảnh bay liên tục
            createContinuousFlyingImages();
            
            playSlideshowSound();
        }
        
        // tạo ảnh bay liên tục nối tiếp nhau
        function createContinuousFlyingImages() {
            const slideshow = document.getElementById("slideshow");
            const windowHeight = window.innerHeight;
            
            // xóa interval cũ nếu có
            if (slideshowInterval) {
                clearInterval(slideshowInterval);
            }
            
            // khoảng cách đều đặn
            slideshowInterval = setInterval(() => {
                if (activeImages < 25) { // số ảnh trên màn
                    createImageSequence(3); // số ảnh mỗi lầ tạo
                }
            }, 600); // tg tạo ảnh
        }
        
        // tạo chuỗi ảnh nối tiếp nhau
        function createImageSequence(count) {
            const slideshow = document.getElementById("slideshow");
            const windowHeight = window.innerHeight;
            
            for (let i = 0; i < count; i++) {
                const img = document.createElement("img");
                
                if (uploadedImages.length > 0) {
                    const randomIndex = Math.floor(Math.random() * uploadedImages.length);
                    img.src = uploadedImages[randomIndex].src;
                    img.alt = uploadedImages[randomIndex].name;
                } else {
                    const randomId = Math.floor(Math.random() * 1000);
                    img.src = `https://picsum.photos/200/180?random=${randomId}`;
                    img.alt = `Ảnh kỷ niệm ${randomId}`;
                }

                // tính toán vị trí ảnh 
                let topPosition;
                if (lastImagePosition === 0) {
                    topPosition = Math.random() * (windowHeight - 200);
                } else {
                    const minGap = 50; // khoảng cách tối thiểu giữa các ảnh
                    const maxGap = 150; // khoảng cách tối đa giữa các ảnh
                    const gap = minGap + Math.random() * (maxGap - minGap);
                    
                    // căn chỉnh ảnh trong khung hình
                    topPosition = lastImagePosition + gap;
                    if (topPosition > windowHeight - 200) {
                        topPosition = Math.random() * (windowHeight - 200); 
                    }
                }
                
                lastImagePosition = topPosition;
                img.style.top = Math.max(0, Math.min(windowHeight - 200, topPosition)) + "px";

                // sử dụng animation ngẫu nhiên
                const animations = ['flyLeft', 'flyLeft2', 'flyLeft3', 'flyLeft4', 'flyLeft5'];
                const randomAnim = animations[Math.floor(Math.random() * animations.length)];
                const duration = 6 + Math.random() * 4; // thời gian di chuyển
                
                img.style.animation = `${randomAnim} ${duration}s linear forwards`;
                
                slideshow.appendChild(img);
                activeImages++;
                
                // xóa ảnh sau khi hoàn thành animation
                setTimeout(() => {
                    if (img.parentNode) {
                        img.parentNode.removeChild(img);
                        activeImages--;
                    }
                }, duration * 1000);
                
                // xử lý lỗi tải ảnh
                img.onerror = function() {
                    console.error("Không thể tải ảnh:", this.src);
                    if (this.parentNode) {
                        this.parentNode.removeChild(this);
                        activeImages--;
                    }
                };
            }
        }
        
        // đóng xem ảnh
        function closeSlideshow() {
            clearInterval(slideshowInterval);
            
            const slideshow = document.getElementById("slideshow");
            slideshow.innerHTML = '<button class="close-slideshow" onclick="closeSlideshow()">×</button>';
            slideshow.style.display = "none";
            
            activeImages = 0;
            lastImagePosition = 0;
            
            document.querySelector(".books-container").style.display = "flex";
            document.getElementById("nextButton").style.display = "inline-block";
            if (uploadedImages.length > 0) {
                document.getElementById('imageGallery').style.display = 'block';
            }
            
            startEffects();
        }
        
        // tạo hiệu ứng kim tuyến
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
        
        function playSlideshowSound() {
            console.log("🎵 Phát nhạc slideshow");
        }

        // điều chỉnh âm lượng bên ngoài
        function setVolume(volume) {
            if (volume >= 0 && volume <= 1) {
                birthdayAudio.volume = volume;
                console.log(`Âm lượng đã được đặt thành: ${volume * 100}%`);
            }
        }

        // tắt/bật nhạc bên ngoài
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
