<template>
    <div class="cart-container">
        <div class="cart" :style="cart">
                <p class="cart-title">Shopping Cart</p>
                <!-- <p class="cart-empty" v-if="total == 0">Your cart is empty</p> -->
                <div class="items" v-for="(c,index) in cart" :key="`c-${index}`">
                    <img :src=c.coverImg class="item-image">
                    <div class="item-details">
                        <p class="item-title">{{c.name}}</p>
                        <p class="item-price">
                            <span>{{c.author}}</span>
                        </p>
                        <p class="item-qty">
                            <span>{{c.qty}}</span>
                        </p>
                    </div>
                </div>
            </div>
    </div>
    
</template>

<script>
export default {
    name:'cart',
    props:['cart'],
    data(){
        return{
          inlineBlock:{
              display:'inlineBlock',

          }
        }
    },
    computed:{
        
    }
}
</script>

<style scoped>
    .cart-container{
        width: 100%;
        background-color: #4DB6AC
    }

    .items{
        display: inline-block;
        margin: 0 25px;
        max-height: 200px;
     }

     .items img{
         max-height: 100px;
     }
</style>
