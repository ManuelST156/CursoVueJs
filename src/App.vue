<template>

  <div class="container text-center mt-3">

    <h1>hola</h1>

    <h2  :class= "contadorComp">{{ contador }}</h2>

    <div class="btn-group">

      <button @click="increment" class="btn btn-success">Aummentar contador</button>
      <button @click="decrease" class="btn btn-danger">Disminuir contador</button>
      <button @click="reset" class="btn btn-secondary">Resetear contador</button>
      <button @click="add" :disabled="compararElementos" class="btn btn-primary">Agregar numero</button>
    </div>
   
    <ul class="list-group mt-4">
      <li class="list-group-item" v-for="(num, index) in arrayElementos" :key="index">
        {{ num }}
      </li>
    </ul>

    <!-- <ul v-if="bandera">


      <template v-for="(objetos,index) in objetosDeVidaReal" :key="objetos.nombre" >

        <li v-if="objetos.cantidad>2">
          
          {{index+1}} -) nombre: {{ objetos.nombre }}, Cantidad: {{ objetos.cantidad }}, Color: {{ objetos.color }}
        
        </li>
        
      </template>
    </ul> -->

  
  </div>

  

</template>  



<style>
h1{
  color: red;
}

.positive{
  color:green;
}

.negative{
  color:red;
}

.neutro{
  color:blue;
}

</style>


<script setup>

//const arrayFruta= ["🍎","🍐","🍇","🍓","🟠"];

  import {ref, computed} from 'vue';


  const objetosDeVidaReal = [
      { nombre: "Silla", cantidad: 4, color: "Marrón" },
      { nombre: "Mesa", cantidad: 1, color: "Negro" },
      { nombre: "Teléfono", cantidad: 2, color: "Plateado" },
      { nombre: "Cuchara", cantidad: 6, color: "Plateado" },
      { nombre: "Plato", cantidad: 8, color: "Blanco" }
    ];


  var bandera=false;

  const contador= ref(0);

  const arrayElementos=ref([]);

  const increment=() => {
    contador.value ++;
  };

  const decrease=() =>{

    contador.value --;
  }

  const reset=()=>{
    contador.value=0;
  }


  const contadorComp=computed(()=>{
    
    if(contador.value>0)
    {
      return 'positive';
    }
    else if(contador.value<0)
    {
      return 'negative';
    }
    else{
      return 'neutro';
    }
  });

  const compararElementos=computed(()=>{

    const numBusqueda= arrayElementos.value.find((num) => num === contador.value);


    return numBusqueda===0 ? true : numBusqueda ? true: false;

  });
  
  const add=()=>{
    arrayElementos.value.push(contador.value);
  }

</script>



<!-- //Notas 

1-) Se puede usar llaves dobles para poner variables en el template de forma mas sencilla. 

2-) v-bind simplifica el uso de atributos y el manejo de estos, y su abreviacion es : 

3-) Al usar llaves dobles o bigotes para traer datos de variables del script al template, puedo utilizar expresiones, como toUperCase

4-) Puedo utilizar arreglos para mostrar atributos o datos desde el script

5-) Puedo usr llaves dobles o interpolacion de texto para cargar un arreglo como texto

6-) Con operadores ternarios puedo comprobar la veracidad de una constante y mostrar algo espe, dependiendo condicion

7-) v-if, v-else, v-else-if son utilizados para manejar condiciones sin interpolar texto, y tienen que ser utilizados seguidos

8-) EL v-show unicamente permite ocultar el elemento cuando no se cumpla la condicion, en vez de destruirlo como hace el v-if
Si vamos a alternar mucho un elemento es mejor usar v-show y v-if si es poco probable que cambie la condicion


Ejemplo de lo visto hasta ahora 
<h1>Hola {{ name.toUpperCase() }}</h1>

<h2 :style="color">Probando</h2> 

<h2 :style="`color:${arrayColores[3]}`">Mi color</h2>

<h2>{{ comp ? 'Estoy activo' : 'Estoy inactivo' }}</h2>
<h2 v-if="comp===true">Es verdad</h2>
<h2 v-else-if="comp===false"> No Es verdad</h2>
<h2 v-else>solo estoy</h2>


<h2 v-show="comp">Mostrando</h2>


9-) v-for se utiliza para iterar elementos y usamos key como llave unica, y para mostrar usamos llaves dobles

<ul>
<li v-for="(fruta,index) in arrayFruta" :key="index" >{{index+1}}-{{fruta}}</li>
</ul>

<ul>
  <li v-for="(objetos,index) in objetosDeVidaReal" :key="objetos.nombre">
    {{index+1}} -) nombre: {{ objetos.nombre }}, Cantidad: {{ objetos.cantidad }}, Color: {{ objetos.color }}
  </li>
</ul>

<ul>
  <li v-for="(obValue, obPropiedad) in objetoPlato" :key="obValue.nombre">

    {{obPropiedad}}: {{ obValue }}
  </li>

</ul>

10-) v-on se utiliza para eventos

11-) con el modificador  @click.right o middle podemos acceder al evento mediante click derecho. Si colocamos @click.rigth.prevent, evitamos que aparezca el menu por defecto que 
tiene el navegador

12-) La reactividad es util ya que permite que podamos hacer cambios en tiempo real a un dom. El ref que importammos y aplicamos en una variable, hace que sea una variable
reactiva, lo que significa que se actualizara su valor en el dom de manera automatica al llamar un evento. Pero, en el script para acceder hay que usar la propiedad .value
ya que trae un objeto la variable ref

13-) Una funcion computada es una que se utiliza para usar variables reactiva.


Fin nota-->



<!-- <script setup>
import HelloWorld from './components/HelloWorld.vue'
import TheWelcome from './components/TheWelcome.vue'
</script>

<template>
  <header>
    <img alt="Vue logo" class="logo" src="./assets/logo.svg" width="125" height="125" />

    <div class="wrapper">
      <HelloWorld msg="You did it!" />
    </div>
  </header>

  <main>
    <TheWelcome />
  </main>
</template>

<style scoped>
header {
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
}
</style> -->
