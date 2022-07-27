<template>
    <div class="d-flex flex-column align-items-center vh-100 justify-content-center">
        <div class="d-flex justify-content-center">
           <h2>Tebrikler Cevap Doğru!</h2>
        </div>
        <button @click="replay()" type="button" class="btn btn-success w-25 mt-2">Tekrar Oyna</button>
    </div>
</template>

<script>
import { EventBus } from "../main";

export default {
    methods: {
        replay(){
            EventBus.$emit("isReplay", true)
        }
    }
}
</script>