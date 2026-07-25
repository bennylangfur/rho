# rho
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>BENNY'S MUSIC</title>
  <style>
    :root {
      --bg-color: #121212;
      --card-bg: #1e1e1e;
      --text-color: #f5f5f5;
      --accent-color: #bb86fc;
    }

    body {
      font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif;
      background-color: var(--bg-color);
      color: var(--text-color);
      margin: 0;
      padding: 40px 20px;
      display: flex;
      flex-direction: column;
      align-items: center;
      min-height: 100vh;
    }

    h1 {
      font-size: 2.5rem;
      letter-spacing: 2px;
      margin-bottom: 10px;
      text-transform: uppercase;
    }

    p.subtitle {
      color: #aaa;
      margin-bottom: 40px;
    }

    /* Album Grid View */
    .grid {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(180px, 1fr));
      gap: 25px;
      width: 100%;
      max-width: 1000px;
    }

    .album-card {
      background: var(--card-bg);
      border-radius: 12px;
      overflow: hidden;
      cursor: pointer;
      transition: transform 0.2s ease, box-shadow 0.2s ease;
      text-align: center;
      padding-bottom: 15px;
    }

    .album-card:hover {
      transform: translateY(-5px);
      box-shadow: 0 8px 20px rgba(0, 0, 0, 0.5);
    }

    .album-card img {
      width: 100%;
      aspect-ratio: 1/1;
      object-fit: cover;
    }

    .album-card h3 {
      font-size: 1.1rem;
      margin: 12px 10px 0;
    }

    /* Detail View for Download Codes */
    .detail-view {
      display: none;
      background: var(--card-bg);
      padding: 30px;
      border-radius: 12px;
      max-width: 500px;
      width: 100%;
      text-align: center;
      box-shadow: 0 10px 30px rgba(0,0,0,0.5);
    }

    .detail-view img {
      width: 250px;
      height: 250px;
      border-radius: 8px;
      object-fit: cover;
      margin-bottom: 20px;
    }

    .code-box {
      background: #111;
      border: 1px dashed var(--accent-color);
      padding: 12px;
      margin: 10px 0;
      font-family: monospace;
      font-size: 1.1rem;
      border-radius: 6px;
      color: #fff;
    }

    .btn {
      display: inline-block;
      margin-top: 20px;
      padding: 10px 20px;
      background: var(--accent-color);
      color: #000;
      font-weight: bold;
      border-radius: 20px;
      text-decoration: none;
      cursor: pointer;
      border: none;
    }

    .btn-back {
      background: transparent;
      color: #aaa;
      border: 1px solid #aaa;
      margin-right: 10px;
    }
  </style>
</head>
<body>

  <h1>BENNY'S MUSIC</h1>
  <p class="subtitle" id="sub-header">Choose an album to download</p>

  <!-- GALLERY VIEW -->
  <div class="grid" id="album-grid">
    <div class="album-card" onclick="showAlbum('rabbit-hole')">
      <img src="images/rabbit-hole.jpg" alt="Rabbit Hole Orchestra">
      <h3>Rabbit Hole Orchestra</h3>
    </div>
    <div class="album-card" onclick="showAlbum('morph-dwarf')">
      <img src="images/morph-dwarf.jpg" alt="Morph Dwarf">
      <h3>Morph Dwarf</h3>
    </div>
    <div class="album-card" onclick="showAlbum('forgotten-kingdoms')">
      <img src="images/forgotten-kingdoms.jpg" alt="Forgotten Kingdoms">
      <h3>Forgotten Kingdoms</h3>
    </div>
    <div class="album-card" onclick="showAlbum('earth-jam')">
      <img src="images/earth-jam.jpg" alt="Earth Jam">
      <h3>Earth Jam</h3>
    </div>
    <div class="album-card" onclick="showAlbum('kaleidoscope-karavan')">
      <img src="images/kaleidoscope-karavan.jpg" alt="Kaleidoscope Karavan">
      <h3>Kaleidoscope Karavan</h3>
    </div>
  </div>

  <!-- DOWNLOAD DETAILS VIEW -->
  <div class="detail-view" id="detail-view">
    <img id="detail-img" src="" alt="Album Cover">
    <h2 id="detail-title">Album Title</h2>
    <p>Redeem your download code below:</p>
    
    <div id="code-container"></div>

    <button class="btn btn-back" onclick="showGrid()">← Back to Albums</button>
    <a id="redeem-link" href="#" target="_blank" class="btn">Redeem Code</a>
  </div>

  <script>
    // EDIT YOUR ALBUM CODES & REDEEM LINKS HERE
    const albums = {
      'rabbit-hole': {
        title: 'Rabbit Hole Orchestra',
        img: 'images/rabbit-hole.jpg',
        codes: ['RABBIT-2026-X1', 'RABBIT-2026-X2'],
        redeemUrl: 'https://bandcamp.com/yum'
      },
      'morph-dwarf': {
        title: 'Morph Dwarf',
        img: 'images/morph-dwarf.jpg',
        codes: ['DWARF-99-A', 'DWARF-99-B'],
        redeemUrl: 'https://bandcamp.com/yum'
      },
      'forgotten-kingdoms': {
        title: 'Forgotten Kingdoms',
        img: 'images/forgotten-kingdoms.jpg',
        codes: ['KINGDOM-77-Q'],
        redeemUrl: 'https://bandcamp.com/yum'
      },
      'earth-jam': {
        title: 'Earth Jam',
        img: 'images/earth-jam.jpg',
        codes: ['EARTH-JAM-01'],
        redeemUrl: 'https://bandcamp.com/yum'
      },
      'kaleidoscope-karavan': {
        title: 'Kaleidoscope Karavan',
        img: 'images/kaleidoscope-karavan.jpg',
        codes: ['KARAVAN-88-Z'],
        redeemUrl: 'https://bandcamp.com/yum'
      }
    };

    function showAlbum(key) {
      const album = albums[key];
      document.getElementById('album-grid').style.display = 'none';
      document.getElementById('sub-header').style.display = 'none';
      
      document.getElementById('detail-img').src = album.img;
      document.getElementById('detail-title').innerText = album.title;
      document.getElementById('redeem-link').href = album.redeemUrl;

      const codeContainer = document.getElementById('code-container');
      codeContainer.innerHTML = '';
      album.codes.forEach(code => {
        const box = document.createElement('div');
        box.className = 'code-box';
        box.innerText = code;
        codeContainer.appendChild(box);
      });

      document.getElementById('detail-view').style.display = 'block';
    }

    function showGrid() {
      document.getElementById('detail-view').style.display = 'none';
      document.getElementById('album-grid').style.display = 'grid';
      document.getElementById('sub-header').style.display = 'block';
    }
  </script>
</body>
</html>
