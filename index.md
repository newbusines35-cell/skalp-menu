<index.html>
<html>
<head>
<meta charset="UTF-8">
<title>SKALP Admin</title>
<style>

body{
font-family:Arial;
background:#111;
color:white;
padding:30px;
}

input,button{
padding:10px;
margin:5px;
}

</style>
</head>

<body>

<h2>SKALP Admin Panel</h2>

<input id="name" placeholder="პროდუქტი">
<input id="price" placeholder="ფასი">
<input id="img" placeholder="სურათის ლინკი">

<button onclick="add()">დამატება</button>

<div id="list"></div>

<script>

let menu=JSON.parse(localStorage.getItem("menu"))||[]

function render(){

let html=""

menu.forEach((i,index)=>{

html+=`
<div>
${i.name} - ${i.price} ₾
<button onclick="del(${index})">წაშლა</button>
</div>
`

})

document.getElementById("list").innerHTML=html

}

function add(){

menu.push({
name:name.value,
price:price.value,
img:img.value
})

localStorage.setItem("menu",JSON.stringify(menu))
render()

}

function del(i){

menu.splice(i,1)

localStorage.setItem("menu",JSON.stringify(menu))

render()

}

render()

</script>

</body>
</html>
