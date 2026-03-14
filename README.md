<!DOCTYPE html>
<html lang="pt-BR">
<head>

<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<title>Cronograma de Apresentações</title>

<script src="https://cdn.tailwindcss.com"></script>

<style>
body{
background:#0f172a;
color:white;
font-family:Arial, Helvetica, sans-serif;
}
</style>

</head>

<body class="p-8">

<div class="max-w-5xl mx-auto">

<h1 class="text-3xl font-bold mb-2">
Cronograma de Apresentações
</h1>

<p class="text-gray-400 mb-6">
Seminário Acadêmico 2026
</p>

<div class="flex gap-3 mb-6">

<input
id="search"
placeholder="Pesquisar equipe..."
class="flex-1 p-2 rounded bg-gray-800 border border-gray-600"
>

<select id="filterDay" class="p-2 rounded bg-gray-800">

<option value="0">Todos</option>
<option value="1">Dia 1</option>
<option value="2">Dia 2</option>

</select>

<button
onclick="openAddModal()"
class="bg-indigo-600 px-4 py-2 rounded"
>

Adicionar Equipe

</button>

</div>

<div class="mb-3 text-gray-400">
Total: <span id="teamCount">0</span>
</div>


<table class="w-full bg-slate-800 rounded overflow-hidden">

<thead class="bg-indigo-600">

<tr>

<th class="p-3 text-left">Equipe</th>
<th class="p-3 text-left">Tema</th>
<th class="p-3 text-center">Dia</th>
<th class="p-3 text-center">Ações</th>

</tr>

</thead>

<tbody id="tableBody"></tbody>

</table>

</div>


<!-- MODAL -->

<div
id="formModal"
class="fixed inset-0 bg-black/60 hidden items-center justify-center"
>

<div class="bg-slate-800 p-6 rounded w-96">

<h2 class="text-xl mb-4">Equipe</h2>

<input id="teamName" placeholder="Nome" class="w-full mb-2 p-2 bg-slate-700 rounded">

<input id="teamTopic" placeholder="Tema" class="w-full mb-2 p-2 bg-slate-700 rounded">

<select id="teamDay" class="w-full mb-4 p-2 bg-slate-700 rounded">

<option value="1">Dia 1</option>
<option value="2">Dia 2</option>

</select>

<div class="flex justify-end gap-2">

<button onclick="closeForm()" class="bg-gray-600 px-3 py-1 rounded">
Cancelar
</button>

<button onclick="saveTeam()" class="bg-indigo-600 px-3 py-1 rounded">
Salvar
</button>

</div>

</div>

</div>


<script>

let teams = [
{ id:1,name:"Equipe 1",topic:"Inteligência Artificial",day:1 },
{ id:2,name:"Equipe 2",topic:"Energias Renováveis",day:1 },
{ id:3,name:"Equipe 3",topic:"Cibersegurança",day:1 },
{ id:4,name:"Equipe 4",topic:"Realidade Virtual",day:1 },
{ id:5,name:"Equipe 5",topic:"Biotecnologia",day:2 },
{ id:6,name:"Equipe 6",topic:"Internet das Coisas",day:2 },
{ id:7,name:"Equipe 7",topic:"Blockchain",day:2 },
{ id:8,name:"Equipe 8",topic:"Computação em Nuvem",day:2 }
]

let editId = null


function render(){

const body = document.getElementById("tableBody")

body.innerHTML = ""

const search = document.getElementById("search").value.toLowerCase()

const filterDay = Number(document.getElementById("filterDay").value)

const filtered = teams.filter(team =>

(team.name.toLowerCase().includes(search) ||
team.topic.toLowerCase().includes(search))

&& (filterDay === 0 || team.day === filterDay)

)

document.getElementById("teamCount").innerText = filtered.length

filtered.forEach(team => {

const row = document.createElement("tr")

row.className = "border-t border-gray-700 hover:bg-slate-700"

row.innerHTML = `

<td class="p-3">${team.name}</td>

<td class="p-3">${team.topic}</td>

<td class="p-3 text-center">Dia ${team.day}</td>

<td class="p-3 text-center">

<button onclick="editTeam(${team.id})" class="text-yellow-400 mr-2">
Editar
</button>

<button onclick="deleteTeam(${team.id})" class="text-red-400">
Excluir
</button>

</td>

`

body.appendChild(row)

})

}


function openAddModal(){

editId = null

document.getElementById("teamName").value = ""
document.getElementById("teamTopic").value = ""

document.getElementById("formModal").classList.remove("hidden")
document.getElementById("formModal").classList.add("flex")

}


function closeForm(){

document.getElementById("formModal").classList.add("hidden")

}


function saveTeam(){

const name = document.getElementById("teamName").value
const topic = document.getElementById("teamTopic").value
const day = Number(document.getElementById("teamDay").value)

if(editId){

const team = teams.find(t => t.id === editId)

team.name = name
team.topic = topic
team.day = day

}else{

teams.push({

id: Date.now(),
name,
topic,
day

})

}

closeForm()

render()

}


function editTeam(id){

const team = teams.find(t => t.id === id)

editId = id

document.getElementById("teamName").value = team.name
document.getElementById("teamTopic").value = team.topic
document.getElementById("teamDay").value = team.day

document.getElementById("formModal").classList.remove("hidden")
document.getElementById("formModal").classList.add("flex")

}


function deleteTeam(id){

teams = teams.filter(t => t.id !== id)

render()

}


document.getElementById("search").addEventListener("input", render)
document.getElementById("filterDay").addEventListener("change", render)

render()

</script>

</body>
</html>
