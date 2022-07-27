<template>
    <div class="d-flex flex-column">
        <div class="d-flex justify-content-center">
                <div
                    v-for="card in cards"
                    :key="card.id" 
                    class="card m-3 animate__animated"
                    style="width: 100%;"
                    id="card">
                        <img @click="selectImage(card.id, $event)" :src="card.image" class="">
                </div>

        </div>
        <app-secret-card></app-secret-card>
    </div>
    
</template>

<script>
import appSecretCard from '../components/SecretCard.vue'
import {EventBus} from '../main';

export default {
    components: {
      appSecretCard  
    },
    data(){
        return {
            cards: [
                {
                    id: 1,
                    image: "/img/1.jpg"
                },
                {
                    id: 2,
                    image: "/img/2.jpg"
                },
                {
                    id: 3,
                    image: "/img/3.jpg"
                },
                {
                    id: 4,
                    image: "/img/4.jpg"
                }
            ],
            selectedCard: null,
            secretCard: null
        }
    },
    methods: {
        selectImage(cardID, el){
            this.selectedCard = cardID;
            EventBus.$emit("isSelected", true);
            el.srcElement.classList.toggle("selected");
            el.srcElement.parentElement.classList.toggle("animate__headShake");
        }
    },
    created(){
        EventBus.$emit("cards", this.cards);
        EventBus.$on("isOpened", () =>{
            if(this.selectedCard == this.secretCard){
                EventBus.$emit("isSucces", true);
            }else{
                EventBus.$emit("isSucces", false);
            }
        });
        EventBus.$on("secretCard", (value) =>{
            this.secretCard = value;
        })
    }
}
</script>
<style scoped>
.selected {
    border: 3px solid red;
}
</style>