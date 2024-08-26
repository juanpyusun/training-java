```java
//1.se puede usar solo el if
if (condicion){
	//En este bloque va todo el codigo si condicion es verdadera
}

//2.se puede usar tambien el if-else, si la condicion es verdadera entra al if, si es falsa entra al bloque del else
if (condicion){
	//En este bloque va todo el codigo si condicion es verdadera
}
else{
	//En este bloque va todo el codigo si condicion es falsa
}

//3.Tambien podemos usar if-else if-else, si la condicion es falsa, va al else if y vuelve a preguntar, y asi sucesivamente sigue  preguntando en varios else if, si no cumple en ninguno entra al else
if (condicion1){
	//En este bloque va todo el codigo si condicion1 es verdadera
}
else if (condicion2){
	//En este bloque va todo el codigo si condicion2 es verdadera
}
else if (condicion3){
	//En este bloque va todo el codigo si condicion3 es verdadera
}
else if (condicion4){
	//En este bloque va todo el codigo si condicion4 es verdadera
}
else if(condicion5){
	//En este bloque va todo el codigo si condicion5 es verdadera
}
else{
	//En este bloque va todo el codigo si ninguna de las anteriores condiciones es verdadera
}

//4.por otro lado tenemos el if de una linea o tambien llamado operador ternario
String mensaje;
boolean condicion = true;

mensaje = (condicion) ? "aqui va el mensaje o valor numerico si la condicion es verdadera" : "aqui va el mensaje o valor numerico si la condicion es falsa";

//5.Por otro lado tenemos la estructura switch

char letra = 'a';

switch(letra){
	case 'a':
		System.out.println("primera letra del abecedario");
	break;

	case 'b':
		System.out.println("segunda letra del abecedario");
	break;

	case 'c':
		System.out.println("tercera letra del abecedario");
	break;

	default:
		System.out.println("Ud no escogio ninguna letra del abecedario");
	break;
}        
```