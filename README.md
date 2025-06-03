<!DOCTYPE html>
<html>
<head>
  <title>Multiple YouTube Video Embeds</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background: #fafafa;
      text-align: center;
      padding: 40px;
    }
    input, button {
      padding: 10px;
      margin: 10px;
      width: 320px;
      font-size: 16px;
    }
    button {
      background-color: #ff0000;
      color: white;
      border: none;
      cursor: pointer;
    }
    #videoContainer {
      margin-top: 30px;
      display: flex;
      flex-wrap: wrap;
      justify-content: center;
      gap: 15px;
    }
    iframe {
      width: 320px;
      height: 180px;
      border: none;
    }
  </style>
</head>
<body>

  <h1>Embed Multiple YouTube Videos</h1>

  <input type="text" id="ytLink" placeholder="Enter YouTube video URL" />
  <br/>
  <input type="number" id="numVideos" placeholder="Number of players" min="1" />
  <br/>
  <button onclick="embedVideos()">Show Videos</button>

  <div id="videoContainer"></div>

  <script>
    function getVideoId(url) {
      try {
        const u = new URL(url);
        if (u.hostname === "youtu.be") {
          return u.pathname.slice(1);
        }
        return u.searchParams.get("v");
      } catch {
        return null;
      }
    }

    function embedVideos() {
      const link = document.getElementById("ytLink").value.trim();
      const count = parseInt(document.getElementById("numVideos").value);
      const container = document.getElementById("videoContainer");
      container.innerHTML = "";

      const videoId = getVideoId(link);
      if (!videoId) {
        alert("Please enter a valid YouTube link.");
        return;
      }
      if (isNaN(count) || count < 1) {
        alert("Please enter a valid number.");
        return;
      }

      for (let i = 0; i < count; i++) {
        const iframe = document.createElement("iframe");
        iframe.src = `https://www.youtube.com/embed/${videoId}`;
        iframe.allow = "accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture";
        iframe.allowFullscreen = true;
        container.appendChild(iframe);
      }
    }
  </script>

</body>
</html>
