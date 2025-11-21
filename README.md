<html lang="fr">
<head>
<meta charset="UTF-8">
<title>🎄 Calendrier de l'Avent 🎄</title>
<style>
  body { 
    font-family: Arial, sans-serif; 
    background: #064E3B; 
    color: #fff; 
    text-align: center; 
    margin:0; 
    padding:20px; 
    overflow-x: hidden;
  }

  /* Titre animé */
  h1 {
    margin-top: 0;
    font-size: 50px;
    color: #FFD700;
    text-shadow: 3px 3px 6px #000;
    animation: blink 1.2s infinite alternate, float 3s ease-in-out infinite;
  }

  @keyframes blink {
    0% { opacity: 0.6; }
    100% { opacity: 1; }
  }
  @keyframes float {
    0% { transform: translateY(0px); }
    50% { transform: translateY(-8px); }
    100% { transform: translateY(0px); }
  }

  .calendar {
    display: grid;
    grid-template-columns: repeat(6, 150px);
    gap: 15px;
    justify-content: center;
    margin: 20px auto;
    max-width: 960px;
  }

  .day {
    background: #e63946;
    width:150px;
    height:150px;
    cursor: pointer;
    font-weight: bold;
    color: #fff;
    text-shadow: 1px 1px 2px #000;
    box-shadow: 0 6px 12px rgba(0,0,0,0.5);
    display:flex;
    align-items:center;
    justify-content:center;
    font-size:28px;
    position: relative;
  }

  .day::before {
    content:'🎀';
    position:absolute;
    top:5px;
    left:5px;
    font-size:20px;
  }

  .popup {
    display:none;
    position: fixed;
    z-index: 9999;
    left:50%;
    top:50%;
    transform: translate(-50%,-50%);
    background:#fff4d9;
    color:#000;
    padding:22px;
    border-radius:12px;
    width:420px;
    max-height:80vh;
    overflow:auto;
    box-shadow: 0 12px 30px rgba(0,0,0,0.5);
  }

  .close {
    margin-top:12px;
    background:#e63946;
    color:#fff;
    border:none;
    padding:8px 12px;
    border-radius:6px;
    cursor:pointer;
  }

  /* Flocons dans popup */
  .popupSnowflake{
    position:absolute;
    top:-10px;
    color:white;
    user-select:none;
    pointer-events:none;
    font-size:14px;
    animation:fallPopup 6s linear infinite;
  }

  @keyframes fallPopup{
    0%{transform:translateY(-10px)}
    100%{transform:translateY(300px)}
  }

  /* Flocons fond */
  .snowflake{
    position:fixed;
    top:-10px;
    color:white;
    user-select:none;
    pointer-events:none;
    z-index:1;
    font-size:16px;
    animation:fallBackground 8s linear infinite;
  }

  @keyframes fallBackground{
    0%{transform:translateY(-10px)}
    100%{transform:translateY(110vh)}
  }
</style>
</head>
<body>

<h1>🎄 Calendrier de l'Avent 🎄</h1>

<div class="calendar" id="calendar"></div>

<div id="popup" class="popup">
  <div id="popupContent"></div>
  <button class="close" onclick="closePopup()">Fermer</button>
</div>

<script>
// Génération des cases 1 à 24
const calendar = document.getElementById('calendar');
for(let i=1;i<=24;i++){
  const dayDiv = document.createElement('div');
  dayDiv.className = 'day';
  dayDiv.textContent = i;
  dayDiv.onclick = () => openPopup(i);
  calendar.appendChild(dayDiv);
}

// Neige fond
(function(){
  const count=80;
  for(let i=0;i<count;i++){
    const el=document.createElement('div');
    el.className='snowflake';
    el.textContent='❄';
    el.style.left=Math.random()*100+'vw';
    el.style.opacity=0.4+Math.random()*0.6;
    el.style.fontSize=(8+Math.random()*18)+'px';
    el.style.animationDuration=(6+Math.random()*8)+'s';
    document.body.appendChild(el);
  }
})();

