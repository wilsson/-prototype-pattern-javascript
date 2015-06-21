PATRON PROTOTYPE 
===================
Continuando la saga de los post sobre patrones de diseño en javaScript, en este hablaremos del patron prototype.

Del patron prototype podemos decir que se centra en la creación de objetos que atúan como prototipos para otros objetos, através de la herencia de prototipos.

La herencia de prototipos evita el uso de clases por completo, ventaja la cual podemos encontrar nativamente atraves de prototipos en lugar de tratar de imitar caracteristicas de otros lenguajes.

La real herencia de prototipos, es definida por el estandar ECMAScript 5, la cual requiere el uso de 'Object.create'.

'Object.create' crea un objeto que tiene un prototipo especificado y opcionalmente contiene propiedades especificas.


```js Object.create``` tambien nos permite implementar facilmente el concepto de la herencia diferencial donde los objetos son capaces de heredar directamente de otros objetos.
```js Object.create``` nos permite inicializar las propiedades del objeto utilizando el segundo parametro.Por ejemplo:
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

pedro.getNombre()
```
Podemos usar el patron prototype sin utilizar directamente el
```js Object.create ```, simulando el patron de acuerdo con el ejemplo anterior seria asi:
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