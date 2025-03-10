# Adityamusics-
Here you can find any type of music
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Unlimited Music Streaming</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>
    <h1>Search and Play Unlimited Songs</h1>
    <input type="text" id="searchBox" placeholder="Type song or artist...">
    <button onclick="searchMusic()">Search</button>
    <div id="results"></div>
    <audio id="audioPlayer" controls></audio>

    <script src="script.js"></script>
</body>
</html>
body {
    font-family: Arial, sans-serif;
    background-color: #f4f4f4;
    text-align: center;
    padding: 20px;
}

h1 {
    color: #333;
}

input[type="text"], button {
    padding: 10px;
    margin: 10px;
    font-size: 16px;
}

#results div {
    background-color: #fff;
    border: 1px solid #ddd;
    padding: 10px;
    margin: 5px;
    cursor: pointer;
}

#results div:hover {
    background-color: #f0f0f0;
}

audio {
    margin-top: 20px;
}
function searchMusic() {
    const query = document.getElementById('searchBox').value;
    const results = document.getElementById('results');
    results.innerHTML = 'Searching...';

    fetch(`https://www.googleapis.com/youtube/v3/search?part=snippet&q=${query}&type=video&key=YOUR_YOUTUBE_API_KEY`)
    .then(response => response.json())
    .then(data => {
        results.innerHTML = '';
        data.items.forEach(item => {
            const videoId = item.id.videoId;
            const title = item.snippet.title;
            const videoUrl = `https://www.youtube.com/watch?v=${videoId}`;
            const downloadUrl = `https://www.y2mate.com/youtube/${videoId}`;

            const div = document.createElement('div');
            div.innerHTML = `
                <strong>${title}</strong><br>
                <button onclick="playMusic('${videoUrl}')">Play</button>
                <button onclick="window.open('${downloadUrl}', '_blank')">Download</button>
            `;
            results.appendChild(div);
        });
    })
    .catch(error => {
        results.innerHTML = 'No results found.';
    });
}

function playMusic(url) {
    const player = document.getElementById('audioPlayer');
    player.src = url;
    player.play();
}
