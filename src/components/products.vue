<template>
  <div>
    <vheader></vheader>
    <v-layout class="products--container">
        <v-flex wrap md12 xs12 lg12 :style="flexContainer">
          <div :style="cont" >
          <v-card addedProducts dark hover raised  :style="card"  v-for="(p,index) in prods" :key="`p-${index}`">
              <v-card-media :src=p.coverImg height="200px"  :style="imageSize"></v-card-media>
              <v-card-title primary-title>
              <div>
                  <h3 class="headline mb-0">{{p.name}}</h3>
                  <div>{{p.author}}</div>
              </div>
              </v-card-title>
              <v-card-actions>
              <v-btn color="teal darken-1" @click='added(p)'>Add to cart</v-btn>
              </v-card-actions>
          </v-card>
          </div>
      </v-flex>
    </v-layout>
    <cart v-bind:cart="cart" :style="cartfix"></cart>
  </div>  
</template>

<script>
  import axios from "axios";
  import Vue from 'vue';
  import cart from './cart'
  import headercomp from './header'
export default {
  name: "products",

  created() {
    var token = localStorage.getItem("token");
    //Getting data from the api
    axios({
      method: "get",
      url: "http://18.218.116.59:3030/api/user/getBooks",
      headers: {
        Authorization: `Bearer ${token}`
      }
    })
      //save the response in an array 
      .then(res => {
        if (res.data.status != 200) {
          console.log(" this is a error");
        } else {
          this.prods = res.data.data;
          console.log(this.prods);
          
        }
      })
      //error handling
      .catch(e => {
        console.log(e);
      });

      var addedProducts = []
  },

  data() {
    return {
      prods: [],
      cart:[],
      cont: {
        display: "inlineBlock"
      },
      flexContainer:{
        marginBottom:'35vh'
      },
      card: {
        width: "400px",
        display: "inline-block",
        margin: "50px 20px"
      },
      imageSize: {
          backgroundSize:'cover'
      },
      cartfix:{
        position:'fixed',
        bottom:'0',
        maxHeight:'70vh'
        
      }
    }
  },
  components:{
    'cart':cart,
    'vheader':headercomp
  },

  methods: {
    //A simple function to add an object in cart upon click
    added : function(p) {
      var found = false;
      this.cart.forEach((element) => {
        if(element.author == p.author){
          var newProduct = element;
          newProduct.qty += 1;
          found = true;
          }
        })
        if(!found){
          p.qty =1;
          this.cart.push(p)
        }
        console.log(this.cart)
      }
    }
  }

</script>
