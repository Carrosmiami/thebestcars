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

header{
padding:20px;
text-align:center;
background:#111;
}

.controls{
display:flex;
flex-wrap:wrap;
gap:10px;
padding:15px;
justify-content:center;
}

input, select{
padding:10px;
border-radius:8px;
border:none;
}

.grid{
display:grid;
grid-template-columns:repeat(auto-fit, minmax(250px,1fr));
gap:15px;
padding:15px;
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

.price{
color:#00e676;
font-weight:bold;
}

/* MODAL */
.modal{
display:none;
position:fixed;
top:0;
left:0;
width:100%;
height:100%;
background:rgba(0,0,0,0.95);
overflow:auto;
}

.modal-content{
background:#111;
margin:40px auto;
padding:20px;
width:90%;
max-width:600px;
border-radius:12px;
}

.close{
float:right;
font-size:22px;
cursor:pointer;
color:red;
}

/* SLIDER */
.slider img{
width:100%;
border-radius:10px;
margin-bottom:10px;
}

.btn{
display:block;
text-align:center;
background:#25D366;
padding:10px;
border-radius:8px;
color:white;
text-decoration:none;
margin-top:10px;
}

.reserve{
background:#ff9800;
}

.admin{
background:#1e88e5;
margin:15px;
padding:15px;
border-radius:10px;
}
</style>
</head>

<body>

<header>
<h1>🚗 The Best Cars Miami</h1>
</header>

<!-- CONTROLES -->
<div class="controls">
<input type="text" id="search" placeholder="Buscar carro..." onkeyup="renderCars()">

<select id="priceFilter" onchange="renderCars()">
<option value="">Precio</option>
<option value="low">Menos de 15k</option>
<option value="mid">15k - 25k</option>
<option value="high">25k+</option>
</select>

<select id="yearFilter" onchange="renderCars()">
<option value="">Año</option>
<option value="2020">2020+</option>
<option value="2018">2018+</option>
</select>
</div>

<!-- PANEL ADMIN SIMPLE -->
<div class="admin">
<h3>📊 Agregar carro (modo simple)</h3>
<p>Ejemplo rápido (editas código y se agrega)</p>
</div>

<!-- INVENTARIO -->
<div class="grid" id="carGrid"></div>

<!-- MODAL -->
<div id="modal" class="modal">
<div class="modal-content">

<span class="close" onclick="closeModal()">✖</span>

<div id="modalBody"></div>

</div>
</div>

<script>

let cars = [
{
name:"Ford Mustang GT",
price:23500,
year:2020,
imgs:[
"[https://images.unsplash.com/photo-1503376780353-7e6692767b70](https://github.com/8ba79c37-09c3-4db1-a946-026c9b89f32b)",
"https://images.unsplash.com/photo-1525609004556-c46c7d6cf023",
"https://images.unsplash.com/photo-1542362567-b07e54358753"
]
},
{
name:"BMW 3 Series",
price:18500,
year:2020,
imgs:[
"https://images.unsplash.com/photo-1493238792000-8113da705763",
"https://images.unsplash.com/photo-1555215695-3004980ad54e",
"https://images.unsplash.com/photo-1502877338535-766e1452684a"
]
}
];

function renderCars(){

let grid = document.getElementById("carGrid");
let search = document.getElementById("search").value.toLowerCase();
let price = document.getElementById("priceFilter").value;
let year = document.getElementById("yearFilter").value;

grid.innerHTML = "";

cars.filter(car=>{

if(search && !car.name.toLowerCase().includes(search)) return false;

if(price==="low" && car.price>15000) return false;
if(price==="mid" && (car.price<15000 || car.price>25000)) return false;
if(price==="high" && car.price<25000) return false;

if(year==="2020" && car.year<2020) return false;
if(year==="2018" && car.year<2018) return false;

return true;

}).forEach((car,i)=>{

grid.innerHTML += `
<div class="card" onclick="openCar(${i})">
<img src="${car.imgs[0]}">
<div class="info">
<h3>${car.name}</h3>
<p>Año: ${car.year}</p>
<p class="price">$${car.price}</p>
</div>
</div>
`;

});

}

function openCar(i){

let car = cars[i];

let images = car.imgs.map(img=>`<img src="${img}">`).join("");

document.getElementById("modalBody").innerHTML = `
<h2>${car.name}</h2>
<p class="price">$${car.price}</p>

<div class="slider">
${images}
</div>

<a class="btn" href="https://wa.me/13050000000">📲 Contactar</a>
<a class="btn reserve" href="#">💳 Reservar carro</a>
`;

document.getElementById("modal").style.display="block";
}

function closeModal(){
document.getElementById("modal").style.display="none";
}

renderCars();

</script>

</body>
</html>