// Ouvrir popup
function openPopup(day){
  const box=document.getElementById('popupContent');
  box.innerHTML='';

  // Flocons dans popup
  for(let i=0;i<30;i++){
    const f=document.createElement('div');
    f.className='popupSnowflake';
    f.textContent='❄';
    f.style.left=Math.random()*380+'px';
    f.style.animationDuration=4+Math.random()*4+'s';
    box.appendChild(f);
  }

  // Contenu des cases
  const content = {
    1:`<h2>Jour 1</h2><p><strong style="color:red;">Info du Jour 🗞️</strong> La DiSI CO a été parmi les premiers établissements à mettre en place l'intranet ULLO.</p>`,

    2:`<h2>Jour 2</h2><p><strong style='color:red;'>Quiz du jour :</strong> Savez-vous par qui a été développé l'outil TaToo météo ?</p>
    <form id='quiz2'>
      <label><input type='radio' name='ans2' value='Nantes'> Nantes</label><br>
      <label><input type='radio' name='ans2' value='Angers'> Angers</label><br>
      <label><input type='radio' name='ans2' value='Rennes'> Rennes</label><br>
      <button type='button' onclick='checkQuiz("quiz2","Angers","res2","info2")'>Valider</button>
    </form>
    <p id='res2'></p>
    <p id='info2' style='display:none;'>TaToo météo a été déployé sur 120 000 postes entre mars et mai 2025.</p>`,

    3:`<h2>Jour 3</h2><p><strong style='color:red;'>Info du jour :</strong> Tous les ans, l'ESI d'Orléans participe au Cross de Bercy. Bravo aux participants !</p>`,

    4:`<h2>Jour 4</h2><p>Le site des Marsauderies accueille chaque année des nouveaux moutons 🐑</p>
    <form id='quiz4'>
      <label><input type='radio' name='ans4' value='1'> 1</label><br>
      <label><input type='radio' name='ans4' value='2'> 2</label><br>
      <label><input type='radio' name='ans4' value='3'> 3</label><br>
      <button type='button' onclick='checkQuiz("quiz4","3","res4")'>Valider</button>
    </form>
    <p id='res4'></p>`,

    5:`<h2>Jour 5</h2><p>Le mois de l'innovation publique a eu pour thème l’IA.</p>
    <form id='quiz5'>
      <label><input type='radio' name='ans5' value='1956'> 1956</label><br>
      <label><input type='radio' name='ans5' value='1962'> 1962</label><br>
      <label><input type='radio' name='ans5' value='1970'> 1970</label><br>
      <button type='button' onclick='checkQuiz("quiz5","1956","res5")'>Valider</button>
    </form>
    <p id='res5'></p>`,

    6:`<h2>Jour 6</h2><p>Recette apéritive : <a target='_blank' href='https://www.marmiton.org/recettes/recette_sapin-feuillete-au-pesto_383379.aspx'>Sapin feuilleté au pesto</a></p>`,

    7:`<h2>Jour 7</h2><p>Recette : <a target='_blank' href='https://www.marmiton.org/recettes/recette_gougeres-au-fromage_20095.aspx'>Gougères au fromage</a></p>`,

    8:`<h2>Jour 8</h2><p>Contenu à ajouter.</p>`,

    9:`<h2>Jour 9</h2><p>Contenu à ajouter.</p>`,

    10:`<h2>Jour 10</h2><p>Contenu à ajouter.</p>`,

    11:`<h2>Jour 11</h2><p>Contenu à ajouter.</p>`,

    12:`<h2>Jour 12</h2><p><strong>En lumière :</strong> Nous avons deux ruches dédiées à la biodiversité 🍯🐝</p>
    <input type="text" id="quiz12Input" placeholder="Votre réponse (ex : 1g)">
    <button type="button" onclick="checkOpenAnswer12()">Valider</button>
    <p id="quiz12Result"></p>`,

    13:`<h2>Jour 13</h2><p>Recette : <a target='_blank' href='https://www.marmiton.org/recettes/recette_huitres-gratinees-au-parmesan_56242.aspx'>Huîtres gratinées</a></p>`,

    14:`<h2>Jour 14</h2><p>Marchés de Noël en Loire-Atlantique : <a target='_blank' href='https://44.kidiklik.fr/articles/335276-les-marches-de-noel-nantes-et-en-loire-atlantique.html'>Voir la liste</a></p>`,

    15:`<h2>Jour 15</h2><p><strong>Relamping :</strong> les néons ont été remplacés par des panneaux LED dans une démarche ÉcoFiP 🌱💡</p>`,

    16:`<h2>Jour 16</h2><p>Contenu à ajouter.</p>`,

    17:`<h2>Jour 17</h2><p>Concours des pulls de Noël 🎅 Venez avec vos plus beaux pulls !</p>`,

    18:`<h2>Jour 18</h2><p>Contenu à ajouter.</p>`,

    19:`<h2>Jour 19</h2><p><strong style='color:red;'>Journée mondiale du pull de Noël 🎄</strong></p>
    <p><strong>Quiz :</strong> D'où vient la tradition du pull de Noël ?</p>
    <form id='quiz19'>
      <label><input type='radio' name='ans19' value='France'> France</label><br>
      <label><input type='radio' name='ans19' value='Suisse'> Suisse</label><br>
      <label><input type='radio' name='ans19' value='Angleterre'> Angleterre</label><br>
      <button type='button' onclick='checkQuiz("quiz19","Angleterre","res19","info19")'>Valider</button>
    </form>
    <p id='res19'></p>
    <p id='info19' style='display:none;'>La tradition vient d’Angleterre en 1980. Elle devient populaire grâce au film “Bridget Jones”.</p>`,

    20:`<h2>Jour 20</h2><p>Recette : <a target='_blank' href='https://www.marmiton.org/recettes/recette_vin-chaud-aux-epices_25224.aspx'>Vin chaud aux épices</a></p>`,

    21:`<h2>Jour 21</h2><p>En ce dimanche, n'oubliez pas de vous réchauffer avec un bon repas : <a target='_blank' href='https://www.marmiton.org/recettes/recette_gratin-dauphinois_13809.aspx'>Gratin dauphinois</a></p>`,

    22:`<h2>Jour 22</h2><p>Contenu à ajouter.</p>`,

    23:`<h2>Jour 23</h2><p>Contenu à ajouter.</p>`,

    24:`<h2>Jour 24</h2><p>Contenu à ajouter.</p>`
  };

  box.innerHTML += content[day];
  document.getElementById('popup').style.display='block';
}

// Fermer popup
function closePopup(){
  document.getElementById('popup').style.display='none';
}

// Quiz radio
function checkQuiz(formId, correct, resId, infoId){
  const form=document.getElementById(formId);
  const selected=form.querySelector("input[type=radio]:checked");
  const res=document.getElementById(resId);
  if(!selected){ res.textContent="Sélectionnez une réponse !"; return; }
  if(selected.value===correct){ res.textContent="Bonne réponse ! 👏"; }
  else{ res.textContent="Perdu ! La bonne réponse était : " + correct; }
  if(infoId) document.getElementById(infoId).style.display="block";
}

// Quiz texte
function checkOpenAnswer12(){
  const v=document.getElementById("quiz12Input").value.trim();
  const r=document.getElementById("quiz12Result");
  if(!v){ r.textContent="Veuillez entrer une réponse."; return; }
  r.innerHTML="Réponse : une abeille produit seulement 1/12 de cuillère de miel (≈ 7 g).";
}
</script>

</body>
</html>
