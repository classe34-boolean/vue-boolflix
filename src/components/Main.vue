<template>
  <main>
      <section 
        class="movies" 
        v-if="movieCards.length > 0">
          <h2>Film</h2>
          <ul class="cards">
              <Card 
                v-for="card in movieCards"
                :key="card.id"
                :item="card"
              />  
                
          </ul>  
      </section>
      <section
        class="series"
        v-if="serieCards.length > 0"
        >
        <h2>Serie TV</h2>
        <ul class="cards">
          <Card 
            v-for="serie in serieCards"
            :key="serie.id"
            :item="serie"  
          />
        </ul>
      </section>

      <h2 v-if="serieCards.length == 0 && movieCards.length == 0 && searching">La tua ricerca non ha prodotto risultati</h2>
  </main>
</template>

<script>
import Card from './Card';

export default {
    name: "Main",
    props: { 
        "movieCards": Array,
        "serieCards": Array,
        "searching": Boolean 
        },
    components: {
        Card
    }    
}
</script>

<style lang="scss">
  main {
    width: 90%;
    margin: 0 auto;
  }

  .series,
  .movies {
    margin-top: 30px;
  }

  .cards {
    display: flex;
    flex-wrap: wrap;

    li {
      list-style: none;
      // border: 1px solid black;
      margin: 10px;
    }

    img {
      width: 342px;
    }

    .flag {
        width: 40px;
    }
  }
</style>