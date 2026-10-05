<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <title>Gerador Infos Bafos</title>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/html2canvas/1.4.1/html2canvas.min.js"></script>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Inter:wght@400;900&display=swap');
        
        body { font-family: 'Inter', sans-serif; background: #121212; color: #fff; margin: 0; padding: 20px; display: flex; gap: 30px; flex-wrap: wrap; }
        .controls { width: 400px; background: #1e1e1e; padding: 20px; border-radius: 12px; }
        .controls h2 { color: #ff007f; margin-top: 0; }
        .form-group { margin-bottom: 15px; }
        label { display: block; margin-bottom: 5px; font-weight: bold; color: #ccc; }
        input[type="text"], textarea, input[type="file"] { width: 100%; padding: 10px; background: #2a2a2a; border: 1px solid #444; color: #fff; border-radius: 6px; box-sizing: border-box; }
        textarea { height: 80px; resize: vertical; }
        button { width: 100%; padding: 15px; background: #ff007f; color: white; border: none; border-radius: 6px; font-size: 16px; font-weight: bold; cursor: pointer; margin-top: 10px; }
        button:hover { background: #d6006b; }

        /* Layout do Post (1080x1080 escalado) */
        #post-canvas {
            width: 540px; height: 540px;
            background: #050002;
            border: 8px solid #ff007f;
            position: relative;
            overflow: hidden;
            display: flex; flex-direction: column; justify-content: space-between;
            box-sizing: border-box;
        }
        
        .badge-urgente {
            position: absolute; top: 20px; left: 50%; transform: translateX(-50%);
            background: #ffe600; color: #000; font-weight: 900;
            padding: 8px 20px; font-size: 18px; border-radius: 8px; z-index: 10;
        }
        
        .image-box {
            width: 100%; height: 320px; background: #1a1a1a;
            display: flex; justify-content: center; align-items: flex-end;
            margin-top: 40px;
        }
        .image-box img { width: 100%; height: 100%; object-fit: cover; }
        
        .content-box { text-align: center; padding: 10px 20px; z-index: 2; }
        .post-title { font-size: 32px; font-weight: 900; text-transform: uppercase; margin: 0; line-height: 1.1; color: #fff; }
        .post-title span { color: #ffe600; }
        .post-desc { font-size: 16px; color: #ddd; line-height: 1.3; margin-top: 10px; }
        
        .footer-post {
            display: flex; justify-content: space-between; align-items: center;
            border-top: 2px solid #ff007f; padding: 10px 20px; margin-bottom: 5px;
        }
        .logo-area { font-weight: 900; color: #ff007f; font-size: 18px; }
        .siga { color: #ffe600; font-weight: 900; font-size: 14px; }
    </style>
</head>
<body>

    <div class="controls">
        <h2>⚡ Gerador Infos Bafos</h2>
        
        <div class="form-group">
            <label>1. Carregar Foto:</label>
            <input type="file" id="input-file" accept="image/*" onchange="loadFile(event)">
        </div>

        <div class="form-group">
            <label>2. Manchete (use &lt;span&gt; para amarelo):</label>
            <input type="text" id="input-title" value="VIROU UM <span>CIRCO!</span>" oninput="updateContent()">
        </div>

        <div class="form-group">
            <label>3. Resumo da fofoca:</label>
            <textarea id="input-desc" oninput="updateContent()">Marina Ruy Barbosa quebra o silêncio sobre boatos de romance com José Loreto e desabafa: "É cruel misturarem mentiras com o nosso trabalho."</textarea>
        </div>
        
        <button onclick="downloadImage()">BAIXAR ARTE PARA INSTAGRAM</button>
    </div>

    <div>
        <div id="post-canvas">
            <div class="badge-urgente">🔥 URGENTE</div>
            <div class="image-box">
                <img id="preview-img" src="https://images.unsplash.com/photo-1534528741775-53994a69daeb?w=500" alt="Foto Base">
            </div>
            <div class="content-box">
                <div id="preview-title" class="post-title">VIROU UM <span>CIRCO!</span></div>
                <div id="preview-desc" class="post-desc">Marina Ruy Barbosa quebra o silêncio sobre boatos de romance com José Loreto e desabafa: "É cruel misturarem mentiras com o nosso trabalho."</div>
            </div>
            <div class="footer-post">
                <div class="logo-area">🗣️ INFOS BAFOS</div>
                <div class="siga">SIGA @INFOSBAFOS PARA MAIS!</div>
            </div>
        </div>
    </div>

    <script>
        function loadFile(event) {
            const reader = new FileReader();
            reader.onload = function(){
                const output = document.getElementById('preview-img');
                output.src = reader.result;
            };
            if(event.target.files[0]) {
                reader.readAsDataURL(event.target.files[0]);
            }
        }

        function updateContent() {
            document.getElementById('preview-title').innerHTML = document.getElementById('input-title').value;
            document.getElementById('preview-desc').innerText = document.getElementById('input-desc').value;
        }

        function downloadImage() {
            const element = document.getElementById('post-canvas');
            html2canvas(element, { scale: 2, backgroundColor: null }).then(canvas => {
                const link = document.createElement('a');
                link.download = 'infos-bafos-post.png';
                link.href = canvas.toDataURL("image/png");
                link.click();
            });
        }
    </script>
</body>
</html>
