<template>
  <div class="restaurant--row">
    <div class="wrapper--card">
        <RestaurantCardVue  v-for="(restaurant,index) of three_restaurant" :key="index" :info_restaurant="restaurant"/>
    </div>
  </div>
</template>

<script>
import RestaurantCardVue from './RestaurantCard.vue';

export default {
    name: "RestaurantRow",
    props: {
        three_restaurant: Array
    },
    components: {
        RestaurantCardVue
    },
    created(){
        //console.log("restaurants in row", this.three_restaurant);
    }
    
}
</script>

<style lang="scss">
    .restaurant--row {
        display: flex;
        flex-direction: column;
        .wrapper--card {
            display: flex;
            align-items: center;
            justify-content: space-between;
        }
    }
</style>