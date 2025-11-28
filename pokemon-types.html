<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Types Pokémon – Analyse complète</title>

    <style>
        body {
            font-family: Arial, sans-serif;
            background: #eef2f3;
            margin: 0;
            padding: 20px;
            text-align: center;
            transition: 0.3s;
        }

        /* MODE SOMBRE */
        body.dark {
            background: #1c1c1c;
            color: #f4f4f4;
        }

        h1 { color: #e3350d; }
        body.dark h1 { color: #ff6b6b; }

        #darkToggle {
            padding: 10px 20px;
            border: none;
            background: #444;
            color: white;
            border-radius: 8px;
            cursor: pointer;
            margin-bottom: 20px;
        }
        #darkToggle:hover { background: #666; }

        /* TABLEAU DES TYPES */
        .type-grid {
            display: grid;
            grid-template-columns: repeat(6, 1fr);
            gap: 8px;
            max-width: 500px;
            margin: 10px auto;
        }

        .type-btn {
            padding: 10px;
            border-radius: 8px;
            cursor: pointer;
            font-weight: bold;
            color: white;
            border: 2px solid transparent;
            transition: 0.2s;
        }

        .type-btn.selected {
            border: 3px solid black;
            transform: scale(1.05);
        }

        body.dark .type-btn.selected {
            border: 3px solid white;
        }

        /* RESULTATS */
        .result {
            margin-top: 20px;
            padding: 20px;
            background: white;
            border-radius: 10px;
            box-shadow: 0 0 10px #ccc;
            max-width: 600px;
            margin-left: auto;
            margin-right: auto;
        }

        body.dark .result {
            background: #2a2a2a;
            box-shadow: 0 0 10px #000;
        }

        .type-tag {
            display: inline-block;
            padding: 6px 12px;
            border-radius: 8px;
            margin: 4px;
            font-weight: bold;
            color: white;
        }

        .cat-title { 
            font-weight: bold; 
            margin-top: 20px; 
            font-size: 18px;
        }
    </style>
</head>

<body>

<h1>Analyse des Types Pokémon</h1>

<button id="darkToggle">🌙 Mode sombre</button>

<h2>Sélectionne ton premier type</h2>
<div id="typeGrid1" class="type-grid"></div>

<h2>Sélectionne ton second type (optionnel)</h2>
<div id="typeGrid2" class="type-grid"></div>

<div id="result" class="result"></div>

<script>
/* -----------------------------------------
   COULEURS DE CHAQUE TYPE
----------------------------------------- */
const typeColors = {
    Normal: "#A8A77A",
    Feu: "#EE8130",
    Eau: "#6390F0",
    Plante: "#7AC74C",
    Électrik: "#F7D02C",
    Glace: "#96D9D6",
    Combat: "#C22E28",
    Poison: "#A33EA1",
    Sol: "#E2BF65",
    Vol: "#A98FF3",
    Psy: "#F95587",
    Insecte: "#A6B91A",
    Roche: "#B6A136",
    Spectre: "#735797",
    Dragon: "#6F35FC",
    Ténèbres: "#705746",
    Acier: "#B7B7CE",
    Fée: "#D685AD"
};

/* -----------------------------------------
   TABLE DES MULTIPLICATEURS
----------------------------------------- */
const chart = {
    Normal:     { Combat:2, Spectre:0 },
    Feu:        { Eau:2, Sol:2, Roche:2, Plante:0.5, Glace:0.5, Insecte:0.5, Acier:0.5 },
    Eau:        { Électrik:2, Plante:2, Feu:0.5, Sol:0.5, Roche:0.5 },
    Plante:     { Feu:2, Glace:2, Poison:2, Vol:2, Insecte:2, Eau:0.5, Sol:0.5, Roche:0.5 },
    Électrik:   { Sol:2, Électrik:0.5, Vol:0.5, Acier:0.5 },
    Glace:      { Feu:2, Combat:2, Roche:2, Acier:2, Glace:0.5 },
    Combat:     { Vol:2, Psy:2, Fée:2, Insecte:0.5, Roche:0.5, Ténèbres:0.5 },
    Psy:        { Insecte:2, Spectre:2, Ténèbres:2, Combat:0.5, Psy:0.5 },
    Roche:      { Eau:2, Plante:2, Combat:2, Sol:2, Acier:2, Normal:0.5, Feu:0.5, Poison:0.5 },
    Sol:        { Eau:2, Plante:2, Glace:2, Poison:0.5, Roche:0.5, Électrik:0 },
    Vol:        { Électrik:2, Glace:2, Roche:2, Plante:0.5, Combat:0.5, Insecte:0.5, Sol:0 },
    Ténèbres:   { Combat:2, Insecte:2, Fée:2, Ténèbres:0.5, Spectre:0.5 },
    Fée:        { Poison:2, Acier:2, Combat:0.5, Insecte:0.5, Ténèbres:0.5 },
    Poison:     { Sol:2, Psy:2, Plante:0.5, Combat:0.5, Poison:0.5, Fée:0.5 },
    Insecte:    { Feu:2, Vol:2, Roche:2, Plante:0.5, Combat:0.5, Sol:0.5 },
    Acier:      { Feu:2, Combat:2, Sol:2, Normal:0.5, Plante:0.5, Glace:0.5, Vol:0.5, Psy:0.5, Insecte:0.5, Roche:0.5, Dragon:0.5, Acier:0.5, Fée:0.5, Poison:0 },
    Dragon:     { Glace:2, Dragon:2, Fée:2, Feu:0.5, Eau:0.5, Plante:0.5, Électrik:0.5 },
    Spectre:    { Spectre:2, Ténèbres:2, Poison:0.5, Insecte:0.5, Normal:0 }
};

const types = Object.keys(chart);

let selected1 = null;
let selected2 = null;

/* -----------------------------------------
   CRÉATION DES TABLEAUX CLIQUABLES
----------------------------------------- */
function createGrid(id, isFirst) {
    const grid = document.getElementById(id);

    types.forEach(type => {
        const btn = document.createElement("div");
        btn.className = "type-btn";
        btn.style.background = typeColors[type];
        btn.innerText = type;

        btn.onclick = () => {
            if (isFirst) {
                selected1 = type;
                [...grid.children].forEach(b => b.classList.remove("selected"));
                btn.classList.add("selected");
            } else {
                selected2 = type;
                [...grid.children].forEach(b => b.classList.remove("selected"));
                btn.classList.add("selected");
            }
            calculate();
        };

        grid.appendChild(btn);
    });
}

createGrid("typeGrid1", true);
createGrid("typeGrid2", false);

/* -----------------------------------------
   TAG COULEUR
----------------------------------------- */
function coloredTag(type) {
    return `<span class="type-tag" style="background:${typeColors[type]};">${type}</span>`;
}

/* -----------------------------------------
   CALCUL
----------------------------------------- */
function calculate() {
    if (!selected1) {
        document.getElementById("result").innerHTML = "";
        return;
    }

    let multipliers = {};
    types.forEach(t => multipliers[t] = 1);

    for (let atk in chart[selected1])
        multipliers[atk] *= chart[selected1][atk];

    if (selected2) {
        for (let atk in chart[selected2])
            multipliers[atk] *= chart[selected2][atk];
    }

    let x4=[], x2=[], x05=[], x0=[];
    for (let atk in multipliers) {
        if (multipliers[atk] === 4) x4.push(atk);
        else if (multipliers[atk] === 2) x2.push(atk);
        else if (multipliers[atk] === 0.5) x05.push(atk);
        else if (multipliers[atk] === 0) x0.push(atk);
    }

    document.getElementById("result").innerHTML = `
        <h2>Résultat pour : ${coloredTag(selected1)} ${selected2 ? "+" + coloredTag(selected2) : ""}</h2>

        <div class="cat-title">🔥 Hyper efficace (x4)</div>
        ${x4.length ? x4.map(coloredTag).join("") : "Aucun"}

        <div class="cat-title">⚔️ Super efficace (x2)</div>
        ${x2.length ? x2.map(coloredTag).join("") : "Aucun"}

        <div class="cat-title">🛡️ Résiste (x0.5)</div>
        ${x05.length ? x05.map(coloredTag).join("") : "Aucun"}

        <div class="cat-title">❌ Immunisé (x0)</div>
        ${x0.length ? x0.map(coloredTag).join("") : "Aucun"}
    `;
}

/* -----------------------------------------
   MODE SOMBRE
----------------------------------------- */
const btn = document.getElementById("darkToggle");

function applyDarkMode(state) {
    if (state) {
        document.body.classList.add("dark");
        btn.innerText = "☀️ Mode clair";
    } else {
        document.body.classList.remove("dark");
        btn.innerText = "🌙 Mode sombre";
    }
}

let saved = localStorage.getItem("darkmode") === "true";
applyDarkMode(saved);

btn.onclick = () => {
    saved = !saved;
    localStorage.setItem("darkmode", saved);
    applyDarkMode(saved);
};
</script>

</body>
</html>
