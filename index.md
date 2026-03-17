<index.html>
<html lang="ka">
<head>

<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<title>SKALP Burger</title>

<style>

body{
margin:0;
font-family:Arial;
background:#050505;
color:white;
}

.header{
text-align:center;
padding:30px;
}

.logo{
width:140px;
animation: neon 1.5s infinite alternate;
}

@keyframes neon{
0%{filter:drop-shadow(0 0 5px #ff00cc);}
100%{filter:drop-shadow(0 0 25px #ff00cc);}
}

.title{
font-size:40px;
color:#ff00cc;
text-shadow:0 0 15px #ff00cc;
}

.slider{
display:flex;
overflow-x:auto;
gap:20px;
padding:20px;
}

.slide{
min-width:240px;
background:#111;
border-radius:20px;
transform:perspective(800px) rotateY(-10deg);
transition:0.3s;
box-shadow:0 0 20px #ff00cc;
}

.slide:hover{
transform:scale(1.05) rotateY(0deg);
}

.slide img{
width:100%;
height:160px;
object-fit:cover;
border-radius:20px 20px 0 0;
}

.slide p{
padding:10px;
}

.menu{
padding:20px;
}

.item{
background:#111;
border-radius:15px;
overflow:hidden;
margin-bottom:20px;
}

.item img{
width:100%;
height:200px;
object-fit:cover;
}

.info{
display:flex;
justify-content:space-between;
padding:15px;
font-size:18px;
}

.price{
color:#00ff9c;
}

button{
background:#ff0066;
border:none;
color:white;
padding:10px 15px;
border-radius:8px;
cursor:pointer;
}

.cart{
position:fixed;
bottom:20px;
right:20px;
background:#ff0066;
padding:15px;
border-radius:50px;
box-shadow:0 0 15px #ff0066;
}

.admin{
background:#111;
padding:20px;
margin:20px;
border-radius:15px;
}

input{
padding:10px;
margin:5px;
border-radius:5px;
border:none;
}

.map{
padding:20px;
}

iframe{
width:100%;
height:250px;
border-radius:15px;
border:none;
}

</style>

</head>

<body>

<div class="header">

<img src="logo.png" class="logo">

<div class="title">SKALP BURGER</div>

</div>


<!-- 3D SLIDER -->

<div class="slider">

<div class="slide">
<img src="https://images.unsplash.com/photo-1568901346375-23c9450c58cd">
<p>ქათმის ბურგერი</p>
</div>

<div class="slide">
<img src="https://images.unsplash.com/photo-1550547660-d9450f859349">
<p>SKALP ბოქსი</p>
</div>

<div class="slide">
<img src="https://images.unsplash.com/photo-1606755962773-d324e2d53a4c">
<p>Chicken Box</p>
</div>

</div>


<!-- MENU -->

<div class="menu" id="menu"></div>


<!-- CART -->

<div class="cart" onclick="showCart()">
🛒 Cart
</div>


<!-- ADMIN PANEL -->

<div class="admin">

<h3>მენიუს მართვა</h3>

<input id="name" placeholder="პროდუქტი">
<input id="price" placeholder="ფასი">

<button onclick="addItem()">დამატება</button>

</div>


<!-- MAP -->

<div class="map">

<iframe
src="https://maps.google.com/maps?q=tbilisi&t=&z=15&ie=UTF8&iwloc=&output=embed">
</iframe>

</div>


<script>

let menu = JSON.parse(localStorage.getItem("menu")) || [

{name:"ქათმის ბურგერი",price:"10₾",img:"https://images.unsplash.com/photo-1568901346375-23c9450c58cd"},
{name:"SKALP ბოქსი",price:"15₾",img:"https://images.unsplash.com/photo-1550547660-d9450f859349"},
{name:"კარტოფილი ფრი",price:"5₾",img:"https://images.unsplash.com/photo-1585238342024-78d387f4a707"}

]

let cart=[]

function render(){

let html=""

menu.forEach((i,index)=>{

html+=`
<div class="item">

<img src="${i.img}">

<div class="info">

<span>${i.name}</span>

<span class="price">${i.price}</span>

<button onclick="addCart(${index})">Add</button>

</div>

</div>
`

})

document.getElementById("menu").innerHTML=html

}

function addCart(i){

cart.push(menu[i])

alert("დაემატა კალათაში")

}

function showCart(){

let txt="თქვენი შეკვეთა:\n"

cart.forEach(i=>{

txt+=i.name+" "+i.price+"\n"

})

alert(txt)

}

function addItem(){

let name=document.getElementById("name").value
let price=document.getElementById("price").value

menu.push({name,price,img:"https://images.unsplash.com/photo-1568901346375-23c9450c58cd"})

localStorage.setItem("menu",JSON.stringify(menu))

render()

}

render()

</script>

</body>
</html>
