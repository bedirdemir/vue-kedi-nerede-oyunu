<template>
    <div class="d-flex justify-content-center mt-5">
        <div
            class="card animate__animated" style="width: 20rem;">
                <img @click="openSecret($event)" :src="isClick == false ? 'img/secret.jpg' : 'img/'+ randomCard +'.jpg'" class="">   
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
        openSecret(el){
            if(this.isSelected){
                this.isClick = true;
                setTimeout(() => {
                    EventBus.$emit("isOpened", true)
                },1500)
            }else{
                alert("Önce seçim yapmalısınız.")
            }
            el.srcElement.parentElement.classList.toggle("animate__flipInY");
        }
    }
}
</script>