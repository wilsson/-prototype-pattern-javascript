PATRON PROTOTYPE
===================
Continuando la saga de los post sobre patrones de diseño en javaScript, en este hablaremos del patron prototype.

Del patron prototype podemos decir que se centra en la creación de objetos que atúan como prototipos para otros objetos, através de la herencia de prototipos.

La herencia de prototipos evita el uso de clases por completo, ventaja la cual podemos encontrar nativamente atraves de prototipos en lugar de tratar de imitar caracteristicas de otros lenguajes.
Para entender mejor, algunos conceptos previos: -

#### Que es un prototipo? 

Un prototipo es un objeto que viene hacer un molde para uno o más objetos, muy util para crear varias instancias de un objeto.

###### ejemplo de un prototipo persona

```js
var prototipoPersona = {
  caminar:function(){
    this.energia-= 1;
  }
}
```

###### para crear objetos a partir de prototipos:
Es nesesario usar 
```js 
Object.create(miPrototipo);
```

```js
var pedro = Object(prototipoPersona);
// por ultimo dichos objetos creados de esta forma deben ser inicializados
pedro.energia = 10;
pedro.caminar()
pedro.energia // => dara como resultado 9
```


#### Objeto prototype - 
Objeto que proporciona propiedades compartidas por otros objetos.
Cada objeto está vinculado a un objeto ```prototype``` de la que puede heredar propiedades.Todos los objetos creados a partir de objetos literales están vinculados a ```Object.prototype```.
```js
function demoPrototype(){
  //--
}
/* creando una propiedad nueva del objecto prototype la cual podra ser compartida en otros objetos */
demoPrototype.prototype.saludo = "saludo!";

/* instanciando demoPrototype */
var test1 = new demoPrototype();
var test2 = new demoPrototype();
/* ambos objetos contienen la misma propiedad saludo que fue definida en el prototype de demoPrototype */
test1.saludo
test2.saludo
```
#### Object.create
Crea un objeto que tiene un prototipo especificado y opcionalmente contiene propiedades especificas, tambien nos permite implementar facilmente el concepto de la herencia diferencial donde los objetos son capaces de heredar directamente de otros objetos.

Como tambien nos permite inicializar las propiedades del objeto utilizando el segundo parametro.Por ejemplo:
```js
var Persona = {
  getNombre : function(){
    console.log("mi nombre es "+this.nombre);
  }
};

var pedro = Object.create(Persona,{
  nombre:{
      value:"pedro"
    }
});

pedro.getNombre();
```
Podemos usar el patron prototype sin utilizar directamente el
```Object.create ```, simulando el patron de acuerdo con el ejemplo anterior seria asi:
```js
var personaPrototype = {
  init:function(nombre){
    this.nombre = nombre;
  },
  getNombre : function(){
    console.log("mi nombre es "+this.nombre);
  }
};

function Persona(nombre){
  function P(){};
  P.prototype = personaPrototype;
  var f = new P();
  f.init(nombre);
  return f;
};

var pedro = Persona("pedro");
pedro.getNombre();
```
Otra forma de implementación del patron prototype:
```js
var vehiculoEsqueleto = function(){
  this.getTipo = function(){
    console.log("Tipo de vehiculo: "+this.tipo)
  };

  this.getMarca = function(){
    console.log("Marca de vehiculo: "+this.marca)
  };
};

var vehiculo = function(tipo,marca){
  this.tipo=tipo;
  this.marca=marca;
};

vehiculo.prototype = new vehiculoEsqueleto();

var testVehiculo = new vehiculo("terrestre","audi");
testVehiculo.getTipo();
testVehiculo.getMarca();
```
