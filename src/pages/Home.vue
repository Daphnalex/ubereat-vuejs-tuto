<template>
  <div class="home">
    <div class="header">
        <img src="https://d3i4yxtzktqr9n.cloudfront.net/web-eats-v2/ee037401cb5d31b23cf780808ee4ec1f.svg" alt="logo uber eats"/>
        <div class="wrapper--input">
            <input v-model="user_search_restaurant" type="text" placeholder="De quoi avez-vous envie ?"/>
            <div class="search">
                <div v-for="(restaurant,i) in search_restaurant" :key="i" class="container--restaurant--search">
                    <router-link class="search--router" :to="{name:'restaurant', params: {name: `${restaurant.name}`}}">
                        <div class="wrapper--img">
                            <img :src="restaurant.image" alt=""/>
                        </div>
                        <p>{{ restaurant.name }}</p>
                    </router-link>
                </div>
            </div>
        </div>
    </div>
    <div class="baniere"></div>
    <h2 class="title">
        Nos restaurants
    </h2>
    <RestaurantRowVue v-for="(restaurantList, i) in data_restaurant" :key="i" :three_restaurant="restaurantList"/>
  </div>
</template>

<script>
import BDD from '@/bdd';
import RestaurantRowVue from '@/components/RestaurantRow.vue';
import { onMounted, ref, watch } from 'vue';

export default {
    name: "HomePage",
    components: {
        RestaurantRowVue
    },
    setup(){
        class Restaurant {
            constructor(name, note, image, drive_time){
                this.name = name;
                this.note = note;
                this.image = image;
                this.drive_time = drive_time;
            }
        }

        let data_restaurant = ref([]);
        let all_restaurant = [];
        const makeDataRestaurant = () => {
            let three_restaurant = [];
            for(const restaurant of BDD){
                const new_restaurant = new Restaurant(restaurant.name, restaurant.note, restaurant.image, restaurant.drive_time);
                all_restaurant.push(new_restaurant);
                if(three_restaurant.length === 2) {
                    three_restaurant.push(new_restaurant);
                    data_restaurant.value.push(three_restaurant);
                    three_restaurant = [];
                } else {
                    three_restaurant.push(new_restaurant);
                }
            }
            console.log("restaurants in Home",data_restaurant.value[0][0]);
        }

        //User searched restaurant
        let user_search_restaurant=ref('');
        let search_restaurant = ref([]);
        watch(user_search_restaurant, new_value => {
            let regex = RegExp(new_value.toLowerCase());
            let new_search_restaurant = all_restaurant.filter(restaurant => regex.test(restaurant.name.toLowerCase()));
            //quand on utilise le ref il faut modifier le .value
            new_value === "" ? search_restaurant.value= [] : search_restaurant.value = new_search_restaurant;
        });

        onMounted(makeDataRestaurant);
        //return for use in template
        return {
            data_restaurant,
            user_search_restaurant,
            search_restaurant
        }
    }
}
</script>

<style lang="scss">
.home {
    .header {
        height: 120px;
        width: 100%;
        display: flex;
        align-items: center;
        justify-content: space-between;
    }
    .baniere {
            height: 200px;
            width: 100%;
            background-image: url('https://www.uber-assets.com/image/upload/f_auto,q_auto:eco,c_fill,w_1312,h_693/v1658225144/assets/30/7d0851-aad0-4583-a029-f339b38a1a9f/original/SSU_hero_2.png');
            background-size: cover;
            background-position: bottom center;
    }
    img {
        width: 200px;
    }
    .wrapper--input {
        position: relative;
        input {
            background-color: #f6f6f6;
            border: none;
            height: 60px;
            width: 400px;
            outline: none;
            padding-left: 20px;
        }
        .search {
            position: absolute;
            top: 100%;
            width: 100%;
            background: #fff;
            border: 1px solid grey;
            .container--restaurant--search {
                .search--router {
                    display: flex;
                    align-items: center;
                    padding: 10px;
                    .wrapper--img {
                    height: 60px;
                    width: 60px;
                    margin-right: 25px;
                    border-radius: 50%;
                    overflow:hidden;
                        img {
                            height: 100%;
                            width: auto;
                        }
                    }
                }
                
            }
        }
    }
    .title {
        font-size: 2rem;
        font-weight: bold;
    }
}


</style>