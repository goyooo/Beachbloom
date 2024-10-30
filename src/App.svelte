<script>
  import * as d3 from "d3"
  import playas from "/src/data/playas.csv"
  // import atletas from "/src/data/playas.json"

  console.log("playas", playas)

    /* 1. cuantitativo: alto de la palmera */
  const minmaxalto = d3.extent(playas, (d) => d.turistas)
  let altura = d3.scaleLinear()
    .domain(minmaxalto).range([1, 12])

    /* 2. cuantitativo: cantidad de hojas  */
  const minmaxhojas = d3.extent(playas,(d) => d.distancia)
  let hojas = d3.scaleLinear()
    .domain(minmaxhojas).range([0, 6])

    /* 3. cuantitativo: color de la arena    */
  const minmaxsilice = d3.extent(playas,(d) => d.silice)
  let silice = d3.scaleLinear()
  .domain(minmaxsilice).range([50, 90])

    /* 4. categorico: hemisferio */
  const cocos = d3
    .scaleOrdinal()
    .domain(["N", "S"])
    .range([false, true])

    /* 5.variables para las referencias */
  let alturaRef = [12, 7, 4]
  let siliceRef = [90, 80, 70, 60, 50]
</script>

<div class="body" style="background-color:#CCF7F4;">
  <div class="header">
    <img class="cangrejo" style="margin-top: -25px;" src="./images/cangrejo.png" width="50" alt="cangrejo">
    <h3 class="headline"> BeachBlooms </h3>
    <img class="cangrejo" style="margin-top: -25px;" src="./images/cangrejo.png" width="50" alt="cangrejo">
    
  </div>
  <p class="subtitulo"> Las 20 playas más visitadas segun Tripadvisor como palmeras</p>



 <div class="referencias-container">
  <div class="primer-bloque-container">

    <div class="container_uno">
      <p class="reff"> 1.Cada trozo del tronco representa 100k turistas por año</p>
      <div class="heightref">
          {#each alturaRef as n}
            <div class="troncos"> 
              <div class="tope"><img src="./images/tope.png" width="40" alt="tope"> </div>
                {#each Array(n) as _,i}
                  <img src="./images/Rect.png" width="30" alt="cuad">
                {/each}
              <p style="font-family:fantasy; margin-left:-12px; margin-top:3px; font-size:20px">{n}00.000</p>
            </div>
          {/each}
      </div>
    </div>

    <div class="container_dos">
      <p class="reff">2.cuan blanca es la arena representa el porcentaje de sílica en la arena</p>
      <div class="loop-container">
        {#each siliceRef as n}
          <div class="arenaref">
            <svg width="90" height="55" xmlns="http://www.w3.org/2000/svg">
              <rect
                width="90"
                height="55"
                ry="20"
                fill=hsl(42,77%,{n}%)> 
              </rect>
            </svg>
            <p style="margin: auto;font-family:fantasy; font-size:20px">{n}%</p>
          </div>
        {/each}
      </div>
   </div>
  </div>

  <div class="segundo-bloque-container">
    <div class="contIzq">
      <p class="reff">3.Cada par de hojas representa 3000km desde Buenos Aires</p>
      <div class="palms">
        <img src="./images/hojas1fr.png" width="210" alt="cuad">
        <img src="./images/hojas2fr.png" width="210" alt="cuad">
        <img src="./images/hojas3fr.png" width="210" alt="cuad">
      </div>
      <div class="kmrefs">
        <p class="km">3000km</p>
        <p class="km">6000km</p>
        <p class="km">9000km</p>
      </div>
      </div>
    

    <div class="contDer">
      <p class="reff" style="margin-top: -15px;">4.Los cocos indican si la playa esta en el hemisferio sur</p>
      <div class="cocos">
        <img src="./images/hn.png" width="210" alt="cuad">
        <img src="./images/hs.png" width="210" alt="cuad">
        <div class="hemref">
          <p>Hemisferio Norte</p>
          <p>Hemisferio Sur</p>
        </div>
      </div>
    </div>
  </div>
  </div>

  <div class="playicas">
     {#each playas as playa}
      <div class="palmeras">
        <div class="hojas">
          {#if hojas(playa.distancia)<=2}
            <img src="./images/hojas1fr.png" width="250" alt="hoja">
          {:else if hojas(playa.distancia)<=4}
            <img src="./images/hojas2fr.png" width="300" alt="hoja">
          {:else if hojas(playa.distancia)<=6}
            <img src="./images/hojas3fr.png" width="300" alt="hoja">
          {/if}
        </div>

        <div class="cocos">
          <!-- {#if cocos(playa.hemisferio)} -->
            <svg width="150" height="150" xmlns="http://www.w3.org/2000/svg">
              <circle r="18"cx="35" cy="115" fill="#692D08" stroke="#7D411C" stroke-width="2"> </circle>
              <circle r="2" cx="38" cy="115"></circle>
              <circle r="2" cx="42" cy="123"></circle>
              <circle r="18" cx="62" cy="115" fill="#692D08" stroke="#7D411C" stroke-width="2"> </circle>
              <circle r="2" cx="66" cy="115"></circle>
              <circle r="2" cx="75" cy="115"></circle>
              <circle r="2" cx="70" cy="123"></circle>
            </svg>
          <!-- {/if} -->
        </div>

        <div class="tronco">
          {#each Array(playa.turistas) as _,i}
            <img src="./images/Rect.png" width="30" alt="cuad">
          {/each}
        </div>

        <div class="arenica">
          <svg width="150" height="75" xmlns="http://www.w3.org/2000/svg">
            <rect
              width="150"
              height="75"
              ry="20"
              fill=hsl(44,77%,{silice(playa.silice)}%)> 
          </rect>
          </svg>
        </div>
        
        <div class="nombre">
          <p>{playa.nombre}</p>
        </div>

      </div>
     {/each}
  </div>

</div>

<style>

  .body{
    margin-top: -20px;
  }

  .header {
    display: flex;
    justify-content: center;
    align-items: center;
    margin-bottom: 40px;
    padding: 50px;
    margin-bottom: 10px;
 }

 .headline{
    font-family: 'Super Woobly';
    font-size: 40px;
    text-align: center;
    margin: 20px;
    margin-top: -20px;
 }

 .subtitulo{
    font-size: 28px;
    text-align: center;
    position:relative;
    bottom:50px;
    font-family:'Super Funky';
 } 

  .primer-bloque-container{
    display:flex;
    flex-direction: row;
    justify-content: space-evenly;
    margin-top: -20px;
  }
  .container_uno{
    display: flex;
    flex-direction: column;
    align-items: center;
  }
  .container_dos{
    margin-top: auto;
    margin-bottom: auto;
    align-items: center;
  }

 .heightref{
  display: flex;
  flex-direction: row;
  gap: 70px;
  align-items: end;
 }
 .troncos{
  display: flex;
  flex-direction: column;
 }
 .tope{
  margin-left: -5px;
  margin-bottom: -15px;
  z-index: 0;
 }

 .loop-container{
  gap: 20px;
  display: flex;
 }
 .arenaref{
  display: flex;
  flex-direction: column;
 }

 .segundo-bloque-container{
  display: flex;
  flex-direction: row;
 }
 .contIzq{
  width: 60%;
  display: flex;
  flex-direction: column;
 }
 .contDer{
  width: 35%;
  margin-top: -25px;
 }

 .palms{
  margin: auto;
 }
 .kmrefs{
  display: flex;
  gap:155px;
  margin-left: auto;
  margin-right: auto;
  margin-top: -20px;
  font-family:fantasy;
  font-size: 20px;
 }
 .hemref{
  display: flex;
  gap: 100px;
  justify-content: center;
  margin-top: -40px;
  font-family:fantasy;
  font-size: 20px;
 }
 .cocos{
  margin-top: -30px;
 }

 .reff{
  font-family:Verdana, Arial, Helvetica, sans-serif;
  font-size: 15px;
  margin-left: auto;
  margin-right: auto;
 }





  .palmeras{
    display: flex;
    flex-direction: column;
    align-items: center;
    margin-bottom: 20px;
  }

  .hojas{
    position: relative;
    margin: -220px;
    z-index: 3;
  }

  .cocos{
    position: relative;
    z-index: 2;
    top: 60px;
    left: 20px;
  }

  .tronco{
    display: flex;
    flex-direction: column;
    position: relative;
    z-index: 1;
  }
  
  .arenica{
    bottom:35px;
    position: relative;
    z-index: 0;
  }

  .playicas{
    position: relative;
    display: flex;
    justify-content: center;
    align-items: end;
    flex-wrap: wrap;
    gap: 150px;
    margin-top: 250px;
  }

  .nombre{
    font-size: 48px;
    font-family:'Super Dream';
    position: relative;
    bottom: 60px;
  }

</style>