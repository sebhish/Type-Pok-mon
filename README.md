<!DOCTYPE html>
<html lang="fr">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Types Pokémon – Analyse complète</title>

<style>
body{
    font-family: Arial, sans-serif;
    background:#eef2f3;
    margin:0;
    padding:20px;
    text-align:center;
    transition:.3s;
}
body.dark{
    background:#1c1c1c;
    color:#f4f4f4;
}
h1{color:#e3350d}
body.dark h1{color:#ff6b6b}

#darkToggle{
    padding:10px 20px;
    border:none;
    background:#444;
    color:white;
    border-radius:8px;
    cursor:pointer;
    margin-bottom:20px;
}
#darkToggle:hover{background:#666}

.type-grid{
    display:grid;
    grid-template-columns:repeat(6,1fr);
    gap:8px;
    max-width:520px;
    margin:10px auto;
}
.type-btn{
    padding:10px;
    border-radius:8px;
    cursor:pointer;
    font-weight:bold;
    color:white;
    border:3px solid transparent;
    transition:.2s;
}
.type-btn.selected{
    border-color:black;
    transform:scale(1.05);
}
body.dark .type-btn.selected{
    border-color:white;
}

.result{
    margin-top:20px;
    padding:20px;
    background:white;
    border-radius:10px;
    box-shadow:0 0 10px #ccc;
    max-width:600px;
    margin-inline:auto;
}
body.dark .result{
    background:#2a2a2a;
    box-shadow:0 0 10px #000;
}

.type-tag{
    display:inline-block;
    padding:6px 12px;
    border-radius:8px;
    margin:4px;
    font-weight:bold;
    color:white;
}

.cat-title{
    font-weight:bold;
    margin-top:18px;
    font-size:18px;
}
</style>
</head>

<body>

<h1>Analyse des Types Pokémon</h1>
<button id="darkToggle">🌙 Mode sombre</button>

<h2>Type 1 (clique pour sélectionner / désélectionner)</h2>
<div id="grid1" class="type-grid"></div>

<h2>Type 2 (optionnel)</h2>
<div id="grid2" class="type-grid"></div>

<div id="result" class="result"></div>

<script>
const typeColors={
Normal:"#A8A77A",Feu:"#EE8130",Eau:"#6390F0",Plante:"#7AC74C",
Électrik:"#F7D02C",Glace:"#96D9D6",Combat:"#C22E28",
Poison:"#A33EA1",Sol:"#E2BF65",Vol:"#A98FF3",
Psy:"#F95587",Insecte:"#A6B91A",Roche:"#B6A136",
Spectre:"#735797",Dragon:"#6F35FC",Ténèbres:"#705746",
Acier:"#B7B7CE",Fée:"#D685AD"
};

const chart={
Normal:{Combat:2,Spectre:0},
Feu:{Eau:2,Sol:2,Roche:2,Plante:.5,Glace:.5,Insecte:.5,Acier:.5},
Eau:{Électrik:2,Plante:2,Feu:.5,Sol:.5,Roche:.5},
Plante:{Feu:2,Glace:2,Poison:2,Vol:2,Insecte:2,Eau:.5,Sol:.5,Roche:.5},
Électrik:{Sol:2,Électrik:.5,Vol:.5,Acier:.5},
Glace:{Feu:2,Combat:2,Roche:2,Acier:2,Glace:.5},
Combat:{Vol:2,Psy:2,Fée:2,Insecte:.5,Roche:.5,Ténèbres:.5},
Psy:{Insecte:2,Spectre:2,Ténèbres:2,Combat:.5,Psy:.5},
Roche:{Eau:2,Plante:2,Combat:2,Sol:2,Acier:2,Normal:.5,Feu:.5,Poison:.5},
Sol:{Eau:2,Plante:2,Glace:2,Poison:.5,Roche:.5,Électrik:0},
Vol:{Électrik:2,Glace:2,Roche:2,Plante:.5,Combat:.5,Insecte:.5,Sol:0},
Ténèbres:{Combat:2,Insecte:2,Fée:2,Ténèbres:.5,Spectre:.5},
Fée:{Poison:2,Acier:2,Combat:.5,Insecte:.5,Ténèbres:.5},
Poison:{Sol:2,Psy:2,Plante:.5,Combat:.5,Poison:.5,Fée:.5},
Insecte:{Feu:2,Vol:2,Roche:2,Plante:.5,Combat:.5,Sol:.5},
Acier:{Feu:2,Combat:2,Sol:2,Normal:.5,Plante:.5,Glace:.5,Vol:.5,Psy:.5,Insecte:.5,Roche:.5,Dragon:.5,Acier:.5,Fée:.5,Poison:0},
Dragon:{Glace:2,Dragon:2,Fée:2,Feu:.5,Eau:.5,Plante:.5,Électrik:.5},
Spectre:{Spectre:2,Ténèbres:2,Poison:.5,Insecte:.5,Normal:0}
};

const types=Object.keys(chart);
let type1=null, type2=null;

function createGrid(id,isFirst){
    const grid=document.getElementById(id);
    types.forEach(t=>{
        const btn=document.createElement("div");
        btn.className="type-btn";
        btn.style.background=typeColors[t];
        btn.innerText=t;

        btn.onclick=()=>{
            if(isFirst){
                if(type1===t){
                    type1=null;
                    btn.classList.remove("selected");
                }else{
                    type1=t;
                    [...grid.children].forEach(b=>b.classList.remove("selected"));
                    btn.classList.add("selected");
                }
            }else{
                if(type2===t){
                    type2=null;
                    btn.classList.remove("selected");
                }else{
                    type2=t;
                    [...grid.children].forEach(b=>b.classList.remove("selected"));
                    btn.classList.add("selected");
                }
            }
            calculate();
        };
        grid.appendChild(btn);
    });
}

createGrid("grid1",true);
createGrid("grid2",false);

function tag(t){
    return `<span class="type-tag" style="background:${typeColors[t]}">${t}</span>`;
}

function calculate(){
    if(!type1){
        document.getElementById("result").innerHTML="";
        return;
    }

    let mult={};
    types.forEach(t=>mult[t]=1);

    for(let a in chart[type1]) mult[a]*=chart[type1][a];
    if(type2) for(let a in chart[type2]) mult[a]*=chart[type2][a];

    let x4=[],x2=[],x05=[],x0=[];
    for(let a in mult){
        if(mult[a]===4)x4.push(a);
        else if(mult[a]===2)x2.push(a);
        else if(mult[a]===.5)x05.push(a);
        else if(mult[a]===0)x0.push(a);
    }

    document.getElementById("result").innerHTML=`
    <h2>${tag(type1)} ${type2?"+ "+tag(type2):""}</h2>

    <div class="cat-title">🔥 Hyper efficace (x4)</div>
    ${x4.length?x4.map(tag).join(""):"Aucun"}

    <div class="cat-title">⚔️ Super efficace (x2)</div>
    ${x2.length?x2.map(tag).join(""):"Aucun"}

    <div class="cat-title">🛡️ Résiste (x0.5)</div>
    ${x05.length?x05.map(tag).join(""):"Aucun"}

    <div class="cat-title">❌ Immunisé (x0)</div>
    ${x0.length?x0.map(tag).join(""):"Aucun"}
    `;
}

/* MODE SOMBRE */
const btn=document.getElementById("darkToggle");
let dark=localStorage.getItem("darkmode")==="true";
function apply(){
    document.body.classList.toggle("dark",dark);
    btn.innerText=dark?"☀️ Mode clair":"🌙 Mode sombre";
}
apply();
btn.onclick=()=>{
    dark=!dark;
    localStorage.setItem("darkmode",dark);
    apply();
};
</script>

</body>
</html>
