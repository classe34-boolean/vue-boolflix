<template>
    <li class="flip-card">
        <div class="flip-card-inner">
            <div class="flip-card-front">
                <img 
                    v-if="item.poster_path"
                    :src="`https://image.tmdb.org/t/p/w342${item.poster_path}`" 
                    :alt="item.title ? item.title : item.name">
                <img 
                    v-else
                    src="https://www.altavod.com/assets/images/poster-placeholder.png" 
                    :alt="`Copertina ${item.title ? item.title : item.name}`">
            </div>
            <div class="flip-card-back">
                <h2>{{ item.title ? item.title : item.name }}</h2>
                <h4>{{ item.original_title ? item.original_title : item.original_name }}</h4>
                <img 
                    class="flag"
                    :src="require(`../assets/images/${item.original_language}.png`)" 
                    :alt="`bandiera ${item.original_language}`"
                    v-if="availableFlags.includes(item.original_language)"
                    >
                <p v-else>{{ item.original_language }}</p>
                <div>
                    <i
                        v-for="n in 5"
                        :key="n"
                        :class="(n <= getVote()) ? 'fas' : 'far'" 
                        class="fa-star"
                    ></i>
                </div>
                <strong>Trama</strong>
                <p>{{ item.overview }}</p>
            </div>
        </div>
    </li>
</template>

<script>
export default {
    name: "Card",
    data: function() {
        return {
            availableFlags: [ 'it', 'en' ]
        };
    },
    methods: {
        getTitle: function() {
           if(this.item.title) {
               return this.item.title;
           } else {
               return this.item.name;
           }    
        },
        getOriginalTitle: function() {
            if(this.item.original_title) {
               return this.item.original_title;
           } else {
               return this.item.original_name;
           }
        },
        getVote: function() {
            return Math.ceil(this.item.vote_average / 2);
        }
    },
    props: {
        "item": Object
    }
}
</script>

<style lang="scss">
    .flip-card {
        background-color: transparent;
        width: 342px;
        height: 513px;
        perspective: 1000px; /* Remove this if you don't want the 3D effect */
    }

    /* This container is needed to position the front and back side */
    .flip-card-inner {
        position: relative;
        width: 100%;
        height: 100%;
        text-align: center;
        transition: transform 0.8s;
        transform-style: preserve-3d;
    }

    /* Do an horizontal flip when you move the mouse over the flip box container */
    .flip-card:hover .flip-card-inner {
        transform: rotateY(180deg);
    }

    /* Position the front and back side */
    .flip-card-front, .flip-card-back {
        position: absolute;
        width: 100%;
        height: 100%;
        -webkit-backface-visibility: hidden; /* Safari */
        backface-visibility: hidden;
    }

    /* Style the front side (fallback if image is missing) */
    .flip-card-front {
        background-color: black;
        color: white;
    }

    /* Style the back side */
    .flip-card-back {
        padding: 20px;
        background-color: black;
        color: white;
        transform: rotateY(180deg);

        & > * {
            margin-bottom: 15px;
        }
        p {
            text-align: justify;
        }
    }
</style>