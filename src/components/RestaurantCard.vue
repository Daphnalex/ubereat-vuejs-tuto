<template>
    <router-link class="restaurant--router" :to="{name: 'restaurant', params: {name: `${info_restaurant.name}`}}">
        <div class="restaurant--card">
            <div class="restaurant--image" :style="{'backgroundImage': `url(${info_restaurant.image})`}">
            </div>
            <div class="restaurant--information">
                <div class="top">
                    <p class="name">
                        {{ info_restaurant.name }}
                    </p>
                    <p class="note">
                        <span>{{ info_restaurant.note }}</span>
                    </p>
                </div>
                <p class="time">
                    {{ info_restaurant.drive_time }}
                </p>
            </div>
        </div>
    </router-link>
</template>

<script>
export default {
    name: "RestaurantCard",
    props: {
        info_restaurant: Object
    },
}
</script>

<style lang="scss">
a.restaurant--router {
    display: flex;
    width: 100%;
    justify-content: center;
    align-items: center;
    text-decoration: none;
    margin: 10px;
    padding: 5px;
    color: #000;
    .restaurant--card {
        width: 90%;
        height: 30vh;
        p {
            margin: 0;
        }
        .restaurant--image {
            background-image: url("https://cn-geo1.uber.com/image-proc/resize/eats/format=webp/width=550/height=440/quality=70/srcb64=aHR0cHM6Ly9kMXJhbHNvZ25qbmczNy5jbG91ZGZyb250Lm5ldC8zNzg4MDJiMC1jNTI4LTQ4MjktYjBiNS0wY2M2NDBkZjYzY2QuanBlZw==");
            height: 70%;
            background-size: cover;
            background-position: center;
        }
        .restaurant--information {
            display: flex;
            flex-direction: column;
            margin: 10px 0px;
            .top {
                display: flex;
                align-items: center;
                justify-content: space-between;
                .note {
                    background-color: #eeeeee;
                    height: 30px;
                    width: 30px;
                    display: flex;
                    justify-content: center;
                    align-items: center;
                    font-size: 0.8rem;
                    border-radius: 50%;
                }
            }
            .time {
                font-size: 0.9rem;
            }
        }
    }
}
a.restaurant--router:hover {
    background-color: #06C167;
    text-decoration: none;
}
</style>