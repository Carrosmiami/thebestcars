<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>The Best Cars Miami</title>

<style>

body{
margin:0;
font-family:Arial,sans-serif;
background:#0b0f19;
color:white;
}

header{
background:#111;
padding:20px;
text-align:center;
position:sticky;
top:0;
z-index:100;
}

header h1{
margin:0;
cursor:pointer;
}

.controls{
display:flex;
flex-wrap:wrap;
gap:10px;
justify-content:center;
padding:15px;
}

input, select{
padding:10px;
border:none;
border-radius:8px;
}

.grid{
display:grid;
grid-template-columns:repeat(auto-fit,minmax(250px,1fr));
gap:15px;
padding:15px;
}

.card{
background:#151b2e;
border-radius:12px;
overflow:hidden;
cursor:pointer;
transition:0.2s;
}

.card:hover{
transform:scale(1.02);
}

.card img{
width:100%;
height:180px;
object-fit:cover;
}

.info{
padding:10px;
}

.price{
color:#00e676;
font-weight:bold;
font-size:18px;
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
z-index:999;
}

.modal-content{
background:#111827;
margin:40px auto;
padding:20px;
width:90%;
max-width:700px;
border-radius:12px;
}

.close{
float:right;
font-size:25px;
cursor:pointer;
color:red;
}

.slider{
position:relative;
}

.slider img{
width:100%;
border-radius:10px;
margin-bottom:10px;
}

.btn{
display:block;
text-align:center;
padding:12px;
border-radius:8px;
text-decoration:none;
margin-top:10px;
color:white;
}

.whatsapp{
background:#25D366;
}

.reserve{
background:#ff9800;
}

/* ADMIN PANEL */

#adminPanel{
display:none;
position:fixed;
bottom:20px;
right:20px;
background:#111827;
padding:15px;
border-radius:12px;
width:300px;
z-index:1000;
box-shadow:0 0 15px rgba(0,0,0,0.5);
}

#adminPanel input{
width:100%;
margin-bottom:10px;
}

.adminBtn{
background:#1e88e5;
padding:10px;
border:none;
width:100%;
border-radius:8px;
color:white;
font-size:16px;
cursor:pointer;
}

.deleteBtn{
background:red;
margin-top:10px;
}

</style>
</head>

<body>

<header>
<h1 id="secretLogo">🚗 The Best Cars Miami</h1>
<p>Luxury | Salvage | Clean Title Inventory</p>
</header>

<div class="controls">

<input type="text" id="search" placeholder="Buscar carro..." onkeyup="renderCars()">

<select id="priceFilter" onchange="renderCars()">
<option value="">Precio</option>
<option value="low">Menos de 15k</option>
<option value="mid">15k - 25k</option>
<option value="high">25k+</option>
</select>

</div>

<div class="grid" id="carGrid"></div>

<!-- MODAL CARRO -->

<div id="carModal" class="modal">
<div class="modal-content">

<span class="close" onclick="closeModal()">✖</span>

<div id="carDetails"></div>

</div>
</div>

<!-- ADMIN PANEL -->

<div id="adminPanel">

<h2>🔒 Admin Panel</h2>

<input type="text" id="carName" placeholder="Nombre del carro">

<input type="number" id="carPrice" placeholder="Precio">

<input type="number" id="carYear" placeholder="Año">

<input type="file" id="carImages" multiple accept="image/*">

<button class="adminBtn" onclick="addCar()">Agregar Carro</button>

</div>

<script>

let secretClicks = 0;

document.getElementById("secretLogo").addEventListener("click", ()=>{

secretClicks++;

if(secretClicks >= 5){

let pass = prompt("🔒 Password:");

if(pass === "miami123"){

document.getElementById("adminPanel").style.display="block";

}else{
alert("Wrong password");
}

secretClicks = 0;

}

});

let cars = JSON.parse(localStorage.getItem("cars")) || [

{
name:"Ford Mustang GT Premium",
price:23500,
year:2020,
imgs:[
"https://images.unsplash.com/photo-1503376780353-7e6692767b70"
]
},

{
name:"BMW 3 Series",
price:18500,
year:2020,
imgs:[
"https://images.unsplash.com/photo-1493238792000-8113da705763"
]
}

];

function saveCars(){
localStorage.setItem("cars", JSON.stringify(cars));
}

function renderCars(){

let grid = document.getElementById("carGrid");

let search = document.getElementById("search").value.toLowerCase();

let price = document.getElementById("priceFilter").value;

grid.innerHTML = "";

cars.filter(car=>{

if(search && !car.name.toLowerCase().includes(search)) return false;

if(price==="low" && car.price>15000) return false;
if(price==="mid" && (car.price<15000 || car.price>25000)) return false;
if(price==="high" && car.price<25000) return false;

return true;

}).forEach((car,index)=>{

grid.innerHTML += `

<div class="card" onclick="openCar(${index})">

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

function openCar(index){

let car = cars[index];

let images = "";

car.imgs.forEach(img=>{

images += `<img src="${img}">`;

});

document.getElementById("carDetails").innerHTML = `

<h2>${car.name}</h2>

<p>Año: ${car.year}</p>

<p class="price">$${car.price}</p>

<div class="slider">
${images}
</div>

<a class="btn whatsapp" href="https://wa.me/17542141799">📲 WhatsApp</a>

<a class="btn reserve" href="#">💳 Reservar Carro</a>

<button class="adminBtn deleteBtn" onclick="deleteCar(${index})">🗑 Borrar Carro</button>

`;

document.getElementById("carModal").style.display="block";

}

function closeModal(){
document.getElementById("carModal").style.display="none";
}

function addCar(){

let name = document.getElementById("carName").value;

let price = document.getElementById("carPrice").value;

let year = document.getElementById("carYear").value;

let files = document.getElementById("carImages").files;

if(!name || !price || !year || files.length===0){
alert("Completa todo");
return;
}

let imgs = [];

let loaded = 0;

for(let file of files){

let reader = new FileReader();

reader.onload = function(e){

imgs.push(e.target.result);

loaded++;

if(loaded === files.length){

cars.push({
name,
price,
year,
imgs
});

saveCars();

renderCars();

alert("🚗 Carro agregado");

document.getElementById("carName").value="";
document.getElementById("carPrice").value="";
document.getElementById("carYear").value="";
document.getElementById("carImages").value="";

}

};

reader.readAsDataURL(file);

}

}

function deleteCar(index){

if(confirm("Borrar este carro?")){

cars.splice(index,1);

saveCars();

renderCars();

closeModal();

}

}

renderCars();

</script>

</body>
</html>
