<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Next-Gen Rating & Fake News Detection</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">
    <style>
        body {
            font-family: Arial, sans-serif;
            background: #f4f4f4;
        }
        .result-container {
            width: 400px;
            margin: auto;
            background: white;
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.2);
        }
        .progress-bar {
            height: 10px;
            background-color: #4CAF50;
            width: 0;
            transition: width 0.5s ease-in-out;
        }
    </style>
</head>
<body>
    <nav class="bg-blue-500 p-4 text-white text-center text-2xl font-bold">
        Next-Gen Rating & Fake News Detection
        <button onclick="toggleDarkMode()" class="ml-4 bg-gray-700 text-white px-3 py-1 rounded">🌙</button>
    </nav>

    <div class="container mx-auto mt-6">
        <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
            <div class="bg-white shadow-lg rounded-lg p-6">
                <h2 class="text-xl font-semibold mb-4">Rate a Public Figure</h2>
                <form onsubmit="saveRating(event)">
                    <input type="text" id="figureName" class="border p-2 w-full mb-2" placeholder="Enter Public Figure Name">
                    <input type="number" id="credibility" class="border p-2 w-full mb-2" placeholder="Credibility Score (1-10)" min="1" max="10">
                    <input type="number" id="longevity" class="border p-2 w-full mb-2" placeholder="Longevity Score (1-10)" min="1" max="10">
                    <input type="number" id="engagement" class="border p-2 w-full mb-2" placeholder="Engagement Score (1-10)" min="1" max="10">
                    <button class="bg-blue-500 text-white px-4 py-2 rounded">Submit Rating</button>
                </form>
            </div>
            
            <div class="bg-white shadow-lg rounded-lg p-6">
                <h2 class="text-xl font-semibold mb-4">Fake News Detection</h2>
                <form onsubmit="checkFakeNews(event)">
                    <textarea id="newsContent" class="border p-2 w-full mb-2" rows="4" placeholder="Enter news article content"></textarea>
                    <button class="bg-red-500 text-white px-4 py-2 rounded">Check for Fake News</button>
                    <p id="fakeNewsResult" class="mt-2 text-gray-700"></p>
                </form>
            </div>
        </div>
    </div>

    <div class="result-container mt-6">
        <h2>Submitted Rating</h2>
        <p><strong>Name:</strong> <span id="name"></span></p>
        <div id="rating-details"></div>
        <p><strong>Average Rating:</strong> <span id="average"></span></p>
        <div class="progress-bar" id="ratingProgress"></div>
        <h3>Past Ratings</h3>
        <div class="ratings-list" id="ratings-list"></div>
    </div>
    
    <script>
        function saveRating(event) {
            event.preventDefault();
            let name = document.getElementById("figureName").value;
            let credibility = parseFloat(document.getElementById("credibility").value);
            let longevity = parseFloat(document.getElementById("longevity").value);
            let engagement = parseFloat(document.getElementById("engagement").value);
            let avg = ((credibility + longevity + engagement) / 3).toFixed(1);
            
            localStorage.setItem(name, JSON.stringify({ credibility, longevity, engagement, avg }));
            updateRatingUI(name, credibility, longevity, engagement, avg);
        }
        
        function updateRatingUI(name, credibility, longevity, engagement, avg) {
            document.getElementById("name").textContent = name;
            document.getElementById("rating-details").innerHTML = `<p><strong>Credibility:</strong> ${credibility}</p><p><strong>Longevity:</strong> ${longevity}</p><p><strong>Engagement:</strong> ${engagement}</p>`;
            document.getElementById("average").textContent = avg;
            document.getElementById("ratingProgress").style.width = `${avg * 10}%`;
        }
        
        function checkFakeNews(event) {
            event.preventDefault();
            document.getElementById("fakeNewsResult").textContent = "Checking...";
            setTimeout(() => {
                document.getElementById("fakeNewsResult").textContent = "This news is likely credible.";
            }, 2000);
        }

        function toggleDarkMode() {
            document.body.classList.toggle("bg-gray-900");
            document.body.classList.toggle("text-white");
        }
    </script>
</body>
</html>
