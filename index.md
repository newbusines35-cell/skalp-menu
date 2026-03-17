<index.html>
<!DOCTYPE html>
<html lang="ka">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>SKALP Burger • QR Menu</title>

<style>
:root{
--neon:#ff00cc;
--neon2:#00ff9c;
--bg:#050505;
--card:#111;
}

*{box-sizing:border-box}

body{
margin:0;
font-family:Arial,Helvetica,sans-serif;
background:var(--bg);
color:white;
}

.header{
text-align:center;
padding:25px 15px 10px;
}

.logo{
width:150px;
animation:glow 2s infinite alternate;
}

@keyframes glow{
from{filter:drop-shadow(0 0 5px var(--neon));}
to{filter:drop-shadow(0 0 25px var(--neon));}
}

.title{
font-size:34px;
color:var(--neon);
text-shadow:0 0 20px var(--neon);
margin-top:10px;
}

.table{
text-align:center;
margin:10px;
font-size:18px;
color:var(--neon2);
}

.menu{
padding:10px 15px 90px;
}

.category{
font-size:24px;
margin:25px 0 10px;
color:var(--neon2);
}

.item{
background:var(--card);
border-radius:15px;
overflow:hidden;
margin-bottom:18px;
box-shadow:0 0 12px rgba(255,0,200,0.4);
cursor:pointer;
}

.item img{
width:100%;
height:210px;
object-fit:cover;
}

.info{
display:flex;
justify-content:space-between;
padding:15px;
font-size:18px;
}

.price{
color:var(--neon2);
font-weight:bold;
}

.cart-btn{
position:fixed;
bottom:20px;
right:20px;
background:var(--neon);
color:white;
border:none;
padding:16px 20px;
border-radius:30px;
font-size:18px;
box-shadow:0 0 15px var(--neon);
cursor:pointer;
}

.modal{
display:none;
position:fixed;
inset:0;
background:rgba(0,0,0,0.85);
align-items:center;
justify-content:center;
z-index:10;
}

.modal-content{
background:#111;
width:90%;
max-width:420px;
border-radius:20px;
overflow:hidden;
text-align:center;
box-shadow:0 0 20px var(--neon);
}

.modal img{
width:100%;
height:260px;
object-fit:cover;
}

.modal h2{margin:10px}

.modal p{padding:0 15px}

.add{
background:var(--neon);
border:none;
padding:12px 20px;
margin:15px;
color:white;
border-radius:10px;
font-size:18px;
cursor:pointer;
}

.cart{
display:none;
position:fixed;
inset:0;
background:#000;
z-index:20;
overflow:auto;
padding:20px;
}

.cart h2{text-align:center}

.cart-item{
display:flex;
justify-content:space-between;
margin:10px 0;
}

.order{
background:var(--neon2);
color:black;
border:none;
width:100%;
padding:15px;
font-size:18px;
border-radius:10px;
margin-top:20px;
cursor:pointer;
}

.map{
padding:20px;
text-align:center;
}

.map a{
color:var(--neon2);
font-size:18px;
text-decoration:none;
}

</style>
</head>

<body>

<div class="header">
<img src="logo.png" class="logo">
<div class="title">SKALP MENU</div>
<div class="table" id="tableInfo"></div>
</div>

<div class="menu" id="menu"></div>

<button class="cart-btn" onclick="openCart()">🛒 Cart</button>

<!-- PRODUCT MODAL -->
<div class="modal" id="modal">
<div class="modal-content">
<img id="mImg">
<h2 id="mName"></h2>
<p id="mDesc"></p>
<div class="price" id="mPrice"></div>
<button class="add" onclick="addToCart()">კალათაში დამატება</button>
<button class="add" onclick="closeModal()">დახურვა</button>
</div>
</div>

<!-- CART -->
<div class="cart" id="cart">
<h2>თქვენი შეკვეთა</h2>
<div id="cartItems"></div>
<button class="order" onclick="sendOrder()">შეკვეთის გაგზავნა</button>
<button class="order" onclick="closeCart()">დახურვა</button>
</div>

