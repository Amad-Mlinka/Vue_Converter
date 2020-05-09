
<template>
 <div id="nav">
     <div id="header">
         <img src="../assets/logo.png" height="30" width="30">
         First attempt at a Vue Converter 
    </div>
     <a v-for="quantity in quantities" v-bind:key="quantity.name" @click="$emit('select-quantity',quantity)" > 
        {{quantity.name}}
     </a>
     <div id="footer">
         Made by <a href="https://amadmlinaric.com/">Amad Mlinaric</a>
     </div>
 </div>
</template>



<script>
export default {
  name:'Navbar',
  data: function(){
      return{
          quantities: [  
           {name:"Length",id:0, units:["mm","cm","m","km"]},
           {name:"Temperature",id:1, units:["C","K","F"]},
           {name:"Time",id:2, units:["s","min","h","day"]},
           {name:"Mass",id:3, units:["mg","g","kg","ton"]},
           {name:"Speed",id:4, units:["m/s","km/h"]}
          ]
      }
  },
  methods:{
   /* ...... */
  }
}
</script>




<style scoped>
    #nav{
        display:flex;
        flex-direction:column;
        height:100vh;
        width:20vw;
        background-color:#34495E;
        color:white;
    }


    #nav>div{
        display:flex;
        flex-direction:column;
        justify-content:center;
        align-items:center;
        padding:20px 0 20px 0;
        text-align:Center;
        vertical-align:middle;
    }

    #header>img{
       background-color:white;
       padding:10px;
       border-radius:20%;
       margin: 5px;
    }

    a{
       text-align:center;
       padding:20px;
       background-color:#41B883;
       transition:background-color 0.5s;
       cursor:pointer;       
    }

    #footer a{
       text-align:center;
       padding:20px;
       background-color:#41B883;
       border-radius: 50%;
       transition:background-color 0.5s;
       cursor:pointer;
       text-decoration: none;
       color: white;
    }
    a:hover{
        background-color:#41B883;
    }

    #footer{
        height:15vh;
        background-color:#34495E;
        margin-top:auto; 
        box-sizing:border-box;
        padding:15px;
        font-size:0.8em;
    }



</style>