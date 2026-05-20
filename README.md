<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>The Best Cars Miami</title>

<style>
body{
margin:0;
font-family:Arial;
background:#0b0f19;
color:white;
}

.hero{
background:#111;
padding:40px 20px;
text-align:center;
}

.grid{
display:grid;
grid-template-columns:repeat(auto-fit, minmax(250px,1fr));
gap:15px;
padding:20px;
}

.card{
background:#151b2e;
border-radius:12px;
overflow:hidden;
cursor:pointer;
}

.card img{
width:100%;
height:160px;
object-fit:cover;
}

.card .info{
padding:10px;
}

/* MODAL */
.modal{
display:none;
position:fixed;
top:0;
left:0;
width:100%;
height:100%;
background:rgba(0,0,0,0.9);
overflow:auto;
}

.modal-content{
background:#111;
margin:50px auto;
padding:20px;
width:90%;
max-width:600px;
border-radius:12px;
}

.modal img{
width:100%;
margin-bottom:10px;
border-radius:10px;
}

.close{
float:right;
font-size:25px;
cursor:pointer;
color:red;
}

.price{
color:#00e676;
font-weight:bold;
}
</style>
</head>

<body>

<div class="hero">
<h1>🚗 The Best Cars Miami</h1>
<p>Toca un carro para ver fotos</p>
</div>

<div class="grid">

<!-- CARRO 1 -->
<div class="card" onclick="openCar('mustang')">
<img src="https://images.unsplash.com/photo-1503376780353-7e6692767b70">
<div class="info">
<h3>Ford Mustang GT 2020</h3>
<p class="price">$23,500</p>
</div>
</div>

<!-- CARRO 2 -->
<div class="card" onclick="openCar('bmw')">
<img src="https://images.unsplash.com/photo-1493238792000-8113da705763">
<div class="info">
<h3>BMW 3 Series 2020</h3>
<p class="price">$18,500</p>
</div>
</div>

</div>

<!-- MODAL -->
<div id="modal" class="modal">
<div class="modal-content">

<span class="close" onclick="closeModal()">✖</span>

<div id="carContent"></div>

</div>
</div>

<script>

function openCar(car){

let content = "";

if(car === "mustang"){
content = `
<h2>Ford Mustang GT 2020</h2>
<p class="price">$23,500</p>

<img src="https://images.unsplash.com/photo-1503376780353-7e6692767b70">
<img src="https://images.unsplash.com/photo-1525609004556-c46c7d6cf023">
<img src="https://images.unsplash.com/photo-1542362567-b07e54358753">

<a href="https://wa.me/13050000000">Contactar por WhatsApp</a>
`;
}

if(car === "bmw"){
content = `
<h2>BMW 3 Series 2020</h2>
<p class="price">$18,500</p>

<img src="https://images.unsplash.com/photo-1493238792000-8113da705763">
<img src="https://images.unsplash.com/photo-1555215695-3004980ad54e">
<img src="https://images.unsplash.com/photo-1502877338535-766e1452684a">

<a href="https://wa.me/13050000000">Contactar por WhatsApp</a>
`;
}

document.getElementById("carContent").innerHTML = content;
document.getElementById("modal").style.display = "block";

}

function closeModal(){
document.getElementById("modal").style.display = "none";
}

</script>

</body>
</html>