<div class="map">
<a href="https://maps.app.goo.gl/M6yWTgJy975hESnt6?g_st=ic" target="_blank">
📍 გახსენი Google Maps ლოკაცია
</a>
</div>

<script>

const menuData=[

{cat:"🍗 ბოქსები",name:"SKALP ბოქსი",price:15,img:"https://images.unsplash.com/photo-1550547660-d9450f859349",desc:"ქათმის ბოქსი + ფრი + სოუსი"},
{cat:"🍗 ბოქსები",name:"SKALP პარმეზან ბოქსი",price:20,img:"https://images.unsplash.com/photo-1606755962773-d324e2d53a4c",desc:"ქათმის ბოქსი პარმეზანის სოუსით"},
{cat:"🍗 ბოქსები",name:"SKALP ქნიქენ ჩიქენ ბოქსი",price:22,img:"https://images.unsplash.com/photo-1600891964599-f61ba0e24092",desc:"ქათმის დიდი პორცია"},
{cat:"🍗 ბოქსები",name:"SKALP სპაისი ბოქსი",price:18,img:"https://images.unsplash.com/photo-1612392062631-94dd858c7d69",desc:"ცხარე ქათმის ბოქსი"},
{cat:"🍗 ბოქსები",name:"SKALP XL ბოქსი",price:20,img:"https://images.unsplash.com/photo-1606755962773-d324e2d53a4c",desc:"დიდი ზომის ბოქსი"},

{cat:"🌮 სხვა",name:"მექსიკური ტაკო",price:5,img:"https://images.unsplash.com/photo-1615870216519-2f9fa575fa5c",desc:"ტაკო ქათმით"},
{cat:"🌮 სხვა",name:"კარტოფილი ფრი",price:5,img:"https://images.unsplash.com/photo-1585238342024-78d387f4a707",desc:"კრისტალური ფრი"},
{cat:"🌮 სხვა",name:"ქათმის ბურგერი",price:10,img:"https://images.unsplash.com/photo-1568901346375-23c9450c58cd",desc:"ქათმის ბურგერი სპეციალური სოუსით"},

{cat:"🍗 ფრთები",name:"ცხელი ქათმის ფრთები 1000გ",price:7,img:"https://images.unsplash.com/photo-1608039829572-78524f79c4c7",desc:"ცხარე ფრთები"}

]

let cart=[]
let current=null

function renderMenu(){
let html=""
let last=""
menuData.forEach((i,index)=>{

if(i.cat!==last){
html+=`<div class="category">${i.cat}</div>`
last=i.cat
}

html+=`
<div class="item" onclick="openModal(${index})">
<img src="${i.img}">
<div class="info">
<span>${i.name}</span>
<span class="price">${i.price} ₾</span>
</div>
</div>`
})
document.getElementById("menu").innerHTML=html
}

function openModal(i){
current=i
let item=menuData[i]
mImg.src=item.img
mName.innerText=item.name
mDesc.innerText=item.desc
mPrice.innerText=item.price+" ₾"
modal.style.display="flex"
}

function closeModal(){modal.style.display="none"}

function addToCart(){
cart.push(menuData[current])
closeModal()
alert("დაემატა კალათაში")
}

function openCart(){
let html=""
cart.forEach(i=>{
html+=`<div class="cart-item"><span>${i.name}</span><span>${i.price} ₾</span></div>`
})
cartItems.innerHTML=html
cart.style.display="block"
}

function closeCart(){cart.style.display="none"}

function sendOrder(){

let table=new URLSearchParams(location.search).get("table")||"?"
let text="SKALP შეკვეთა მაგიდა "+table+"%0A"

cart.forEach(i=>{
text+=i.name+" - "+i.price+"₾%0A"
})

window.open("https://wa.me/995555123456?text="+text)

}

function detectTable(){
let table=new URLSearchParams(location.search).get("table")
if(table){
tableInfo.innerText="მაგიდა № "+table
}
}

renderMenu()
detectTable()

</script>

</body>
</html>
