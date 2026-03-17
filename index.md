<index.html>
<html lang="ka">
<head>

<meta charset="UTF-8">
<meta name="viewport" content="width=device-width,initial-scale=1">

<title>SKALP Burger</title>

<style>

body{
margin:0;
font-family:Arial;
background:#000;
color:white;
}

.header{
text-align:center;
padding:20px;
}

.logo{
width:130px;
filter:drop-shadow(0 0 10px #ff00cc);
}

.category{
padding:15px;
font-size:22px;
color:#00ff9c;
}

.menu{
padding-bottom:100px;
}

.card{
background:#111;
border-radius:20px;
margin:15px;
overflow:hidden;
box-shadow:0 0 10px #ff00cc44;
}

.card img{
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

.add{
background:#ff0066;
border:none;
color:white;
padding:10px 15px;
border-radius:10px;
}

.bottom{
position:fixed;
bottom:0;
left:0;
right:0;
background:#111;
display:flex;
justify-content:space-around;
padding:15px;
}

.bottom button{
background:none;
border:none;
color:white;
font-size:18px;
}

.cart{
display:none;
position:fixed;
inset:0;
background:#000;
padding:20px;
}

.order{
background:#00ff9c;
border:none;
padding:15px;
width:100%;
font-size:18px;
border-radius:10px;
}

</style>

</head>

<body>

<div class="header">
<img src="logo.png" class="logo">
<h2>SKALP MENU</h2>
</div>

<div class="menu" id="menu"></div>

<div class="bottom">

<button onclick="showMenu()">🍔 Menu</button>

<button onclick="openCart()">🛒 Cart</button>

<button onclick="location.href='https://maps.app.goo.gl/M6yWTgJy975hESnt6'">
📍 Location
</button>

</div>

<div class="cart" id="cart">

<h2>თქვენი შეკვეთა</h2>

<div id="cartItems"></div>

<button class="order" onclick="sendOrder()">
შეკვეთის გაგზავნა
</button>

</div>

<script>

const menu=[
{name:"SKALP ბოქსი",price:15,img:"https://images.unsplash.com/photo-1550547660-d9450f859349"},
{name:"პარმეზან ბოქსი",price:20,img:"https://images.unsplash.com/photo-1606755962773-d324e2d53a4c"},
{name:"ქათმის ბურგერი",price:10,img:"https://images.unsplash.com/photo-1568901346375-23c9450c58cd"},
{name:"კარტოფილი ფრი",price:5,img:"https://images.unsplash.com/photo-1585238342024-78d387f4a707"}
]

let cart=[]

function render(){

let html=""

menu.forEach((i,index)=>{

html+=`
<div class="card">

<img src="${i.img}">

<div class="info">

<span>${i.name} - ${i.price}₾</span>

<button class="add" onclick="add(${index})">+</button>

</div>

</div>
`

})

menu.innerHTML=html

}

function add(i){

cart.push(menu[i])

alert("დაემატა")

}

function openCart(){

let html=""

cart.forEach(i=>{
html+=`<div>${i.name} - ${i.price}₾</div>`
})

cartItems.innerHTML=html

document.getElementById("cart").style.display="block"

}

function sendOrder(){

let text="SKALP ORDER%0A"

cart.forEach(i=>{
text+=i.name+" "+i.price+"₾%0A"
})

window.open("https://wa.me/995555123456?text="+text)

}

render()

</script>

</body>
</html>
