<meta charset="UTF-8">
<title>🎄 Calendrier de l'Avent 🎄</title>
<style>
  body { font-family: Arial, sans-serif; background: #064E3B; color: #fff; text-align: center; margin:0; padding:20px; overflow: hidden; }
  h1 { margin-top: 0; font-size: 44px; color: #FFD700; text-shadow: 3px 3px 6px #000; }
  .calendar { display: grid; grid-template-columns: repeat(6, 150px); gap: 15px; justify-content: center; margin: 20px auto; max-width: 960px; }
  .day { background: #e63946; width:150px; height:150px; cursor: pointer; font-weight: bold; color: #fff; text-shadow: 1px 1px 2px #000; box-shadow: 0 6px 12px rgba(0,0,0,0.5); display:flex; align-items:center; justify-content:center; font-size:28px; position: relative; }
  .day::before { content:'🎀'; position:absolute; top:5px; left:5px; font-size:20px; }
  .popup { display:none; position: fixed; z-index: 9999; left:50%; top:50%; transform: translate(-50%,-50%); background:#fff4d9; color:#000; padding:22px; border-radius:12px; width:420px; max-height:80vh; overflow:auto; box-shadow: 0 12px 30px rgba(0,0,0,0.5); }
  .close { margin-top:12px; background:#e63946; color:#fff; border:none; padding:8px 12px; border-radius:6px; cursor:pointer; }
  input[type='text']{padding:6px; width:70%;}
  a{ color:#064E3B; font-weight:bold; }
  .popupSnowflake{position:absolute; top:-10px; color:white; user-select:none; pointer-events:none; font-size:14px; animation:fallPopup 6s linear infinite;}
  @keyframes fallPopup{0%{transform:translateY(-10px)}100%{transform:translateY(300px)}}
  .snowflake{position:fixed; top:-10px; color:white; user-select:none; pointer-events:none; z-index:1; font-size:16px; animation:fallBackground 8s linear infinite;}
  @keyframes fallBackground{0%{transform:translateY(-10px)}100%{transform:translateY(110vh)}}
</style>

<h1>🎄 Calendrier de l'Avent 🎄</h1>

<div class="calendar" id="calendar"></div>

<div id="popup" class="popup">
  <div id="popupContent"></div>
  <button class="close" onclick="closePopup()">Fermer</button>
</div>

<script>
// Générer les cases 1 à 24
const calendar = document.getElementById('calendar');
for(let i=1;i<=24;i++){
  const dayDiv = document.createElement('div');
  dayDiv.className = 'day';
  dayDiv.textContent = i;
  dayDiv.onclick = () => openPopup(i);
  calendar.appendChild(dayDiv);
}

// Animation neige
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

// Ouvrir popup — **TOUTES LES CASES SONT OUVERTES**
function openPopup(day){
  const box=document.getElementById('popupContent');
  box.innerHTML='';

  for(let i=0;i<30;i++){
    const f=document.createElement('div');
    f.className='popupSnowflake';
    f.textContent='❄';
    f.style.left=Math.random()*380+'px';
    f.style.animationDuration=4+Math.random()*4+'s';
    box.appendChild(f);
  }

  switch(day){
    case 1: box.innerHTML+=`<h2>Jour 1</h2><p><strong style='color:red;'>Info du Jour🗞️</strong> La DiSI CO a été parmi les premiers établissements à mettre en place l'intranet ULLO.</p>`; break;
    case 2: box.innerHTML+=`<h2>Jour 2</h2><p><strong style='color:red;'>Quiz :</strong> Par qui a été développé l'outil TaToo météo ?</p>
      <form id='quiz2'><label><input type='radio' name='ans2' value='Nantes'> Nantes</label><br>
      <label><input type='radio' name='ans2' value='Angers'> Angers</label><br>
      <label><input type='radio' name='ans2' value='Rennes'> Rennes</label><br>
      <button type='button' onclick='checkQuiz("quiz2","Angers","res2","info2")'>Valider</button></form>
      <p id='res2'></p>
      <p id='info2' style='display:none;'>Déployé sur 120 000 postes entre mars et mai 2025.</p>`; break;

    case 3: box.innerHTML+=`<h2>Jour 3</h2><p><strong>🏃 Cross de Bercy :</strong><br>Nicolas 322e (5km)<br>Éric 630e (10km)<br>Charles-Étienne 127e (10km) 🎉</p>`; break;

    case 4: box.innerHTML+=`<h2>Jour 4</h2><p>Le site des Marsauderies accueille chaque année des nouveaux moutons 🐑</p><strong style='color:red;'>Quiz :</strong> Combien d’agneaux la DiSI CO a eu ce printemps ?</p>
      <form id='quiz4'><label><input type='radio' name='ans4' value='1'> 1</label><br>
      <label><input type='radio' name='ans4' value='2'> 2</label><br>
      <label><input type='radio' name='ans4' value='3'> 3</label><br>
      <button type='button' onclick='checkQuiz("quiz4","3","res4","info4")'>Valider</button></form>
      <p id='res4'></p>`; break;
    case 5: box.innerHTML+=`<h2>Jour 5</h2><p><strong style='color:red;'>Quiz :</strong> Le mois dernier a eu lieu le mois de l'innovation publique avec pour thème principal l'IA, savez vous en quelle année l’IA a été créée ?</p>
      <form id='quiz5'><label><input type='radio' name='ans5' value='1956'> 1956</label><br>
      <label><input type='radio' name='ans5' value='1962'> 1962</label><br>
      <label><input type='radio' name='ans5' value='1970'> 1970</label><br>
      <button type='button' onclick='checkQuiz("quiz5","1956","res5","info5")'>Valider</button></form><p id='res5'></p>`; break;

    case 6: box.innerHTML+=`<h2>Jour 6</h2><p><a href='https://www.marmiton.org/recettes/recette_sapin-feuillete-au-pesto_383379.aspx' target='_blank'>🌲 Sapin feuilleté au pesto</a></p>`; break;
    case 7: box.innerHTML+=`<h2>Jour 7</h2><p><a href='https://www.marmiton.org/recettes/recette_gougeres-au-fromage_20095.aspx' target='_blank'>🧀 Gougères au fromage</a></p>`; break;
    case 8:
  box.innerHTML += `
    <h2>Jour 8</h2>
    <p><strong style='color:red;'>Quiz :</strong> Savez-vous quel mois a eu lieu le "Mois à vélo" ? </p>Une action avec l'ESI de Rennes et la DiSI CO, avec un atelier réparation et un challenge Geovelo ?</p>
    <form id='quiz8'>
      <label><input type='radio' name='ans8' value='Mai'> Mai</label><br>
      <label><input type='radio' name='ans8' value='Juin'> Juin</label><br>
      <label><input type='radio' name='ans8' value='Septembre'> Septembre</label><br>
      <button type='button' onclick='checkQuiz("quiz8","Mai","res8","info8")'>Valider</button>
    </form>
    <p id='res8'></p>
    <p id='info8' style='display:none;'>Le "Mois à vélo" a eu lieu en Mai, avec atelier réparation et challenge Geovelo.</p>
  `;
  break;
    case 9:
  box.innerHTML += `
    <h2>Jour 9</h2>
    <p><strong style='color:red;'>Info du Jour 🗞️</strong></p>
    <p>Cette année, dans le cadre du DuoDay, l'ESI de Tours a eu le plaisir d'accueillir une personne avec un TSA (trouble du spectre autistique) passionnée et intéressée par l'informatique 💻✨.</p>
    <p>Ce moment a été rempli de joie et de partage, et nous sommes ravis d'avoir pu offrir une expérience enrichissante et chaleureuse pour tous.❤️</p>
  `;
  break;
    case 10:
  box.innerHTML += `
    <h2>Jour 10</h2>
    <p><strong style='color:red;'>Quiz :</strong> Savez-vous quel sport est actuellement au cœur d'un tournoi à la DiSI CO ?</p>
    <form id='quiz10'>
      <label><input type='radio' name='ans10' value='Fléchettes'> Fléchettes</label><br>
      <label><input type='radio' name='ans10' value='Babyfoot'> Babyfoot</label><br>
      <label><input type='radio' name='ans10' value='Lancer de hache'> Lancer de hache</label><br>
      <button type='button' onclick='checkQuiz("quiz10","Babyfoot","res10","info10")'>Valider</button>
    </form>
    <p id='res10'></p>
    <p id='info10' style='display:none;'>
      Le tournoi en cours à la DiSI CO est le tournoi de Babyfoot ! 🎉<br>
      Encore bravo à l'équipe Patators pour avoir remporté la coupe lors du dernier tournoi de Babyfoot entre la DiSI CO et l'ESI de Nantes 🏆
    </p>
  `;
  break;
   case 11:
  box.innerHTML += `
    <h2>Jour 11</h2>
    <p><strong style='color:red;'>Quiz :</strong> Savez-vous combien de stagiaires de seconde et première l'ESI de Rennes a accueillis cette année en juin ?</p>
    <form id='quiz11'>
      <label><input type='radio' name='ans11' value='1'> 1</label><br>
      <label><input type='radio' name='ans11' value='5'> 5</label><br>
      <label><input type='radio' name='ans11' value='10'> 10</label><br>
      <button type='button' onclick='checkQuiz("quiz11","5","res11","info11")'>Valider</button>
    </form>
    <p id='res11'></p>
    <p id='info11' style='display:none;'>Bravo ! L'ESI de Rennes a accueilli 5 stagiaires de seconde et première en juin. 🎉</p>
  `;
  break;
       case 12: box.innerHTML+=`<h2>Jour 12</h2><p><strong>En lumière :</strong> Nous avons 2 ruches aux Marsauderies pour la biodiversité 🍯🐝 et nous avons reçu des pots de miel.<p>Quiz : à votre avis, combien une abeille produit-elle de miel au cours de sa vie ? (g)</p>
      <input type="text" id="quiz12Input" placeholder="Votre réponse">
      <button type="button" onclick="checkOpenAnswer12()">Valider</button>
      <p id="quiz12Result"></p>`; break;

    case 13: box.innerHTML+=`<h2>Jour 13</h2><p><a href='https://www.marmiton.org/recettes/recette_huitres-gratinees-au-parmesan_56242.aspx' target='_blank'>🦪 Huîtres gratinées</a></p>`; break;
    case 14: box.innerHTML+=`<h2>Jour 14</h2><p><a href='https://44.kidiklik.fr/articles/335276-les-marches-de-noel-nantes-et-en-loire-atlantique.html' target='_blank'>🛍️ Marchés de Noël</a></p>`; break;
    case 15: box.innerHTML+=`<h2>Jour 15<p><strong style='color:red;'>Info du Jour<p></strong></h2><p>Relamping du couloir du rez-de-chaussée :<p></strong> les néons ont été remplacés par des panneaux LED💡 Cette démarche s'inscrit dans la politique <strong>ÉcoFiP</strong> de la direction<p>une vraie action écologique : réduction de la consommation électrique et moins de déchets.</p>`; break;
    case 16:
  box.innerHTML += `
    <h2>Jour 16</h2>
    <p><strong style='color:red;'>Info du Jour 🗞️</strong></p>
    <p>Un immense bravo à tous les agents qui ont participé aux salons étudiants cette année ! 👏✨</p>
    <p>Grâce à leur énergie, leur disponibilité et leur bonne humeur, ils ont brillamment représenté nos équipes et ont permis à de nombreux jeunes de découvrir nos métiers et nos missions. 🌟</p>
    <p>Merci à eux pour leur engagement et leur enthousiasme ! ❤️</p>
  `;
  break;
    case 17: box.innerHTML+=`<h2>Jour 17</h2><p><strong>Info :</strong> Concours des pulls de Noël le 19 décembre 🎅 ! <p>Venez avec votre plus beau pull de Noël et gagnez des chocolats 🍫 ! <p>A la DiSI nous prendrons une photo a 11H30 dans le hall des Marsauderies pour le vote final 📸.</p>`; break;
   case 18:
  box.innerHTML += `
    <h2>Jour 18</h2>
    <p><strong style='color:red;'>Quiz :</strong> Savez-vous dans combien de ministères l’ESI de Tours a mis en place la PSC (Protection Sociale Complémentaire) cette année sur PAYSAGE ?</p>

    <form id='quiz18'>
      <label><input type='radio' name='ans18' value='1'> 1 ministère</label><br>
      <label><input type='radio' name='ans18' value='2'> 2 ministères</label><br>
      <label><input type='radio' name='ans18' value='3'> 3 ministères</label><br>
      <button type='button' onclick='checkQuiz("quiz18","3","res18","info18")'>Valider</button>
    </form>

    <p id='res18'></p>
    <p id='info18' style='display:none;'>
      Bravo 🎉 L’ESI de Tours a bien déployé la PSC dans <strong>3 ministères</strong> : Agriculture, Environnement et Services du Premier Ministre.  
      Une très belle réussite pour nos équipes ! 🌟
    </p>
  `;
  break;
     case 19: box.innerHTML+=`<h2>Jour 19</h2><p>🎉 Aujourd'hui, c'est la Journée mondiale du pull de Noël 🎄</p><p><strong style='color:red;'>Quiz :</strong> Savez-vous d'où vient la tradition du jour des pulls de Noël ?</p><form id='quiz19'><label><input type='radio' name='ans19' value='France'> France</label><br><label><input type='radio' name='ans19' value='Suisse'> Suisse</label><br><label><input type='radio' name='ans19' value='Angleterre'> Angleterre</label><br><button type='button' onclick='checkQuiz("quiz19","Angleterre","res19","info19")'>Valider</button></form><p id='res19'></p><p id='info19' style='display:none;'>La tradition trouve ses origines en Angleterre en 1980. Mais ce n’est que dans les années 2000 que le pull trouvera son succès grâce au film “Bridget Jones“.</p> <p>Rappel : Une photo peut être proposée dans les établissements, a la DiSI CO rendez-vous à 11h30 dans le hall des Marsauderies pour participer au concours des pulls de Noël 🎁 !</p> <hr>`;
      `;
  `;
    break;
    case 20: box.innerHTML+=`<h2>Jour 20</h2><p><a href='https://www.marmiton.org/recettes/recette_vin-chaud-aux-epices_25224.aspx' target='_blank'>🍷 Vin chaud</a></p>`; break;
    case 21: box.innerHTML+=`<h2>Jour 21</h2><p><a href='https://www.marmiton.org/recettes/recette_gratin-dauphinois_13809.aspx' target='_blank'>🥔 Gratin dauphinois</a></p>`; break;
   case 22:
  box.innerHTML += `
    <h2>Jour 22</h2>
    <p><strong style="color:red;">Quiz du jour ❓📞</strong></p>

    <p>Savez-vous combien de sites ont basculé vers la portabilité <strong>ToIP</strong> cette année&nbsp;?</p>

    <form id="quiz22">
      <label>
        <input type="radio" name="ans22" value="19"> 19
      </label><br>

      <label>
        <input type="radio" name="ans22" value="21"> 21
      </label><br>

      <label>
        <input type="radio" name="ans22" value="28"> 28
      </label><br><br>

      <button type="button" onclick="checkQuiz('quiz22','19','res22')">Valider</button>
    </form>

    <p id="res22" style="font-weight:bold; margin-top:10px;"></p>
  `;
  break;
    case 23:
  box.innerHTML += `
    <h2>Jour 23</h2>
    <p><strong style="color:red;">Quiz du jour ❓🎓</strong></p>

    <p>Savez-vous combien d’<strong>apprentis</strong> ont été accueillis dans nos établissements en <strong>2025</strong>&nbsp;?</p>

    <form id="quiz23">
      <label>
        <input type="radio" name="ans23" value="8"> 8
      </label><br>

      <label>
        <input type="radio" name="ans23" value="12"> 12
      </label><br>

      <label>
        <input type="radio" name="ans23" value="14"> 14
      </label><br><br>

      <button type="button" onclick="checkQuiz('quiz23','14','res23')">Valider</button>
    </form>

    <p id="res23" style="font-weight:bold; margin-top:10px;"></p>
  `;
  break;
  case 24:
  box.innerHTML += `
    <h2>Jour 24</h2>

    <div style="position:relative; padding:15px; border:2px solid #c62828; border-radius:12px; background:#fff; color:#111; overflow:hidden;">

      <p><strong>Message de la Directrice</strong></p>
      <p>
        Chers collègues,
Merci pour votre engagement et votre professionnalisme au quotidien.
      </p>
      <p>
        C'est grâce à chacun d’entre vous que le système d’information apporte, chaque jour, à nos collègues, nos partenaires et nos usagers, ce dont ils ont le plus besoin : un environnement numérique et d’assistance de qualité, disponible, efficace et sécurisé. Bravo.
      </p>
      <p>
       Je vous souhaite à toutes et à tous de très belles fêtes de fin d’année.
      </p>

      <!-- Cotillons -->
      <div class="confetti-container">
        <div class="confetti" style="left:10%; background:#e63946;"></div>
        <div class="confetti" style="left:25%; background:#f1c40f;"></div>
        <div class="confetti" style="left:40%; background:#4caf50;"></div>
        <div class="confetti" style="left:55%; background:#2196f3;"></div>
        <div class="confetti" style="left:70%; background:#ff9800;"></div>
        <div class="confetti" style="left:85%; background:#9c27b0;"></div>
      </div>

      <style>
        .confetti-container { position:absolute; top:0; left:0; width:100%; height:100%; pointer-events:none; overflow:hidden; }
        .confetti {
          position:absolute;
          width:6px;
          height:12px;
          opacity:0.9;
          animation: fall 3s linear infinite;
        }
        .confetti:nth-child(odd) { animation-duration:2.5s; }
        .confetti:nth-child(even) { animation-duration:3.5s; }

        @keyframes fall {
          0% { top:-10px; transform:rotate(0deg); }
          100% { top:120%; transform:rotate(360deg); }
        }
      </style
  `;
  break;
  }

  document.getElementById('popup').style.display='block';
}

function closePopup(){ document.getElementById('popup').style.display='none'; }

function checkQuiz(formId, correct, resId, infoId){
  const form=document.getElementById(formId);
  const selected=form?form.querySelector('input[type=radio]:checked'):null;
  const res=document.getElementById(resId);
  if(!selected){ res.textContent='Sélectionnez une réponse !'; return; }
  if(selected.value===correct) res.textContent='Bonne réponse ! 👏';
  else res.textContent=`Loupé ! La bonne réponse est ${correct}.`;
  if(infoId){ document.getElementById(infoId).style.display='block'; }
}

function checkOpenAnswer12(){
  const v=document.getElementById('quiz12Input').value.trim();
  const r=document.getElementById('quiz12Result');
  if(!v){ r.textContent='Veuillez entrer une réponse.'; return; }
  r.innerHTML='Une abeille produit environ <strong>7g</strong> de miel dans sa vie.';
}
</script>
