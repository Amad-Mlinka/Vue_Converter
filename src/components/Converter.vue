<template>
  <div id="container">
    <h1>{{physicalQuantity.name}}</h1>

    <div id="main">
      <input type="text" v-model="fromValue" placeholder="enter amount" />
      <select v-model="fromUnit">

      <option v-for="unit in physicalQuantity.units" v-bind:key="unit">{{unit}}</option>
      </select>
        <font-awesome-icon style="margin:auto;" icon="angle-double-right"/>
      <p id="result">{{result}}</p>
      <select v-model="resultUnit" placeholder="result">
 
        <option v-for="unit in physicalQuantity.units" v-bind:key="unit">{{unit}}</option>
      </select>
    </div>
  </div>
</template>


<script>
export default {
  name: 'Converter',
  
  props: {
    physicalQuantity: Object   
  },

  data: function(){            
       return{
         fromValue:1,
         fromUnit:"",
         resultUnit:""
       }
  },

  methods:
  {
      toMinutes: function(value,unit){   
          switch(unit){
            case("s"):
                return value/60;
            case("min"):
                return value;
            case("h"):
                 return value*60;
            case("day"):
                 return value*60*24;
            default:
                 console.log("toMinutes conversion failed - unit incorrect")
                 return value;
          }
      },

      toMeters: function(value,unit){   
        switch(unit){
            case("mm"):
                return value/1000;
            case("cm"):
                return value/100;
            case("m"):
                return value;
            case("km"):
                return value*1000;
            default:
                console.log("toMeters conversion failed - unit incorrect")
                return value;
        }
      },

      toCelsius: function(value,unit){   
        switch(unit){
            case("C"):
                return value;
            case("F"):
                return (value-32)*5/9;
            case("K"):
                return value-273.15;
            default:
                console.log("toCelsius conversion failed - unit incorrect")
                return value;
        }
      },
      toKilogram: function(value,unit){   
        switch(unit){
            case("mg"):
                return value*1000000;
            case("g"):
                return value*1000;
            case("kg"):
                return value;
            case("ton"):
                return value/1000;
            default:
                console.log("toKilogram conversion failed - unit incorrect")
                return value;
        }
      },

      toKS: function(value,unit){   
        switch(unit){
            case("m/s"):
                return value/(1000/3600);
            case("km/h"):
                return value;
            default:
                console.log("toKilogram conversion failed - unit incorrect")
                return value;
        }
      },
  },


  computed: {            
      result: function(){
            let value = parseFloat(this.fromValue);  
            if(isFinite(value)){                         

              switch(this.physicalQuantity.name){    
                case("Time"): {
                    /* ------------T I M E-------------*/
                        let valueInMinutes = this.toMinutes(value,this.fromUnit);  
                        switch(this.resultUnit){
                        case("s"):
                            return parseFloat((valueInMinutes*60).toFixed(5));   // limit to 5 decimals and parseFloat() it to remove redundant 0s
                        case("min"):
                            return parseFloat((valueInMinutes).toFixed(5));
                        case("h"):
                            return parseFloat((valueInMinutes/60).toFixed(5));
                        case("day"):
                            return parseFloat((valueInMinutes/60/24).toFixed(5));
                        default:
                            console.log("Error while converting time - resultUnit not detected!");
                            return "...";
                         }
                }
                  /* ----------------------------*/
                 case("Length"): {
                    /* ------------L E N G T H-------------*/
                        let valueInMeters= this.toMeters(value,this.fromUnit);  
                        switch(this.resultUnit){
                        case("mm"):
                            return parseFloat((valueInMeters*1000).toFixed(5));   
                        case("cm"):
                            return parseFloat((valueInMeters*100).toFixed(5));
                        case("m"):
                            return parseFloat((valueInMeters).toFixed(5));
                         case("km"):
                            return parseFloat((valueInMeters/1000).toFixed(5));
                        default:
                            console.log("Error while converting length - resultUnit not detected!");
                            return "...";
                        }
                 }
                  /* ----------------------------*/
                  case("Temperature"): {
                    /* ------------T E M P E R A T U R E-------------*/
                        let valueInCelsius= this.toCelsius(value,this.fromUnit);  
                        switch(this.resultUnit){
                        case("C"):
                            return parseFloat((valueInCelsius).toFixed(5));   
                        case("K"):
                            return parseFloat((valueInCelsius+273.15).toFixed(5));
                        case("F"):
                            return parseFloat((valueInCelsius*1.8+32).toFixed(5));
                        default:
                            console.log("Error while converting temperature - resultUnit not detected!");
                            return "...";
                        }
                  }
                  /* ----------------------------*/
                   case("Mass"): {
                    /* ------------M A S S-------------*/
                        let valueInKilogram= this.toKilogram(value,this.fromUnit);  
                        switch(this.resultUnit){
                        case("mg"):
                            return parseFloat((valueInKilogram/1000000).toFixed(18));   
                        case("g"):
                            return parseFloat((valueInKilogram/1000).toFixed(5));
                        case("kg"):
                            return parseFloat(valueInKilogram);
                        case("ton"):
                            return parseFloat((valueInKilogram*1000).toFixed(5));
                        default:
                            console.log("Error while converting mass - resultUnit not detected!");
                            return "...";
                        }
                  }
                  /* ----------------------------*/
                   case("Speed"): {
                    /* ------------S P E E D-------------*/
                        let valueInKS= this.toKS(value,this.fromUnit);  
                        switch(this.resultUnit){
                        case("m/s"):
                            return parseFloat(valueInKS*(1000/3600)).toFixed(5);   
                        case("km/h"):
                            return parseFloat((valueInKS));
                        default:
                            console.log("Error while converting speed - resultUnit not detected!");
                            return "...";
                        }
                  }
                  /* ----------------------------*/
              }
              
            }      
            return "...";  
      }
  }

}
</script>

<style scoped>
#container {
  width: 80vw;
  color: rgb(20, 20, 20);
  height: 100vh;
  display: flex;
  flex-direction: column;
  justify-content: flex-start;
  align-items: center;
}

h1 {
  width: 100%;
  background-color: rgb(250, 250, 250);
  box-sizing: border-box;
  padding: 40px;
}

#main {
  display: flex;
  box-sizing: border-box;
  padding: 40px;
  width: 60vw;
  justify-content: end;
  border: 1px solid #34495E;
 
}

#main > * {
  margin: 0 5px 0 5px;
}

input,
select,
#result {
  padding: 10px;
  border: 1px solid #41B883;
  border-radius: 10px;
  width: 10vw;
  font-family: "Source Sans Pro";
  font-size: 1em;
  display: flex;
  align-items: center;
  text-align: center;
}
</style>
