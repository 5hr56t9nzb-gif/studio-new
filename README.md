# studio-new
from pathlib import Path
from zipfile import ZipFile

root = Path("/mnt/data/StudioSMMakeup_Completo")
(root / "imagens").mkdir(parents=True, exist_ok=True)

html = """<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Studio SM Makeup</title>
<link href="https://fonts.googleapis.com/css2?family=Cormorant+Garamond:wght@400;600&family=Montserrat:wght@300;400;500&display=swap" rel="stylesheet">
<link rel="stylesheet" href="style.css">
</head>
<body>

<header>
<img src="imagens/logo.png" class="logo">
<nav>
<a href="#sobre">Sobre</a>
<a href="#servicos">Serviços</a>
<a href="#galeria">Galeria</a>
<a href="#contato">Contato</a>
</nav>
<a class="btn" href="https://wa.me/558421325564">Orçamento</a>
</header>

<section class="hero">
<div>
<h1>Studio SM Makeup</h1>
<p>Realçando sua beleza para momentos inesquecíveis.</p>
<a class="btn" href="https://wa.me/558421325564">Solicitar Orçamento</a>
</div>
<img src="imagens/banner.jpg">
</section>

<section id="servicos">
<h2>Serviços</h2>
<div class="cards">
<div class="card">Maquiagem Social</div>
<div class="card">Maquiagem Artística</div>
<div class="card">Maquiagem + Escova</div>
<div class="card">Maquiagem + Babyliss</div>
</div>
</section>

<section id="sobre" class="sobre">
<img src="imagens/sobre.jpg">
<div>
<h2>Sobre o Studio</h2>
<p>Atendimento personalizado, técnicas modernas e foco em valorizar a beleza única de cada cliente.</p>
</div>
</section>

<section id="galeria">
<h2>Galeria</h2>
<div class="galeria">
<img src="imagens/galeria1.jpg">
<img src="imagens/galeria2.jpg">
<img src="imagens/galeria3.jpg">
</div>
</section>

<section id="contato">
<h2>Contato</h2>
<p>WhatsApp: (84) 2132-5564</p>
<p>Instagram: @studiosm.makeup</p>
<p>Parnamirim/RN</p>
</section>

<footer>© Studio SM Makeup</footer>
</body>
</html>"""

css = """
body{margin:0;font-family:Montserrat,sans-serif;background:#fff;color:#222}
header{display:flex;justify-content:space-between;align-items:center;padding:15px 5%;box-shadow:0 2px 8px rgba(0,0,0,.08);position:sticky;top:0;background:#fff}
.logo{height:70px}
nav a{text-decoration:none;color:#222;margin:0 10px}
.btn{background:#b48a3c;color:#fff;padding:12px 20px;border-radius:6px;text-decoration:none}
.hero,.sobre{display:grid;grid-template-columns:1fr 1fr;gap:40px;padding:60px 8%;align-items:center}
.hero img,.sobre img,.galeria img{width:100%;border-radius:12px}
h1,h2{font-family:'Cormorant Garamond',serif}
h1{font-size:56px}
#servicos,#galeria,#contato{text-align:center;padding:60px 8%}
.cards{display:grid;grid-template-columns:repeat(4,1fr);gap:20px}
.card{padding:30px;border:1px solid #eee;border-radius:10px}
.galeria{display:grid;grid-template-columns:repeat(3,1fr);gap:20px}
footer{background:#111;color:#fff;text-align:center;padding:20px}
@media(max-width:768px){
.hero,.sobre,.cards,.galeria{grid-template-columns:1fr}
nav{display:none}
h1{font-size:40px}
}
"""

(root/"index.html").write_text(html, encoding="utf-8")
(root/"style.css").write_text(css, encoding="utf-8")

(root/"imagens"/"COLOQUE_AQUI_SUAS_IMAGENS.txt").write_text(
"Adicione: logo.png, banner.jpg, sobre.jpg, galeria1.jpg, galeria2.jpg, galeria3.jpg",
encoding="utf-8"
)

zip_path="/mnt/data/StudioSMMakeup_Completo.zip"
with ZipFile(zip_path,"w") as z:
    for f in root.rglob("*"):
        z.write(f, f.relative_to(root))

print(zip_path)