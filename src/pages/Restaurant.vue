<template>
    <div class="restaurant--vue">
        <div class="redirect--home">
            <a href="/">Retour Accueil</a>
        </div>
        <div class="restaurant--name">
            <h1>
            {{ restaurant_find.name }}
            </h1>
        </div>
        <div class="restaurant--image">
            <img :src="restaurant_find.image" alt="">
        </div>
        <div class="restaurant--info">
            <div class="restaurant--note">
                <span class="restaurant--info--title">Note: </span>{{ restaurant_find.note }}
            </div>
            <div class="restaurant--driveTime">
                <span class="restaurant--info--title">Temps d'attente moyen: </span>{{ restaurant_find.drive_time }}
            </div>
        </div>
    </div>
  <p></p>
</template>

<script>
import { ref } from 'vue';
import BDD from '../bdd.js';
import { useRoute } from 'vue-router';

export default {
    name: "RestaurantVue",
    setup() {
        const route = useRoute();
        let restaurant_find = ref({});
        restaurant_find.value = BDD.find(restaurant => restaurant.name.toLowerCase() === route.params.name.toLowerCase());
        console.log("restaurant_find", restaurant_find.value);
        return {
            restaurant_find
        }
    }
}
</script>

<style lang="scss">
.restaurant--vue {
    display: flex;
    flex-direction: column;
    .redirect--home {
        margin-top: 2em;
        font-weight: 400;
        text-decoration: none !important;
        a:hover {
            height: 50px;
            font-weight: 900;
            cursor: pointer;
        }
    }
    .restaurant--name {
        h1{}
    }
    .restaurant--image {
        width: 100%;
        max-height: 400px;
        overflow: hidden;
        display: flex;
        align-items: center;
        justify-content: center;
        margin-bottom: 2em;
        img {
            width: 70%;
            height: auto;
        }
    }
    .restaurant--info {
        display: flex;
        flex-direction: row;
        justify-content: space-around;
        div {
            .restaurant--info--title{
                font-weight: bold;
            }
        }
        .restaurant--note {}
        .restaurant--driveTime {}
    }
}

</style>