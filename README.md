
<html lang="pt-BR">

<head>

<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<title>Cronograma de Apresentações</title>

<script src="https://cdn.tailwindcss.com"></script>

<link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600&family=Playfair+Display:wght@600;700&display=swap" rel="stylesheet">

<style>

body{
background:#0f172a;
color:white;
font-family:'Inter',sans-serif;
}

h1{
font-family:'Playfair Display',serif;
}

.card{
background:#1e293b;
border:1px solid #334155;
}

</style>

</head>

<body class="p-8">

<div class="max-w-6xl mx-auto">

<!-- CABEÇALHO -->

<div class="flex flex-col items-center text-center mb-10">

<img
src="https://62ad35b797.nxcli.net/wp-content/uploads/2022/02/Logo600.png"
class="w-28 mb-4"
>

<h1 class="text-4xl md:text-5xl font-bold">
Cronograma de Apresentações
</h1>

<p class="text-indigo-400 text-lg mt-2">
Curso: Engenharia da Computação
</p>

<p class="text-gray-400">
Seminário Acadêmico 2026
</p>

</div>


<!-- CONTROLES -->

<div class="flex flex-col md:flex-row gap-4 mb-6">

<input
id="search"
placeholder="Pesquisar equipe ou tema..."
class="flex-1 p-3 rounded bg-slate-800 border border-slate-600"
>

<select id="filterDay" class="p-3 rounded bg-slate-800 border border-slate-600">

<option value="0">Todos</option>
<option value="1">Dia 1</option>
<option value="2">Dia 2</option>

</select>

<button onclick="openAddModal()" class="bg-indigo-600 px-5 py-3 rounded">
Adicionar Equipe
</button>

</div>

<div class="mb-4 text-gray-400">
Total de equipes: <span id="teamCount">0</span>
</div>


<!-- TABELA -->

<div class="card rounded-xl overflow-hidden">

<table class="w-full">

<thead class="bg-indigo-600/20">

<tr>

<th class="p-4 text-left">Equipe</th>
<th class="p-4 text-left">Tema</th>
<th class="p-4 text-center">Dia</th>
<th class="p-4 text-center">Integrantes</th>
<th class="p-4 text-center">Ações</th>

</tr>

</thead>

<tbody id="tableBody"></tbody>

</table>

</div>

</div>



<!-- MODAL DETALHES -->

<div id="detailModal" class="fixed inset-0 bg-black/60 hidden items-center justify-center">

<div class="bg-slate-800 p-6 rounded-xl w-96">

<h2 id="detailTeam" class="text-xl mb-3 font-semibold"></h2>

<p class="text-indigo-400 mb-2">Integrantes:</p>

<ul id="detailMembers" class="text-gray-300 mb-4"></ul>

<button onclick="closeDetail()" class="bg-indigo-600 px-4 py-2 rounded">
Fechar
</button>

</div>

</div>



<script>

let teams=[

{
id:1,
name:"Equipe 1",
topic:"Inteligência Artificial",
day:1,
members:[
"João Silva",
"Maria Souza",
"Pedro Santos"
]
},

{
id:2,
name:"Equipe 2",
topic:"Energias Renováveis",
day:1,
members:[
"Lucas Oliveira",
"Ana Pereira",
"Carlos Lima"
]
},

{
id:3,
name:"Equipe 3",
topic:"Cibersegurança",
day:1,
members:[
"Bruno Costa",
"Juliana Alves",
"Paulo Rocha"
]
},

{
id:4,
name:"Equipe 4",
topic:"Realidade Virtual",
day:1,
members:[
"Rafael Martins",
"Fernanda Gomes",
"Daniel Ribeiro"
]
},

{
id:5,
name:"Equipe 5",
topic:"Biotecnologia",
day:2,
members:[
"Patricia Carvalho",
"Marcos Ferreira",
"Renata Dias"
]
},

{
id:6,
name:"Equipe 6",
topic:"Internet das Coisas",
day:2,
members:[
"Thiago Barbosa",
"Larissa Nunes",
"Gustavo Teixeira"
]
},

{
id:7,
name:"Equipe 7",
topic:"Blockchain",
day:2,
members:[
"Felipe Andrade",
"Camila Batista",
"Diego Lopes"
]
},

{
id:8,
name:"Equipe 8",
topic:"Computação em Nuvem",
day:2,
members:[
"Eduardo Cardoso",
"Vanessa Freitas",
"Rodrigo Melo"
]
}

]


function render(){

const body=document.getElementById("tableBody")
body.innerHTML=""

const search=document.getElementById("search").value.toLowerCase()
const filterDay=Number(document.getElementById("filterDay").value)

const filtered=teams.filter(team=>

(team.name.toLowerCase().includes(search)
|| team.topic.toLowerCase().includes(search))

&& (filterDay===0 || team.day===filterDay)

)

document.getElementById("teamCount").innerText=filtered.length

filtered.forEach(team=>{

const row=document.createElement("tr")

row.className="border-t border-slate-700 hover:bg-slate-700"

row.innerHTML=`

<td class="p-4">${team.name}</td>

<td class="p-4">${team.topic}</td>

<td class="p-4 text-center">Dia ${team.day}</td>

<td class="p-4 text-center">
<button onclick="showDetail(${team.id})" class="text-indigo-400">
Ver nomes
</button>
</td>

<td class="p-4 text-center">

<button onclick="deleteTeam(${team.id})" class="text-red-400">
Excluir
</button>

</td>

`

body.appendChild(row)

})

}


function showDetail(id){

const team=teams.find(t=>t.id===id)

document.getElementById("detailTeam").innerText=team.name

const list=document.getElementById("detailMembers")

list.innerHTML=""

team.members.forEach(member=>{

const li=document.createElement("li")
li.innerText=member
list.appendChild(li)

})

document.getElementById("detailModal").classList.remove("hidden")
document.getElementById("detailModal").classList.add("flex")

}


function closeDetail(){

document.getElementById("detailModal").classList.add("hidden")

}


function deleteTeam(id){

teams=teams.filter(t=>t.id!==id)

render()

}


document.getElementById("search").addEventListener("input",render)
document.getElementById("filterDay").addEventListener("change",render)

render()

</script>

</body>
</html>
