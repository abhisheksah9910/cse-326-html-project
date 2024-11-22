# cse-326-html-project
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Instagram</title>
    <style>
        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
        }

        body {
            font-family: Arial, sans-serif;
            background-color: #fafafa;
            color: #333;

        }

        header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 10px 20px;
            background-color: #fff;
            box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
        }

        .logo {
            font-weight: bold;
            font-size: 24px;
        }

        nav a {
            margin: 0 15px;
            text-decoration: none;
            color: #0073e6;
            transition: color 0.3s;
        }

        nav a:hover {
            color: #005bb5;
        }

        main {
            padding: 20px;
        }

        .smalldp {
            height: 30px;
            width: 30px;
            border-radius: 50px;
        }

        .post {
            background-color: #fff;
            border: 1px solid #eaeaea;
            border-radius: 5px;
            padding: 15px;
            margin-bottom: 20px;
            height: auto;
            width: 500px;
            box-shadow: 0px 4px 8px rgba(0, 0, 0, 0.1);
        }

        .post-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            cursor: pointer;
        }

        .post-image {
            width: 100%;
            border-radius: 5px;
            margin: 10px 0;
        }

        .heart {
            width: 30px;
            height: 30px;
            fill: #aaa;
            transition: transform 0.3s ease;
        }

        #heart-button {
            margin-left: 0px;
            float: left;
        }

        button.liked .heart {
            fill: #e0245e;
            animation: pop 0.3s forwards;

        }

        @keyframes pop {
            0% {
                transform: scale(1);
            }

            50% {
                transform: scale(1.2);
            }

            100% {
                transform: scale(1);
            }
        }

        .btn:hover {
            opacity: 0.9;
        }

        #comment-button {
            margin-left: 10px;
            float: left;
        }

        .comment-icon {
            width: 30px;
            height: 30px;
            fill: #aaa;
            transition: transform 0.3s ease, fill 0.3s ease;
        }

        button.commented .comment-icon {
            fill: #1e90ff;
            animation: bounce 0.3s forwards;
        }

        @keyframes bounce {
            0% {
                transform: scale(1);
            }

            50% {
                transform: scale(1.2);
            }

            100% {
                transform: scale(1);
            }
        }

        .plane-icon {
            width: 30px;
            height: 30px;
            fill: #aaa;
            transition: transform 0.3s ease, fill 0.3s ease;
        }

        #share-button {
            margin-left: 10px;
            float: left;

        }

        button.shared .plane-icon {
            fill: #1e90ff;
            animation: fly 0.5s forwards;
        }

        @keyframes fly {
            0% {
                transform: translateX(0) rotate(0deg);
            }

            50% {
                transform: translateX(-10px) rotate(10deg);
            }

            100% {
                transform: translateX(100px) rotate(-45deg);
                opacity: 0;
            }
        }

        .sidebar {
            width: 250px;
            background-color: #fff;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
            display: flex;
            flex-direction: column;
            align-items: center;
            padding-top: 20px;
            position: fixed;
            height: 100vh;
            background: linear-gradient(to bottom, #f45608, #ee2a7b, #515bd4);
        }

        .sidebar-logo {
            font-size: 24px;
            font-weight: bold;
            margin-bottom: 40px;
        }

        .nav-item {
            width: 90%;
            padding: 15px;
            margin: 10px 0;
            text-align: left;
            display: flex;
            align-items: center;
            color: #333;
            font-size: 18px;
            text-decoration: none;
            border-radius: 8px;
            transition: background-color 0.3s, color 0.3s;
        }

        .nav-item:hover {
            background-color: #f0f0f0;
            color: #0095f6;
        }

        .nav-item svg {
            margin-right: 15px;
            width: 24px;
            height: 24px;
            fill: currentColor;
        }

        .nav-item.active {
            background-color: #e0f7fa;
            color: #0095f6;
            font-weight: bold;
        }

        .footer {
            margin-top: auto;
            font-size: 12px;
            color: #999;
            text-align: center;
            padding: 20px;
        }


        
        .story-navigation {
            display: flex;
            margin-right: 350px;
            padding: 10px;
            background-color: #fafafa;
            width: 900px;
        }

        .story {
            flex: 0 0 auto;
            text-align: center;
            margin-right: 10px;
            cursor: pointer;

        }

        .story img {
            width: 80px;
            height: 80px;
            border-radius: 50%;
            border: 3px solid #FF4500;
           
        }

        .story p {
            margin-top: 5px;
            font-size: 12px;
            color: #333;
        }

        

        .story-modal {
            display: none;
           
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0, 0, 0, 0.8);
            justify-content: center;
            align-items: center;
        }

        .story-modal video {
            max-width: 90%;
            max-height: 90%;
            border-radius: 15px;
        }

        .close-btn {
            position: absolute;
            top: 20px;
            right: 20px;
            color: #fff;
            font-size: 24px;
            cursor: pointer;
        }
    </style>
</head>

