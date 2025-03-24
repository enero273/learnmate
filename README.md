<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>LearnMate - Your Learning Companion</title>
    <style>
       body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 0;
            background: url('backg.avif') no-repeat center center fixed;
            background-size: cover;
            color: #333;
        }
        header {
            background-color: rgba(51, 51, 51, 0.9); 
            color: white;
            display: flex;
            align-items: center;
            padding: 20px;
            flex-wrap: wrap;
            justify-content: space-between;
        }
        .logo {
            width: 50px;
            height: 50px;
            margin-right: 15px;
        }
        .motto {
            font-style: italic;
            font-size: 14px;
            color: #f8f8f8;
        }
        .search-container {
            display: flex;
            justify-content: center;
            flex-wrap: wrap;
            margin: 10px;
        }
        .search-bar {
            width: 80%;
            max-width: 400px;
            padding: 12px;
            font-size: 16px;
            border: 2px solid #ccc;
            border-radius: 4px;
        }
        .search-button {
            padding: 12px 15px;
            font-size: 16px;
            cursor: pointer;
            background-color: #ff5722;
            color: white;
            border: none;
            border-radius: 4px;
            margin-top: 10px;
        }
        .search-button:hover {
            background-color: #e64a19;
        }
        .container {
            display: flex;
            flex-direction: column;
            align-items: center;
            margin-top: 20px;
            padding: 10px;
        }
        .pdf-list, .pdf-viewer {
            width: 90%;
            max-width: 600px;
            padding: 20px;
            border: 1px solid #ccc;
            background-color: rgba(255, 255, 255, 0.9);
            border-radius: 8px;
            margin-bottom: 20px;
            text-align: center;
        }
        .pdf-list h3 {
            color: #333;
        }
        .pdf-list ul {
            list-style-type: none;
            padding: 0;
        }
        .pdf-list li {
            display: none;
            padding: 10px;
            margin-bottom: 10px;
            background-color: #ffcc80;
            cursor: pointer;
            border-radius: 4px;
            transition: background-color 0.3s;
        }
        .pdf-list li:hover {
            background-color: #ffb74d;
        }
        .pdf-viewer iframe {
            width: 100%;
            height: 400px;
        }
        footer {
            text-align: center;
            margin-top: 20px;
            background-color: rgba(51, 51, 51, 0.9);
            color: white;
            padding: 10px;
        }
        .menu-btn {
            font-size: 15px;
            cursor: pointer;
            padding: 10px;
            background: #ff5722;
            color: white;
            border: none;
            position: fixed;
            left: 10px;
            top: 10px;
            z-index: 1000;
            border-radius: 5px;
        }
        .side-menu {
            width: 0;
            position: fixed;
            top: 0;
            left: 0;
            height: 100%;
            background-color: rgba(0, 0, 0, 0.9);
            overflow-x: hidden;
            transition: 0.5s;
            padding-top: 60px;
        }
        .side-menu a {
            padding: 15px;
            text-decoration: none;
            font-size: 20px;
            color: white;
            display: block;
            transition: 0.3s;
        }
        .side-menu a:hover {
            background-color: #ff5722;
        }
        .close-btn {
            position: absolute;
            top: 10px;
            right: 20px;
            font-size: 30px;
            cursor: pointer;
            color: white;
        }
    </style>
</head>
<body>

<header>
    <button class="menu-btn" onclick="openMenu()">☰ Menu</button>
    <h1>LearnMate</h1>
    <p class="motto">"Empowering minds, one lesson at a time." ✨</p>
</header>

<div id="sideMenu" class="side-menu">
    <span class="close-btn" onclick="closeMenu()">&times;</span>
    <a href="#about">About</a>
    <a href="#contact">Contact</a>
    <a href="#lessons">Lessons</a>
</div>

<div class="search-container">
    <input type="text" id="searchBar" class="search-bar" placeholder="Search for a lesson..." onkeyup="searchLessons()">
    <button class="search-button" onclick="searchLessons()">🔍 Search</button>
</div>

<div class="container">
    <div class="pdf-list">
        <h3>📚 Select a PDF Lesson:</h3>
        <ul>
            <li onclick="viewPdf('1-IT Era Introduction.pdf')">📄 Lesson 1 - Era Introduction</li>
            <li onclick="viewPdf('2-IT Era Evolution.pdf')">🎨 Lesson 2 - Era Evolution</li>
            <li onclick="viewPdf('3-IT Era Role.pdf')">💻 Lesson 3 - Era Role</li>
            <li onclick="viewPdf('4-IT Era Risks.pdf')">🎐 Lesson 4 - Era Risks</li>
            <li onclick="viewPdf('5-IT Era Use.pdf')">🧨 Lesson 5 - Era Use</li>
            <li onclick="viewPdf('6-IT Era Future.pdf')">👓 Lesson 6 - Era Future</li>
            <li onclick="viewPdf('Fundamentals of Programming.pdf')">🧵 Lesson 7 - Fundamentals of Programming</li>
            <li onclick="viewPdf('Introduction to Programming L___.pdf')">🧵 Lesson 8 - Introduction to Programming</li>
            <li onclick="viewPdf('Introduction to Java Programming.pdf')">💻 Lesson 9 - Introduction to Java Programming</li>
        </ul>
    </div>
    <div class="pdf-viewer">
        <p>📖 Select a lesson to view its content.</p>
        <iframe id="pdfViewer" src="" frameborder="0"></iframe>
    </div>
</div>

<footer>
    <p>📘 LearnMate - Your Learning Companion. Created with ❤️</p>
</footer>

<script>
    function openMenu() {
        document.getElementById("sideMenu").style.width = "250px";
    }
    function closeMenu() {
        document.getElementById("sideMenu").style.width = "0";
    }
    function searchLessons() {
        const input = document.getElementById('searchBar').value.toLowerCase();
        const lessons = document.querySelectorAll('.pdf-list li');
        const pdfList = document.querySelector('.pdf-list ul');

        let found = false;

        lessons.forEach(lesson => {
            if (lesson.innerText.toLowerCase().includes(input)) {
                lesson.style.display = 'block';
                found = true;
            } else {
                lesson.style.display = 'none';
            }
        });

        // Hide the entire list if no search input or no matches
        pdfList.style.display = (input === '' || !found) ? 'none' : 'block';
    }
    function viewPdf(pdfUrl) {
        document.getElementById('pdfViewer').src = pdfUrl;
    }
</script>

</body>
</html>
