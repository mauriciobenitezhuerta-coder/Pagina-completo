
<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Recetario Gourmet Internacional</title>
<link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;600&display=swap" rel="stylesheet">

<style>
  :root { --primary: #6a5acd; --secondary: #836fff; --bg: #f3f0ff; }
  body { margin:0; font-family:'Poppins',sans-serif; background: var(--bg); }
  
  header {
    background: linear-gradient(90deg, var(--primary), var(--secondary));
    color: white; text-align: center; padding: 30px;
  }

  .user-auth {
    background: white; padding: 10px; text-align: right;
    box-shadow: 0 2px 5px rgba(0,0,0,0.1); font-size: 0.9rem;
  }

  .recipe-img { width: 100%; height: 180px; object-fit: cover; border-radius: 10px; margin-bottom: 15px; }

  .tabs { display:flex; justify-content:center; flex-wrap:wrap; background:white; padding:15px; position: sticky; top: 0; z-index: 100; box-shadow: 0 2px 10px rgba(0,0,0,0.1); }
  .tab-btn { background:#dcd6f7; border:none; margin:5px; padding:10px 20px; cursor:pointer; border-radius:20px; font-weight:600; transition: 0.3s; }
  .tab-btn.active { background: var(--primary); color:white; }
  
  .recipes-section { display:none; padding:40px; }
  .recipes-grid { display:grid; grid-template-columns:repeat(auto-fit,minmax(300px,1fr)); gap:25px; }
  .recipe-card { background:white; border-radius:15px; padding:20px; box-shadow:0 8px 20px rgba(0,0,0,.1); cursor:pointer; transition: 0.3s; }
  .recipe-card:hover { transform: translateY(-5px); }
  .recipe-card h3 a { text-decoration: none; color: var(--primary); }
  .recipe-card h3 a:hover { text-decoration: underline; }

  .details { max-height:0; overflow:hidden; transition:max-height .6s ease; margin-top:10px; font-size: 0.9rem; }
  .details h4 { color: var(--secondary); margin-bottom: 5px; }

  .comment-section { background: white; margin-top: 40px; padding: 25px; border-radius: 15px; max-width: 900px; margin: 40px auto; }
  .comment-input { width: 100%; padding: 10px; border-radius: 8px; border: 1px solid #ddd; margin-bottom: 10px; font-family: inherit; box-sizing: border-box; }
  .comment-btn { background: var(--primary); color: white; border: none; padding: 10px 20px; border-radius: 5px; cursor: pointer; font-weight: 600; }
  .comment-list { margin-top: 20px; border-top: 1px solid #eee; padding-top: 10px; text-align: left; }
  .comment-item { background: #f9f9f9; padding: 10px; border-radius: 5px; margin-bottom: 10px; border-left: 4px solid var(--primary); }

  .modal { display: none; position: fixed; z-index: 200; top: 0; left: 0; width: 100%; height: 100%; background: rgba(0,0,0,0.6); }
  .modal-content { background: white; width: 300px; margin: 100px auto; padding: 30px; border-radius: 15px; text-align: center; }
  .modal-content input { width: 90%; padding: 10px; margin: 10px 0; border: 1px solid #ddd; border-radius: 5px; }
  
  footer { text-align:center; padding:20px; background: var(--primary); color:white; margin-top:40px; }
</style>
</head>
<body>

<div class="user-auth">
  <span id="userWelcome">Bienvenido, Invitado</span> | 
  <button onclick="openModal()" id="authBtn" style="border:none; background:none; color:var(--primary); cursor:pointer; font-weight:600;">Iniciar Sesión</button>
</div>

<header>
  <h1>Recetario Gourmet Internacional</h1>
  <p>15 Sabores del Mundo en tu Pantalla</p>
</header>

<div class="tabs">
  <button class="tab-btn active" onclick="showSection(event,'america')">América</button>
  <button class="tab-btn" onclick="showSection(event,'europa')">Europa</button>
  <button class="tab-btn" onclick="showSection(event,'asia')">Asia</button>
  <button class="tab-btn" onclick="showSection(event,'africa')">África</button>
  <button class="tab-btn" onclick="showSection(event,'oceania')">Oceanía</button>
</div>

<section id="america" class="recipes-section" style="display:block;">
  <div class="recipes-grid">
    <div class="recipe-card" onclick="toggleDetails(this)">
      <img src="https://images.unsplash.com/photo-1535454014929-6028f178132e?w=500" class="recipe-img">
      <h3><a href="https://www.google.com/search?q=receta+ceviche+peruano" target="_blank">Ceviche Peruano</a></h3>
      <div class="details"><h4>Ingredientes:</h4><ul><li>Pescado fresco</li><li>Limón</li><li>Ají amarillo</li></ul></div>
    </div>
    <div class="recipe-card" onclick="toggleDetails(this)">
      <img src="https://images.unsplash.com/photo-1565299585323-38d6b0865b47?w=500" class="recipe-img">
      <h3><a href="https://www.google.com/search?q=receta+tacos+mexicanos" target="_blank">Tacos al Pastor</a></h3>
      <div class="details"><h4>Ingredientes:</h4><ul><li>Carne de cerdo</li><li>Achiote</li><li>Piña</li></ul></div>
    </div>
    <div class="recipe-card" onclick="toggleDetails(this)">
      <img src="https://images.unsplash.com/photo-1558030006-450675393462?w=500" class="recipe-img">
      <h3><a href="https://www.google.com/search?q=receta+filete+mignon" target="_blank">Filete Mignon</a></h3>
      <div class="details"><h4>Ingredientes:</h4><ul><li>Solomillo</li><li>Tocineta</li><li>Vino tinto</li></ul></div>
    </div>
  </div>
  <div class="comment-section">
    <h3>Opiniones de América</h3>
    <textarea class="comment-input" id="commentTextAmerica" placeholder="Escribe aquí..."></textarea>
    <button class="comment-btn" onclick="addComment('America')">Publicar</button>
    <div class="comment-list" id="listAmerica"></div>
  </div>
</section>

<section id="europa" class="recipes-section">
  <div class="recipes-grid">
    <div class="recipe-card" onclick="toggleDetails(this)">
      <img src="https://images.unsplash.com/photo-1513104890138-7c749659a591?w=500" class="recipe-img">
      <h3><a href="https://www.google.com/search?q=receta+pizza+margherita" target="_blank">Pizza Italiana</a></h3>
      <div class="details"><h4>Ingredientes:</h4><ul><li>Harina 00</li><li>Mozzarella</li><li>Albahaca</li></ul></div>
    </div>
    <div class="recipe-card" onclick="toggleDetails(this)">
      <img src="https://images.unsplash.com/photo-1539755530862-0123ef9539d0?w=500" class="recipe-img">
      <h3><a href="https://www.google.com/search?q=receta+paella+valenciana" target="_blank">Paella Española</a></h3>
      <div class="details"><h4>Ingredientes:</h4><ul><li>Arroz Bomba</li><li>Azafrán</li><li>Mariscos</li></ul></div>
    </div>
    <div class="recipe-card" onclick="toggleDetails(this)">
      <img src="https://images.unsplash.com/photo-1551024601-bec78aea704b?w=500" class="recipe-img">
      <h3><a href="https://www.google.com/search?q=receta+croissant" target="_blank">Croissant Francés</a></h3>
      <div class="details"><h4>Ingredientes:</h4><ul><li>Mantequilla</li><li>Harina</li><li>Levadura</li></ul></div>
    </div>
  </div>
  <div class="comment-section">
    <h3>Opiniones de Europa</h3>
    <textarea class="comment-input" id="commentTextEuropa" placeholder="Escribe aquí..."></textarea>
    <button class="comment-btn" onclick="addComment('Europa')">Publicar</button>
    <div class="comment-list" id="listEuropa"></div>
  </div>
</section>

<section id="asia" class="recipes-section">
  <div class="recipes-grid">
    <div class="recipe-card" onclick="toggleDetails(this)">
      <img src="https://images.unsplash.com/photo-1579871494447-9811cf80d66c?w=500" class="recipe-img">
      <h3><a href="https://www.google.com/search?q=receta+sushi" target="_blank">Sushi Japonés</a></h3>
      <div class="details"><h4>Ingredientes:</h4><ul><li>Arroz</li><li>Pescado</li><li>Alga Nori</li></ul></div>
    </div>
    <div class="recipe-card" onclick="toggleDetails(this)">
      <img src="https://images.unsplash.com/photo-1559339352-11d035aa65de?w=500" class="recipe-img">
      <h3><a href="https://www.google.com/search?q=receta+pad+thai" target="_blank">Pad Thai Tailandés</a></h3>
      <div class="details"><h4>Ingredientes:</h4><ul><li>Fideos de arroz</li><li>Camarones</li><li>Tamarindo</li></ul></div>
    </div>
    <div class="recipe-card" onclick="toggleDetails(this)">
      <img src="https://images.unsplash.com/photo-1585937421612-71104e4e2fd3?w=500" class="recipe-img">
      <h3><a href="https://www.google.com/search?q=receta+tikka+masala" target="_blank">Pollo Tikka Masala</a></h3>
      <div class="details"><h4>Ingredientes:</h4><ul><li>Pollo</li><li>Yogur</li><li>Especias</li></ul></div>
    </div>
  </div>
  <div class="comment-section">
    <h3>Opiniones de Asia</h3>
    <textarea class="comment-input" id="commentTextAsia" placeholder="Escribe aquí..."></textarea>
    <button class="comment-btn" onclick="addComment('Asia')">Publicar</button>
    <div class="comment-list" id="listAsia"></div>
  </div>
</section>

<section id="africa" class="recipes-section">
  <div class="recipes-grid">
    <div class="recipe-card" onclick="toggleDetails(this)">
      <img src="https://images.unsplash.com/photo-1541518763669-27fef04b14ea?w=500" class="recipe-img">
      <h3><a href="https://www.google.com/search?q=receta+cuscus+marroqui" target="_blank">Cuscús Marroquí</a></h3>
      <div class="details"><h4>Ingredientes:</h4><ul><li>Sémola</li><li>Verduras</li><li>Especias</li></ul></div>
    </div>
    <div class="recipe-card" onclick="toggleDetails(this)">
      <img src="https://images.unsplash.com/photo-1604329760661-e71dc83f8f26?w=500" class="recipe-img">
      <h3><a href="https://www.google.com/search?q=receta+jollof+rice" target="_blank">Arroz Jollof</a></h3>
      <div class="details"><h4>Ingredientes:</h4><ul><li>Arroz</li><li>Tomate</li><li>Pimientos</li></ul></div>
    </div>
    <div class="recipe-card" onclick="toggleDetails(this)">
      <img src="https://images.unsplash.com/photo-1635363638580-c2809d049eee?w=500" class="recipe-img">
      <h3><a href="https://www.google.com/search?q=receta+tagine" target="_blank">Tagine de Pollo</a></h3>
      <div class="details"><h4>Ingredientes:</h4><ul><li>Pollo</li><li>Limón en conserva</li><li>Aceitunas</li></ul></div>
    </div>
  </div>
  <div class="comment-section">
    <h3>Opiniones de África</h3>
    <textarea class="comment-input" id="commentTextAfrica" placeholder="Escribe aquí..."></textarea>
    <button class="comment-btn" onclick="addComment('Africa')">Publicar</button>
    <div class="comment-list" id="listAfrica"></div>
  </div>
</section>

<section id="oceania" class="recipes-section">
  <div class="recipes-grid">
    <div class="recipe-card" onclick="toggleDetails(this)">
      <img src="https://images.unsplash.com/photo-1589119908995-c6837fa14848?w=500" class="recipe-img">
      <h3><a href="https://www.google.com/search?q=receta+pavlova" target="_blank">Pavlova Neozelandesa</a></h3>
      <div class="details"><h4>Ingredientes:</h4><ul><li>Claras de huevo</li><li>Azúcar</li><li>Frutos rojos</li></ul></div>
    </div>
    <div class="recipe-card" onclick="toggleDetails(this)">
      <img src="https://images.unsplash.com/photo-1601315379734-22551068827b?w=500" class="recipe-img">
      <h3><a href="https://www.google.com/search?q=receta+meat+pie+australiano" target="_blank">Meat Pie Australiano</a></h3>
      <div class="details"><h4>Ingredientes:</h4><ul><li>Hojaldre</li><li>Carne picada</li><li>Salsa Gravy</li></ul></div>
    </div>
    <div class="recipe-card" onclick="toggleDetails(this)">
      <img src="https://images.unsplash.com/photo-1544644304-66b99660c631?w=500" class="recipe-img">
      <h3><a href="https://www.google.com/search?q=receta+lamingtons" target="_blank">Lamingtons</a></h3>
      <div class="details"><h4>Ingredientes:</h4><ul><li>Bizcocho</li><li>Chocolate</li><li>Coco</li></ul></div>
    </div>
  </div>
  <div class="comment-section">
    <h3>Opiniones de Oceanía</h3>
    <textarea class="comment-input" id="commentTextOceania" placeholder="Escribe aquí..."></textarea>
    <button class="comment-btn" onclick="addComment('Oceania')">Publicar</button>
    <div class="comment-list" id="listOceania"></div>
  </div>
</section>

<div id="loginModal" class="modal">
  <div class="modal-content">
    <h3>Acceso Gourmet</h3>
    <input type="email" id="emailInput" placeholder="Email">
    <input type="password" id="passInput" placeholder="Contraseña">
    <button class="comment-btn" style="width:100%" onclick="login()">Entrar</button>
    <p onclick="closeModal()" style="cursor:pointer; font-size: 0.8rem; margin-top: 10px;">Cerrar</p>
  </div>
</div>

<footer>© 2026 Recetario Gourmet Internacional</footer>

<script>
  let currentUser = "Invitado";

  function showSection(event,id){
    document.querySelectorAll('.recipes-section').forEach(s=>s.style.display='none');
    document.querySelectorAll('.tab-btn').forEach(b=>b.classList.remove('active'));
    document.getElementById(id).style.display='block';
    event.target.classList.add('active');
  }

  function toggleDetails(card){
    let d=card.querySelector('.details');
    if(d) d.style.maxHeight=d.style.maxHeight?null:d.scrollHeight+"px";
  }

  function openModal() { document.getElementById('loginModal').style.display='block'; }
  function closeModal() { document.getElementById('loginModal').style.display='none'; }

  function login() {
    let email = document.getElementById('emailInput').value;
    if(email.includes('@')) {
      currentUser = email.split('@')[0];
      document.getElementById('userWelcome').innerText = "Hola, " + currentUser;
      document.getElementById('authBtn').style.display = 'none';
      closeModal();
    }
  }

  function addComment(section) {
    let input = document.getElementById('commentText' + section);
    let list = document.getElementById('list' + section);
    if(input.value.trim()==="") return;
    let div = document.createElement('div');
    div.className = 'comment-item';
    div.innerHTML = `<strong>${currentUser}:</strong> ${input.value}`;
    list.prepend(div);
    input.value = "";
  }
</script>
</body>
</html>