<body>
    <center>
        <script>
            function toggleLike() {
                const button = document.getElementById('heart-button');
                button.classList.toggle('liked');
            }
            function toggleComment() {
                const button = document.getElementById('comment-button');
                button.classList.toggle('commented');
            }

            function toggleShare() {
                const button = document.getElementById('share-button');
                button.classList.add('shared');

                // Reset animation after it completes
                setTimeout(() => {
                    button.classList.remove('shared');
                }, 500);
            }
            // Function to open the story and play video
            function openStory(videoSrc) {
                const modal = document.getElementById('storyModal');
                const video = document.getElementById('storyVideo');

                video.src = videoSrc; // Set the video source
                video.play(); // Play the video
                modal.style.display = 'flex'; // Show the modal
            }

            // Function to close the story
            function closeStory() {
                const modal = document.getElementById('storyModal');
                const video = document.getElementById('storyVideo');

                video.pause(); // Pause the video
                video.currentTime = 0; // Reset the video time
                modal.style.display = 'none'; // Hide the modal
            }

        </script>
        <div class="sidebar">
            <div class="sidebar-logo">
                <img src="insta.png" alt="Instagram Logo" height="50">
            </div>
            <a href="#aa" class="nav-item active">
                <svg viewBox="0 0 24 24">
                    <path
                        d="M22 11V5c0-1.1-.9-2-2-2h-4V1h-4v2H8V1H4v2H2C.9 3 0 3.9 0 5v6c0 4.2 3.4 7.7 7.8 8V23h8.4v-4.1c4.4-.3 7.8-3.8 7.8-8zM7.8 20v-2.8H6.4c-2.8 0-5.1-2.3-5.1-5.2V7h2v4c0 2.8 2.3 5.1 5.1 5.1h1.4v2.9H7.8zM20 12v-4h-4v4h4zm-4.8 8V17H15v-3.1c0-1.7-1.4-3.1-3.2-3.1H8V12c0-1.7-1.4-3.1-3.2-3.1H3V7h5.1C12.6 7 14.9 9.3 14.9 12v3h4.3V9.5h1.9V20h-4.9z" />
                </svg>
                Home
            </a>

            <a href="explore.html" class="nav-item">
                <svg viewBox="0 0 24 24">
                    <path
                        d="M12 2a9 9 0 00-9 9c0 4.5 4.4 8.6 8.9 13.5.6.7 1.5.7 2.1 0 4.5-4.9 8.9-9 8.9-13.5 0-4.9-4-9-9-9zm0 13c-1.7 0-3-1.3-3-3s1.3-3 3-3 3 1.3 3 3-1.3 3-3 3z" />
                </svg>
                Explore
            </a>

            <a href="https://www.messenger.com/" class="nav-item">
                <svg viewBox="0 0 24 24">
                    <path d="M20 2h-8c-1.1 0-2 .9-2 2v12h8V4h2v16h-2v2h8V4c0-1.1-.9-2-2-2z" />
                </svg>
                Messages
            </a>
            <a href="https://www.instagram.com/its_abhisheek/" class="nav-item">
                <svg viewBox="0 0 24 24">
                    <path
                        d="M12 14.7c-3.7 0-6.7 2.3-6.7 5.2v2.3h13.4v-2.3c0-2.9-3-5.2-6.7-5.2zm0-10.2c2.2 0 4.1 1.8 4.1 4 0 2.3-1.9 4-4.1 4-2.3 0-4.1-1.8-4.1-4 0-2.2 1.8-4 4.1-4z" />
                </svg>
                Profile
            </a>
            <a href="https://www.instagram.com/accounts/edit/" class="nav-item">
                <svg viewBox="0 0 24 24">
                    <path
                        d="M19.1 3H5.2C3.4 3 2 4.4 2 6.2v11.6C2 19.6 3.4 21 5.2 21h13.9c1.8 0 3.2-1.4 3.2-3.2V6.2C22.3 4.4 20.9 3 19.1 3zm0 13.8H5.2c-.4 0-.8-.4-.8-.8V6.2c0-.4.4-.8.8-.8h13.9c.4 0 .8.4.8.8v9.7c.1.4-.3.8-.8.8z" />
                </svg>
                Settings
            </a>
            <a href="signup.html" class="nav-item">
                <svg xmlns="http://www.w3.org/2000/svg"
                    viewBox="0 0 512 512"><!--!Font Awesome Free 6.6.0 by @fontawesome - https://fontawesome.com License - https://fontawesome.com/license/free Copyright 2024 Fonticons, Inc.-->
                    <path
                        d="M377.9 105.9L500.7 228.7c7.2 7.2 11.3 17.1 11.3 27.3s-4.1 20.1-11.3 27.3L377.9 406.1c-6.4 6.4-15 9.9-24 9.9c-18.7 0-33.9-15.2-33.9-33.9l0-62.1-128 0c-17.7 0-32-14.3-32-32l0-64c0-17.7 14.3-32 32-32l128 0 0-62.1c0-18.7 15.2-33.9 33.9-33.9c9 0 17.6 3.6 24 9.9zM160 96L96 96c-17.7 0-32 14.3-32 32l0 256c0 17.7 14.3 32 32 32l64 0c17.7 0 32 14.3 32 32s-14.3 32-32 32l-64 0c-53 0-96-43-96-96L0 128C0 75 43 32 96 32l64 0c17.7 0 32 14.3 32 32s-14.3 32-32 32z" />
                </svg>
                Log Out
            </a>
            <div class="footer">
                © 2024 Instagram by Abhishek
            </div>



        </div>
        <header>
            <div id="aa"></div>
            <div class="story-navigation">
                <div class="story" onclick="openStory('spider2.mp4')">
                    <img src="dp.jpg" alt="User 1">
                    <p>Abhishek</p>
                </div>
                <div class="story" onclick="openStory('marvel.mp4')">
                    <img src="adi2.jpg" alt="User 2">
                    <p>Aditya</p>
                </div>
                <div class="story" onclick="openStory('shangchi.mp4')">
                    <img src="ujjwal1.jpg" alt="User 3">
                    <p>ujjwal</p>
                </div>
                <div class="story" onclick="openStory('dc.mp4')">
                    <img src="sushant1.jpg" alt="User 3">
                    <p>sushant</p>
                </div>
                <div class="story" onclick="openStory('spider.mp4')">
                    <img src="raza.jpg" alt="User 3">
                    <p>Raza</p>
                </div>
                <div class="story" onclick="openStory('avatar.mp4')">
                    <img src="ai1.jpg" alt="User 3">
                    <p>abhi</p>
                </div>
                <div class="story" onclick="openStory('spider3.mp4')">
                    <img src="adi1.jpg" alt="User 3">
                    <p>Adi</p>
                </div>
                <div class="story" onclick="openStory('deadpool.mp4')">
                    <img src="dp2.jpg" alt="User 3">
                    <p>Abhishek</p>
                </div>
                <div class="story" onclick="openStory('marvel.mp4')">
                    <img src="rdj.jpeg" alt="User 3">
                    <p>RDJ</p>
                </div>
                <div class="story" onclick="openStory('dc.mp4')">
                    <img src="marvel.jpg" alt="User 3">
                    <p>Marvel</p>
                </div>
                <div class="story" onclick="openStory('shangchi.mp4')">
                    <img src="deadpool.jpeg" alt="User 3">
                    <p>Deadpool</p>
                </div>
                <div class="story" onclick="openStory('spider.mp4')">
                    <img src="spider.jpg" alt="User 3">
                    <p>Spiderman</p>
                </div>
                <div class="story" onclick="openStory('spider2.mp4')">
                    <img src="group1.jpg" alt="User 3">
                    <p>Rohit</p>
                </div>
                <div class="story" onclick="openStory('shangchi.mp4')">
                    <img src="sony.png" alt="User 3">
                    <p>Sony</p>
                </div>





            </div>

            <!-- Modal for playing stories -->
            <div class="story-modal" id="storyModal">
                <span class="close-btn" onclick="closeStory()">&times;</span>
                <video id="storyVideo" controls></video>
            </div>
        </header>

        <main>

            <div class="post">
                <div class="post-header">
                    <img src="dp.jpg" alt="Post Image" class="smalldp">
                    <h4 style="margin-right:315px;">its_abhisheek</h4>

                </div>
                <img src="friends.jpg" alt="Post Image" class="post-image">
                <!-- <video class="post-image" src="marvel.mp4"  muted loop autoplay > -->

                </video>
                <button id="heart-button" onclick="toggleLike()" style="text-align:left">
                    <svg class="heart" viewBox="0 0 24 24">
                        <path
                            d="M12 21.35l-1.45-1.32C5.4 15.36 2 12.28 2 8.5 2 5.42 4.42 3 7.5 3c1.74 0 3.41.81 4.5 2.09C13.09 3.81 14.76 3 16.5 3 19.58 3 22 5.42 22 8.5c0 3.78-3.4 6.86-8.55 11.54L12 21.35z" />
                    </svg>
                </button>
                <button id="comment-button" onclick="toggleComment()">
                    <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 512 512" class="comment-icon">
                        <path
                            d="M123.6 391.3c12.9-9.4 29.6-11.8 44.6-6.4c26.5 9.6 56.2 15.1 87.8 15.1c124.7 0 208-80.5 208-160s-83.3-160-208-160S48 160.5 48 240c0 32 12.4 62.8 35.7 89.2c8.6 9.7 12.8 22.5 11.8 35.5c-1.4 18.1-5.7 34.7-11.3 49.4c17-7.9 31.1-16.7 39.4-22.7zM21.2 431.9c1.8-2.7 3.5-5.4 5.1-8.1c10-16.6 19.5-38.4 21.4-62.9C17.7 326.8 0 285.1 0 240C0 125.1 114.6 32 256 32s256 93.1 256 208s-114.6 208-256 208c-37.1 0-72.3-6.4-104.1-17.9c-11.9 8.7-31.3 20.6-54.3 30.6c-15.1 6.6-32.3 12.6-50.1 16.1c-.8 .2-1.6 .3-2.4 .5c-4.4 .8-8.7 1.5-13.2 1.9c-.2 0-.5 .1-.7 .1c-5.1 .5-10.2 .8-15.3 .8c-6.5 0-12.3-3.9-14.8-9.9c-2.5-6-1.1-12.8 3.4-17.4c4.1-4.2 7.8-8.7 11.3-13.5c1.7-2.3 3.3-4.6 4.8-6.9l.3-.5z" />
                    </svg>
                </button>
                <button id="share-button" onclick="toggleShare()">
                    <svg class="plane-icon" viewBox="0 0 24 24">
                        <path d="M2 21l21-9-21-9v7l15 2-15 2z" />
                    </svg>
                </button>
                <br><br><br><br>
                <p class="post-caption" style="text-align: left; ">Capturing the essence of friendship &#128512</p>
            </div>


            <div class="post">
                <div class="post-header">
                    <img src="adi2.jpg" alt="Post Image" class="smalldp">
                    <h4 style="margin-right:325px;">aditya_gupta</h4>

                </div>
                <img src="friends2.jpg" alt="Post Image" class="post-image">
                <!-- <video class="post-image" src="marvel.mp4"  muted loop autoplay > -->

                </video>
                <button id="heart-button" onclick="toggleLike()" style="text-align:left">
                    <svg class="heart" viewBox="0 0 24 24">
                        <path
                            d="M12 21.35l-1.45-1.32C5.4 15.36 2 12.28 2 8.5 2 5.42 4.42 3 7.5 3c1.74 0 3.41.81 4.5 2.09C13.09 3.81 14.76 3 16.5 3 19.58 3 22 5.42 22 8.5c0 3.78-3.4 6.86-8.55 11.54L12 21.35z" />
                    </svg>
                </button>
                <button id="comment-button" onclick="toggleComment()">
                    <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 512 512" class="comment-icon">
                        <path
                            d="M123.6 391.3c12.9-9.4 29.6-11.8 44.6-6.4c26.5 9.6 56.2 15.1 87.8 15.1c124.7 0 208-80.5 208-160s-83.3-160-208-160S48 160.5 48 240c0 32 12.4 62.8 35.7 89.2c8.6 9.7 12.8 22.5 11.8 35.5c-1.4 18.1-5.7 34.7-11.3 49.4c17-7.9 31.1-16.7 39.4-22.7zM21.2 431.9c1.8-2.7 3.5-5.4 5.1-8.1c10-16.6 19.5-38.4 21.4-62.9C17.7 326.8 0 285.1 0 240C0 125.1 114.6 32 256 32s256 93.1 256 208s-114.6 208-256 208c-37.1 0-72.3-6.4-104.1-17.9c-11.9 8.7-31.3 20.6-54.3 30.6c-15.1 6.6-32.3 12.6-50.1 16.1c-.8 .2-1.6 .3-2.4 .5c-4.4 .8-8.7 1.5-13.2 1.9c-.2 0-.5 .1-.7 .1c-5.1 .5-10.2 .8-15.3 .8c-6.5 0-12.3-3.9-14.8-9.9c-2.5-6-1.1-12.8 3.4-17.4c4.1-4.2 7.8-8.7 11.3-13.5c1.7-2.3 3.3-4.6 4.8-6.9l.3-.5z" />
                    </svg>
                </button>
                <button id="share-button" onclick="toggleShare()">
                    <svg class="plane-icon" viewBox="0 0 24 24">
                        <path d="M2 21l21-9-21-9v7l15 2-15 2z" />
                    </svg>
                </button>
                <br><br><br><br>
                <p class="post-caption" style="text-align: left; ">Birthday celebration with awesome batchmates &#127880
                    &#127881 &#127882</p>
            </div>


            <div class="post">
                <div class="post-header">
                    <img src="group1.jpg" alt="Post Image" class="smalldp">
                    <h4 style="margin-right:330px;">rohit_kumar</h4>

                </div>
                <!-- <img src="dp.jpg" alt="Post Image" class="post-image"> -->
                <video class="post-image" src="avatar.mp4" muted loop autoplay>

                </video>
                <button id="heart-button" onclick="toggleLike()" style="text-align:left">
                    <svg class="heart" viewBox="0 0 24 24">
                        <path
                            d="M12 21.35l-1.45-1.32C5.4 15.36 2 12.28 2 8.5 2 5.42 4.42 3 7.5 3c1.74 0 3.41.81 4.5 2.09C13.09 3.81 14.76 3 16.5 3 19.58 3 22 5.42 22 8.5c0 3.78-3.4 6.86-8.55 11.54L12 21.35z" />
                    </svg>
                </button>
                <button id="comment-button" onclick="toggleComment()">
                    <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 512 512" class="comment-icon">
                        <path
                            d="M123.6 391.3c12.9-9.4 29.6-11.8 44.6-6.4c26.5 9.6 56.2 15.1 87.8 15.1c124.7 0 208-80.5 208-160s-83.3-160-208-160S48 160.5 48 240c0 32 12.4 62.8 35.7 89.2c8.6 9.7 12.8 22.5 11.8 35.5c-1.4 18.1-5.7 34.7-11.3 49.4c17-7.9 31.1-16.7 39.4-22.7zM21.2 431.9c1.8-2.7 3.5-5.4 5.1-8.1c10-16.6 19.5-38.4 21.4-62.9C17.7 326.8 0 285.1 0 240C0 125.1 114.6 32 256 32s256 93.1 256 208s-114.6 208-256 208c-37.1 0-72.3-6.4-104.1-17.9c-11.9 8.7-31.3 20.6-54.3 30.6c-15.1 6.6-32.3 12.6-50.1 16.1c-.8 .2-1.6 .3-2.4 .5c-4.4 .8-8.7 1.5-13.2 1.9c-.2 0-.5 .1-.7 .1c-5.1 .5-10.2 .8-15.3 .8c-6.5 0-12.3-3.9-14.8-9.9c-2.5-6-1.1-12.8 3.4-17.4c4.1-4.2 7.8-8.7 11.3-13.5c1.7-2.3 3.3-4.6 4.8-6.9l.3-.5z" />
                    </svg>
                </button>
                <button id="share-button" onclick="toggleShare()">
                    <svg class="plane-icon" viewBox="0 0 24 24">
                        <path d="M2 21l21-9-21-9v7l15 2-15 2z" />
                    </svg>
                </button>
                <br><br><br><br>
                <p class="post-caption" style="text-align: left; ">Avatar: The way of water</p>
            </div>

            <div class="post">
                <div class="post-header">
                    <img src="marvel.jpg" alt="Post Image" class="smalldp">
                    <h4 style="margin-right:370px;">marvel</h4>

                </div>
                <!-- <img src="dp.jpg" alt="Post Image" class="post-image"> -->
                <video class="post-image" src="shangchi.mp4" muted loop autoplay>

                </video>
                <button id="heart-button" onclick="toggleLike()" style="text-align:left">
                    <svg class="heart" viewBox="0 0 24 24">
                        <path
                            d="M12 21.35l-1.45-1.32C5.4 15.36 2 12.28 2 8.5 2 5.42 4.42 3 7.5 3c1.74 0 3.41.81 4.5 2.09C13.09 3.81 14.76 3 16.5 3 19.58 3 22 5.42 22 8.5c0 3.78-3.4 6.86-8.55 11.54L12 21.35z" />
                    </svg>
                </button>
                <button id="comment-button" onclick="toggleComment()">
                    <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 512 512" class="comment-icon">
                        <path
                            d="M123.6 391.3c12.9-9.4 29.6-11.8 44.6-6.4c26.5 9.6 56.2 15.1 87.8 15.1c124.7 0 208-80.5 208-160s-83.3-160-208-160S48 160.5 48 240c0 32 12.4 62.8 35.7 89.2c8.6 9.7 12.8 22.5 11.8 35.5c-1.4 18.1-5.7 34.7-11.3 49.4c17-7.9 31.1-16.7 39.4-22.7zM21.2 431.9c1.8-2.7 3.5-5.4 5.1-8.1c10-16.6 19.5-38.4 21.4-62.9C17.7 326.8 0 285.1 0 240C0 125.1 114.6 32 256 32s256 93.1 256 208s-114.6 208-256 208c-37.1 0-72.3-6.4-104.1-17.9c-11.9 8.7-31.3 20.6-54.3 30.6c-15.1 6.6-32.3 12.6-50.1 16.1c-.8 .2-1.6 .3-2.4 .5c-4.4 .8-8.7 1.5-13.2 1.9c-.2 0-.5 .1-.7 .1c-5.1 .5-10.2 .8-15.3 .8c-6.5 0-12.3-3.9-14.8-9.9c-2.5-6-1.1-12.8 3.4-17.4c4.1-4.2 7.8-8.7 11.3-13.5c1.7-2.3 3.3-4.6 4.8-6.9l.3-.5z" />
                    </svg>
                </button>
                <button id="share-button" onclick="toggleShare()">
                    <svg class="plane-icon" viewBox="0 0 24 24">
                        <path d="M2 21l21-9-21-9v7l15 2-15 2z" />
                    </svg>
                </button>
                <br><br><br><br>
                <p class="post-caption" style="text-align: left; ">Shangchi</p>
            </div>

            <div class="post">
                <div class="post-header">
                    <img src="deadpool.jpeg" alt="Post Image" class="smalldp">
                    <h4 style="margin-right:350px;">deadpool</h4>

                </div>
                <!-- <img src="dp.jpg" alt="Post Image" class="post-image"> -->
                <video class="post-image" src="deadpool.mp4" muted loop autoplay>

                </video>
                <button id="heart-button" onclick="toggleLike()" style="text-align:left">
                    <svg class="heart" viewBox="0 0 24 24">
                        <path
                            d="M12 21.35l-1.45-1.32C5.4 15.36 2 12.28 2 8.5 2 5.42 4.42 3 7.5 3c1.74 0 3.41.81 4.5 2.09C13.09 3.81 14.76 3 16.5 3 19.58 3 22 5.42 22 8.5c0 3.78-3.4 6.86-8.55 11.54L12 21.35z" />
                    </svg>
                </button>
                <button id="comment-button" onclick="toggleComment()">
                    <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 512 512" class="comment-icon">
                        <path
                            d="M123.6 391.3c12.9-9.4 29.6-11.8 44.6-6.4c26.5 9.6 56.2 15.1 87.8 15.1c124.7 0 208-80.5 208-160s-83.3-160-208-160S48 160.5 48 240c0 32 12.4 62.8 35.7 89.2c8.6 9.7 12.8 22.5 11.8 35.5c-1.4 18.1-5.7 34.7-11.3 49.4c17-7.9 31.1-16.7 39.4-22.7zM21.2 431.9c1.8-2.7 3.5-5.4 5.1-8.1c10-16.6 19.5-38.4 21.4-62.9C17.7 326.8 0 285.1 0 240C0 125.1 114.6 32 256 32s256 93.1 256 208s-114.6 208-256 208c-37.1 0-72.3-6.4-104.1-17.9c-11.9 8.7-31.3 20.6-54.3 30.6c-15.1 6.6-32.3 12.6-50.1 16.1c-.8 .2-1.6 .3-2.4 .5c-4.4 .8-8.7 1.5-13.2 1.9c-.2 0-.5 .1-.7 .1c-5.1 .5-10.2 .8-15.3 .8c-6.5 0-12.3-3.9-14.8-9.9c-2.5-6-1.1-12.8 3.4-17.4c4.1-4.2 7.8-8.7 11.3-13.5c1.7-2.3 3.3-4.6 4.8-6.9l.3-.5z" />
                    </svg>
                </button>
                <button id="share-button" onclick="toggleShare()">
                    <svg class="plane-icon" viewBox="0 0 24 24">
                        <path d="M2 21l21-9-21-9v7l15 2-15 2z" />
                    </svg>
                </button>
                <br><br><br><br>
                <p class="post-caption" style="text-align: left; ">Deadpool & Woolverine</p>
            </div>

            <div class="post">
                <div class="post-header">
                    <img src="marvel.jpg" alt="Post Image" class="smalldp">
                    <h4 style="margin-right:370px;">marvel</h4>

                </div>
                <!-- <img src="dp.jpg" alt="Post Image" class="post-image"> -->
                <video class="post-image" src="marvel.mp4" muted loop autoplay>

                </video>
                <button id="heart-button" onclick="toggleLike()" style="text-align:left">
                    <svg class="heart" viewBox="0 0 24 24">
                        <path
                            d="M12 21.35l-1.45-1.32C5.4 15.36 2 12.28 2 8.5 2 5.42 4.42 3 7.5 3c1.74 0 3.41.81 4.5 2.09C13.09 3.81 14.76 3 16.5 3 19.58 3 22 5.42 22 8.5c0 3.78-3.4 6.86-8.55 11.54L12 21.35z" />
                    </svg>
                </button>
                <button id="comment-button" onclick="toggleComment()">
                    <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 512 512" class="comment-icon">
                        <path
                            d="M123.6 391.3c12.9-9.4 29.6-11.8 44.6-6.4c26.5 9.6 56.2 15.1 87.8 15.1c124.7 0 208-80.5 208-160s-83.3-160-208-160S48 160.5 48 240c0 32 12.4 62.8 35.7 89.2c8.6 9.7 12.8 22.5 11.8 35.5c-1.4 18.1-5.7 34.7-11.3 49.4c17-7.9 31.1-16.7 39.4-22.7zM21.2 431.9c1.8-2.7 3.5-5.4 5.1-8.1c10-16.6 19.5-38.4 21.4-62.9C17.7 326.8 0 285.1 0 240C0 125.1 114.6 32 256 32s256 93.1 256 208s-114.6 208-256 208c-37.1 0-72.3-6.4-104.1-17.9c-11.9 8.7-31.3 20.6-54.3 30.6c-15.1 6.6-32.3 12.6-50.1 16.1c-.8 .2-1.6 .3-2.4 .5c-4.4 .8-8.7 1.5-13.2 1.9c-.2 0-.5 .1-.7 .1c-5.1 .5-10.2 .8-15.3 .8c-6.5 0-12.3-3.9-14.8-9.9c-2.5-6-1.1-12.8 3.4-17.4c4.1-4.2 7.8-8.7 11.3-13.5c1.7-2.3 3.3-4.6 4.8-6.9l.3-.5z" />
                    </svg>
                </button>
                <button id="share-button" onclick="toggleShare()">
                    <svg class="plane-icon" viewBox="0 0 24 24">
                        <path d="M2 21l21-9-21-9v7l15 2-15 2z" />
                    </svg>
                </button>
                <br><br><br><br>
                <p class="post-caption" style="text-align: left; ">RDJ As Dr. Doom</p>
            </div>

            <div class="post">
                <div class="post-header">
                    <img src="marvel.jpg" alt="Post Image" class="smalldp">
                    <h4 style="margin-right:370px;">marvel</h4>

                </div>
                <!-- <img src="dp.jpg" alt="Post Image" class="post-image"> -->
                <video class="post-image" src="spider3.mp4" muted loop autoplay>

                </video>
                <button id="heart-button" onclick="toggleLike()" style="text-align:left">
                    <svg class="heart" viewBox="0 0 24 24">
                        <path
                            d="M12 21.35l-1.45-1.32C5.4 15.36 2 12.28 2 8.5 2 5.42 4.42 3 7.5 3c1.74 0 3.41.81 4.5 2.09C13.09 3.81 14.76 3 16.5 3 19.58 3 22 5.42 22 8.5c0 3.78-3.4 6.86-8.55 11.54L12 21.35z" />
                    </svg>
                </button>
                <button id="comment-button" onclick="toggleComment()">
                    <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 512 512" class="comment-icon">
                        <path
                            d="M123.6 391.3c12.9-9.4 29.6-11.8 44.6-6.4c26.5 9.6 56.2 15.1 87.8 15.1c124.7 0 208-80.5 208-160s-83.3-160-208-160S48 160.5 48 240c0 32 12.4 62.8 35.7 89.2c8.6 9.7 12.8 22.5 11.8 35.5c-1.4 18.1-5.7 34.7-11.3 49.4c17-7.9 31.1-16.7 39.4-22.7zM21.2 431.9c1.8-2.7 3.5-5.4 5.1-8.1c10-16.6 19.5-38.4 21.4-62.9C17.7 326.8 0 285.1 0 240C0 125.1 114.6 32 256 32s256 93.1 256 208s-114.6 208-256 208c-37.1 0-72.3-6.4-104.1-17.9c-11.9 8.7-31.3 20.6-54.3 30.6c-15.1 6.6-32.3 12.6-50.1 16.1c-.8 .2-1.6 .3-2.4 .5c-4.4 .8-8.7 1.5-13.2 1.9c-.2 0-.5 .1-.7 .1c-5.1 .5-10.2 .8-15.3 .8c-6.5 0-12.3-3.9-14.8-9.9c-2.5-6-1.1-12.8 3.4-17.4c4.1-4.2 7.8-8.7 11.3-13.5c1.7-2.3 3.3-4.6 4.8-6.9l.3-.5z" />
                    </svg>
                </button>
                <button id="share-button" onclick="toggleShare()">
                    <svg class="plane-icon" viewBox="0 0 24 24">
                        <path d="M2 21l21-9-21-9v7l15 2-15 2z" />
                    </svg>
                </button>
                <br><br><br><br>
                <p class="post-caption" style="text-align: left; ">spierman</p>
            </div>

            <div class="post">
                <div class="post-header">
                    <img src="marvel.jpg" alt="Post Image" class="smalldp">
                    <h4 style="margin-right:370px;">marvel</h4>

                </div>
                <!-- <img src="dp.jpg" alt="Post Image" class="post-image"> -->
                <video class="post-image" src="dc.mp4" muted loop autoplay>

                </video>
                <button id="heart-button" onclick="toggleLike()" style="text-align:left">
                    <svg class="heart" viewBox="0 0 24 24">
                        <path
                            d="M12 21.35l-1.45-1.32C5.4 15.36 2 12.28 2 8.5 2 5.42 4.42 3 7.5 3c1.74 0 3.41.81 4.5 2.09C13.09 3.81 14.76 3 16.5 3 19.58 3 22 5.42 22 8.5c0 3.78-3.4 6.86-8.55 11.54L12 21.35z" />
                    </svg>
                </button>
                <button id="comment-button" onclick="toggleComment()">
                    <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 512 512" class="comment-icon">
                        <path
                            d="M123.6 391.3c12.9-9.4 29.6-11.8 44.6-6.4c26.5 9.6 56.2 15.1 87.8 15.1c124.7 0 208-80.5 208-160s-83.3-160-208-160S48 160.5 48 240c0 32 12.4 62.8 35.7 89.2c8.6 9.7 12.8 22.5 11.8 35.5c-1.4 18.1-5.7 34.7-11.3 49.4c17-7.9 31.1-16.7 39.4-22.7zM21.2 431.9c1.8-2.7 3.5-5.4 5.1-8.1c10-16.6 19.5-38.4 21.4-62.9C17.7 326.8 0 285.1 0 240C0 125.1 114.6 32 256 32s256 93.1 256 208s-114.6 208-256 208c-37.1 0-72.3-6.4-104.1-17.9c-11.9 8.7-31.3 20.6-54.3 30.6c-15.1 6.6-32.3 12.6-50.1 16.1c-.8 .2-1.6 .3-2.4 .5c-4.4 .8-8.7 1.5-13.2 1.9c-.2 0-.5 .1-.7 .1c-5.1 .5-10.2 .8-15.3 .8c-6.5 0-12.3-3.9-14.8-9.9c-2.5-6-1.1-12.8 3.4-17.4c4.1-4.2 7.8-8.7 11.3-13.5c1.7-2.3 3.3-4.6 4.8-6.9l.3-.5z" />
                    </svg>
                </button>
                <button id="share-button" onclick="toggleShare()">
                    <svg class="plane-icon" viewBox="0 0 24 24">
                        <path d="M2 21l21-9-21-9v7l15 2-15 2z" />
                    </svg>
                </button>
                <br><br><br><br>
                <p class="post-caption" style="text-align: left; ">Superman & Batman</p>
            </div>

            <div class="post">
                <div class="post-header">
                    <img src="marvel.jpg" alt="Post Image" class="smalldp">
                    <h4 style="margin-right:370px;">marvel</h4>

                </div>
                <!-- <img src="dp.jpg" alt="Post Image" class="post-image"> -->
                <video class="post-image" src="spider2.mp4" muted loop autoplay>

                </video>
                <button id="heart-button" onclick="toggleLike()" style="text-align:left">
                    <svg class="heart" viewBox="0 0 24 24">
                        <path
                            d="M12 21.35l-1.45-1.32C5.4 15.36 2 12.28 2 8.5 2 5.42 4.42 3 7.5 3c1.74 0 3.41.81 4.5 2.09C13.09 3.81 14.76 3 16.5 3 19.58 3 22 5.42 22 8.5c0 3.78-3.4 6.86-8.55 11.54L12 21.35z" />
                    </svg>
                </button>
                <button id="comment-button" onclick="toggleComment()">
                    <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 512 512" class="comment-icon">
                        <path
                            d="M123.6 391.3c12.9-9.4 29.6-11.8 44.6-6.4c26.5 9.6 56.2 15.1 87.8 15.1c124.7 0 208-80.5 208-160s-83.3-160-208-160S48 160.5 48 240c0 32 12.4 62.8 35.7 89.2c8.6 9.7 12.8 22.5 11.8 35.5c-1.4 18.1-5.7 34.7-11.3 49.4c17-7.9 31.1-16.7 39.4-22.7zM21.2 431.9c1.8-2.7 3.5-5.4 5.1-8.1c10-16.6 19.5-38.4 21.4-62.9C17.7 326.8 0 285.1 0 240C0 125.1 114.6 32 256 32s256 93.1 256 208s-114.6 208-256 208c-37.1 0-72.3-6.4-104.1-17.9c-11.9 8.7-31.3 20.6-54.3 30.6c-15.1 6.6-32.3 12.6-50.1 16.1c-.8 .2-1.6 .3-2.4 .5c-4.4 .8-8.7 1.5-13.2 1.9c-.2 0-.5 .1-.7 .1c-5.1 .5-10.2 .8-15.3 .8c-6.5 0-12.3-3.9-14.8-9.9c-2.5-6-1.1-12.8 3.4-17.4c4.1-4.2 7.8-8.7 11.3-13.5c1.7-2.3 3.3-4.6 4.8-6.9l.3-.5z" />
                    </svg>
                </button>
                <button id="share-button" onclick="toggleShare()">
                    <svg class="plane-icon" viewBox="0 0 24 24">
                        <path d="M2 21l21-9-21-9v7l15 2-15 2z" />
                    </svg>
                </button>
                <br><br><br><br>
                <p class="post-caption" style="text-align: left; ">spiderman</p>
            </div>

            <div class="post">
                <div class="post-header">
                    <img src="marvel.jpg" alt="Post Image" class="smalldp">
                    <h4 style="margin-right:370px;">marvel</h4>

                </div>
                <!-- <img src="dp.jpg" alt="Post Image" class="post-image"> -->
                <video class="post-image" src="spider.mp4" muted loop autoplay>

                </video>
                <button id="heart-button" onclick="toggleLike()" style="text-align:left">
                    <svg class="heart" viewBox="0 0 24 24">
                        <path
                            d="M12 21.35l-1.45-1.32C5.4 15.36 2 12.28 2 8.5 2 5.42 4.42 3 7.5 3c1.74 0 3.41.81 4.5 2.09C13.09 3.81 14.76 3 16.5 3 19.58 3 22 5.42 22 8.5c0 3.78-3.4 6.86-8.55 11.54L12 21.35z" />
                    </svg>
                </button>
                <button id="comment-button" onclick="toggleComment()">
                    <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 512 512" class="comment-icon">
                        <path
                            d="M123.6 391.3c12.9-9.4 29.6-11.8 44.6-6.4c26.5 9.6 56.2 15.1 87.8 15.1c124.7 0 208-80.5 208-160s-83.3-160-208-160S48 160.5 48 240c0 32 12.4 62.8 35.7 89.2c8.6 9.7 12.8 22.5 11.8 35.5c-1.4 18.1-5.7 34.7-11.3 49.4c17-7.9 31.1-16.7 39.4-22.7zM21.2 431.9c1.8-2.7 3.5-5.4 5.1-8.1c10-16.6 19.5-38.4 21.4-62.9C17.7 326.8 0 285.1 0 240C0 125.1 114.6 32 256 32s256 93.1 256 208s-114.6 208-256 208c-37.1 0-72.3-6.4-104.1-17.9c-11.9 8.7-31.3 20.6-54.3 30.6c-15.1 6.6-32.3 12.6-50.1 16.1c-.8 .2-1.6 .3-2.4 .5c-4.4 .8-8.7 1.5-13.2 1.9c-.2 0-.5 .1-.7 .1c-5.1 .5-10.2 .8-15.3 .8c-6.5 0-12.3-3.9-14.8-9.9c-2.5-6-1.1-12.8 3.4-17.4c4.1-4.2 7.8-8.7 11.3-13.5c1.7-2.3 3.3-4.6 4.8-6.9l.3-.5z" />
                    </svg>
                </button>
                <button id="share-button" onclick="toggleShare()">
                    <svg class="plane-icon" viewBox="0 0 24 24">
                        <path d="M2 21l21-9-21-9v7l15 2-15 2z" />
                    </svg>
                </button>
                <br><br><br><br>
                <p class="post-caption" style="text-align: left; ">spiderman</p>
            </div>


        </main>
    </center>
</body>

</html>