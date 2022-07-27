<template>
    <div class="d-flex justify-content-center mt-5">
        <div
            class="card" style="width: 20rem;">
                <img @click="openSecret()" :src="isClick == false ? 'img/secret.jpg' : 'img/'+ randomCard +'.jpg'" class="card-img-top">   
        </div>
    </div>
</template>

<script>
import { EventBus } from "../main";

export default {
    data(){
        return{
            cards: [],
            randomCard: null,
            isClick: false,
            isSelected: null
        }
    },
    created(){
        EventBus.$on("cards", (value) =>{
            this.cards = value
        });
        
        this.randomCard = Math.ceil(Math.random() * 4);
        EventBus.$emit("secretCard", this.randomCard);
        EventBus.$on("isSelected", (value) =>{
            this.isSelected = value;
        });
    },
    methods: {
        openSecret(){
            if(this.isSelected){
                this.isClick = true;
                EventBus.$emit("isOpened", true)
            }else{
                alert("Önce seçim yapmalısınız.")
            }
        }
    }
}
</script>