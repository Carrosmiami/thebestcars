
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
background:#111;
padding:20px;
text-align:center;
}

header h1{
cursor:pointer;
}

.controls{
padding:15px;
text-align:center;
}

input{
padding:10px;
border-radius:8px;
border:none;
width:80%;
max-width:300px;
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

.slider img{
width:100%;
margin-bottom:10px;
border-radius:10px;
}

.btn{
display:block;
text-align:center;
padding:12px;
border-radius:8px;
margin-top:10px;
text-decoration:none;
color:white;
cursor:pointer;
}

.whatsapp{background:#25D366;}
.edit{background:#1e88e5;}
.delete{background:#e53935;}
.add{background:#ff9800;margin-top:10px;}

/* ADMIN */
#adminPanel{
display:none;
position:fixed;
bottom:20px;
right:20px;
background:#111;
padding:15px;
border-radius:12px;
width:280px;
z-index:1000;
}

#adminPanel input{
width:100%;
margin-bottom:8px;
padding:8px;
border-radius:6px;
border:none;
}
</style>
</head>

<body>

<header>
<h1 id="secret">🚗 The Best Cars Miami</h1>
</header>

<div class="controls">
<input id="search" placeholder="Buscar carro..." onkeyup="render()">
</div>

<div class="grid" id="grid"></div>

<!-- MODAL -->
<div id="modal" class="modal">
<div class="modal-content">
<span class="close" onclick="closeModal()">✖</span>
<div id="modalBody"></div>
</div>
</div>

<!-- ADMIN -->
<div id="adminPanel">

<h3>🔒 Admin Panel</h3>

<input id="name" placeholder="Nombre">
<input id="price" placeholder="Precio">
<input id="year" placeholder="Año">
<input id="imgs" placeholder="Fotos (URL1,URL2,URL3)">

<button class="btn add" onclick="saveCar()">Guardar / Agregar</button>

</div>

<script>

let editIndex = null;

let clicks = 0;

document.getElementById("secret").onclick = () => {
clicks++;
if(clicks >= 5){
let pass = prompt("Password:");
if(pass === "Khloe070304"){
document.getElementById("adminPanel").style.display="block";
}else{
alert("Incorrecto");
}
clicks = 0;
}
};

let cars = JSON.parse(localStorage.getItem("cars")) || [
{
name:"Ford Mustang GT",
price:23500,
year:2020,
imgs:[
"https://images.unsplash.com/photo-1503376780353-7e6692767b70",
"https://images.unsplash.com/photo-1525609004556-c46c7d6cf023"
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

function save(){
localStorage.setItem("cars", JSON.stringify(cars));
}

function render(){

let grid = document.getElementById("grid");
let search = document.getElementById("search").value.toLowerCase();

grid.innerHTML="";

cars.filter(c=>c.name.toLowerCase().includes(search))
.forEach((car,i)=>{

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

let imgs = car.imgs.map(img=>`<img src="${img}">`).join("");

document.getElementById("modalBody").innerHTML = `
<h2>${car.name}</h2>
<p class="price">$${car.price}</p>

<div class="slider">${imgs}</div>

<a class="btn whatsapp" href="https://wa.me/13050000000">WhatsApp</a>

<button class="btn edit" onclick="editCar(${i})">✏ Editar</button>
<button class="btn delete" onclick="deleteCar(${i})">🗑 Borrar</button>
`;

document.getElementById("modal").style.display="block";

}

function closeModal(){
document.getElementById("modal").style.display="none";
}

function saveCar(){

let name = document.getElementById("name").value;
let price = document.getElementById("price").value;
let year = document.getElementById("year").value;
let imgs = document.getElementById("imgs").value.split(",").map(x=>x.trim());

if(editIndex !== null){

cars[editIndex] = {name,price,year,imgs};
editIndex = null;

}else{

cars.push({name,price,year,imgs});

}

save();
render();
clearForm();

alert("Guardado");
}

function editCar(i){

let car = cars[i];
editIndex = i;

document.getElementById("name").value = car.name;
document.getElementById("price").value = car.price;
document.getElementById("year").value = car.year;
document.getElementById("imgs").value = car.imgs.join(",");

document.getElementById("adminPanel").style.display="block";
closeModal();
}

function deleteCar(i){

if(confirm("Borrar este carro?")){
cars.splice(i,1);
save();
render();
closeModal();
}
}

function clearForm(){
document.getElementById("name").value="";
document.getElementById("price").value="";
document.getElementById("year").value="";
document.getElementById("imgs").value="";
}

render();

</script>

</body>
</html>
