<script setup>
import {ref,computed} from 'vue'
const name = 'Vue dinamico';
const styleColor = "color: blue";
const color = "color:green"
const color1 = "color:red"
const activo = true;
const arrayFrutas = ["🍎", "🍌", "🍉", "🍓", "🍒"];
const arrayFrutasL = [
        {
            name: "Manzana",
            price: "$1.00",
            description: "Una manzana",
            stock: 0,
        },
        {
            name: "Pera",
            price: "$2.00",
            description: "Una pera",
            stock: 10,
        },
        {
            name: "Naranja",
            price: "$3.00",
            description: "Una naranja",
            stock: 20,
        },
    ];
const objetoFruta = {
        name: "Manzana",
        price: "$1.00",
        description: "Una manzana",  
        id:"1",
}
//metodo - methods
const handleClick = (message) => {
  console.log(message)
}
const counter = ref(0);
const arrayFavoritos = ref([]);
const increment = () => {
  counter.value ++;
}
const menos = () => {
  counter.value --;
}
const reset = () => {
  counter.value = 0;
}
const add = () => {
  arrayFavoritos.value.push(counter.value);
}
const classCounter = computed(() =>{
  if(counter.value === 0){
    return 'zero'
  }
  if(counter.value > 0){
    return 'positive'
  }
  if(counter.value){
    return 'negative'
  }
});
const bloquearBtnAdd = computed(() => {
  const numSearch = arrayFavoritos.value.find((num) => num === counter.value);
  if(numSearch === 0) return true;
  return numSearch ? true : false;
})

</script>

<template> <!-- sintaxis de plantilla -->
  <h1>Const "variables"</h1>
  <hr>
  <br>
  <h2>Hola {{ name }}</h2>
  <br>
  <hr>
  <br>
  <h1>v-bind y su abreviación</h1>
  <hr>
  <br>
  <h2 v-bind:style="styleColor">Soy azul con v-bind</h2>
  <h2 :style="styleColor">soy azul pero con abreviación de v-bind</h2>
  <h2 :style ="styleColor">
    {{ activo ? "Estoy activo" : "Estoy inactivo"}}
  </h2>
  <h2 v-if="activo">Estoy activo por un v-if</h2>
  <h2 v-else-if="activo">Estoy inactivo por v-else-if</h2>
  <h2 v-else>Estoy indeciso</h2>
  <br>
  <hr>
  <br>
  <h1>V-for</h1>
  <hr>
  <br>
  <h2>Mostrando el array: {{ arrayFrutas }}</h2>
  <h2>Recorriendo el array con un v-for</h2>
  <ul>
    <li v-for="fruta in arrayFrutas">
      {{ fruta }}
    </li>
  </ul>
  <br>
  <hr>
  <br>
  <h1>Ejercicio v-for</h1>
  <hr>
  <br>
  <ul>
    <li v-for="frutal in arrayFrutasL" :key="frutal.name">
      {{ frutal.name }} - {{ frutal.price }} - {{ frutal.description }}
    </li>
  </ul>
  <br>
  <hr>
  <br>
  <h1>Recorrer objeto con v-for</h1>
  <hr>
  <br>
  {{objetoFruta}}
  <ul>
    <li v-for="(value, propiedad) in objetoFruta" :key="value">
      {{propiedad}} : {{ value }}
    </li>
  </ul>
  <br>
  <hr>
  <br>
  <h1>v-for con v-if</h1>
  <h2>mostrar las frutas que tenga mas que 0 en stock</h2>
  <hr>
  <br>
  <ul>
    <li v-for="fruta in arrayFrutasL">
      {{ fruta }}
    </li>
  </ul>
  <br>
  <h2>Resultado</h2>
  <ul>
    <template v-for="item in arrayFrutasL" :key="item.name">
      <li v-if="item.stock > 0">
      {{ item.name }} - {{ item.price }}
    </li>
    </template>
  </ul>
  <br>
  <hr>
  <br>
  <h1>Eventos</h1>
  <hr>
  <br>
  <button v-on:click="handleClick('evento con v-on')">
    Activame con v-on    
  </button>
  <br>
  <button @click="handleClick('evento con abreviación')">
    Activame con abreviación   
  </button>
  <br>
  <hr>
  <h2>juego de botones</h2>
  <br>
  <button v-on:click.right.prevent="handleClick('Texto Right')">
    Activame rigth    
  </button>
  <br>
  <button @click.middle="handleClick('Texto middle')">
    Activame middle 
  </button>
  <br>
  <button @click="handleClick('Texto left')">
    Activame left 
  </button>
  <br>
  <hr>
  <br>
  <h1>Reactividad</h1>
  <hr>
  <br>
  <h2>{{ counter }}</h2>
  <button @click="increment">
    Aumentar
  </button>
  <br>
  <hr>
  <br>
  <h1>Ejercicio Reactividad</h1>
  <hr>
  <br>
  <h2 v-if="counter == 0">{{ counter }}</h2>
  <h2 :style="color" v-if="counter > 0">{{ counter }}</h2>
  <h2 :style="color1" v-if="counter < 0">{{ counter }}</h2>
  <button @click="increment">
    Aumentar
  </button>
  <br>
  <button @click="menos">
    Disminuir
  </button>
  <br>
  <button @click="reset">
    Resetear
  </button>
  <br>
  <h1>Solución Ejercicio Reactividad</h1>
  <hr>
  <h2 :class="classCounter">{{ counter }}</h2>
  <button @click="increment">Increment</button>
  <button @click="menos">Decrement</button>
  <button @click="reset">Reset</button>
  <br>
  <hr>
  <br>
  <h1>Practica</h1>
  <hr>
  <br>
  <h2 :class="classCounter">{{ counter }}</h2>
  {{ arrayFavoritos }}
  <br>
  <button @click="increment">Increment</button>
  <button @click="menos">Decrement</button>
  <button @click="reset">Reset</button>
  <button @click="add" :disabled="bloquearBtnAdd">Add</button>
  <ul>
    <li v-for="(num,index) in arrayFavoritos" :key="index">
      {{ num }}
    </li>
  </ul>
  
  
  
</template>



<style>
h1 {
  color: red;
}
.positive{
  color: green;
}
.negative{
  color:red;
}
.zero{
  color:black;
}
</style>