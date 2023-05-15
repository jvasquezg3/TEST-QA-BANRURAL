PLAN DE ATAQUE
1. Se definen los requisitos
2. Proceso de testeo de las funcionalidades (ejecución)
3. Analisis y corrección de los defectos o errores encontrados.
4. Nueva ejecución de pruebas para determinar que no hayan más defectos.
5. Cierre de las pruebas.

****************************************************************************************************************************************

REQUISITOS:

En base a los siguientes requisitos, se procede con las pruebas correspondientes.

1. El número a adivinar debe pertenecer al conjunto de los enteros (e.g. 1, 2, 3...)
2. El número que ingresará el jugador debe pertenecer al conjunto de los enteros (e.g. 1, 2, 3...), en caso que no ingrese un número entero, debe mostrarse una alerta al usuario y no se debe incrementar un intento de prueba.
3. Sí el número que ingresó el jugador es mayor al número a adivinar, se debe mostrar el siguiente mensaje en color negro: "Incorrecto! El número es mayor!", en caso que sea menor, se debe mostrar: "Incorrecto! El número es menor!".
4. Si después de 10 intentos, el usuario no adivina el número, se debe mostrarse el mensaje de color rojo: "!!!Pérdistes!!!"
5. Si el usuario adivina el número antes de los 10 intentos, se debe mostrar el mensaje de color verde: "Felicitaciones! adivinaste el número!".


****************************************************************************************************************************************
TESTEO DEL PROYECTO

Se corre el proyecto para iniciar con la verificación.

Al intentar utilizar el proyecto se valida que el botón Ingresar número aleatorio no funiciona.
Se procede a abrir la consola del navegador y en efecto muestra un error.

0001 Error: Uncaught TypeError: guessSubmit.addeventListener is not a function at index.html:87:15
Verificación: error de sintaxis línea 87. 
Actualmente se encuentra de la siguiente forma: guessSubmit.addeventListener('click', checkGuess);
Solución: se agrego mayúscula en método: guessSubmit.addEventListener('click', checkGuess);

0002 Error:Uncaught TypeError: Cannot set properties of null (setting 'textContent') at HTMLInputElement.checkGuess (index.html:77:29)
Verificación: Ser valida el error, sin embargo, la línea 77 se encuentra bien, el error se encuentra en la declaración de la línea 49, definición de constantes.
Actualmente esta definido como: const lowOrHi = document.querySelector('lowOrHi');
Solución: se agrego el punto faltante const lowOrHi = document.querySelector('.lowOrHi'); 

**Una vez solucionado las funcionalidades principales la cual permite el uso del botón e iniciar con el ingreso de los números se muestra que los colores de los mensajes no corresponden a lo establecido en los requisitos, estos no muestran ninguna descripción de error.

0003 Error: Color establecido cuando el número es incorrecto, línea 75 no corresponde a los requisitos.
Actualmente muestra color verde: lastResult.style.backgroundColor = 'green';
Solución: colocar color negro: lastResult.style.backgroundColor = 'black';

0004 Error: Validación de intentos, los requisitos indican que deben ser 10 intentos, mientras que el programa tiene establecido 5.
Actualmente tiene declarado 5 intentos, dentro de la constante: const ATTEMPS = 5; línea 46, la cual afecta la línea 69 al momento de la ejecución en else if(guessCount === ATTEMPS),.
Solución: se cambia el valor de la contante de 5 a 10, const ATTEMPS = 10; para cumplir con los 10 intentos establecidos en los requisito (punto 4).

0005 Error: frase no corresponde a la respuesta establecida cuando el usuario no adivina el número despues de los 10 intentos, línea 70.
Actualmente muestra la frase: lastResult.textContent = 'Felicitaciones! adivinaste el número!';
Solución: cambio de la descripción de la frase: lastResult.textContent = '!!!Pérdistes!!!';

0006 Error: Botón "Comienza un juego nuevo" no funciona, Uncaught TypeError: guessSubmit.addeventListener is not a function at index html:95.
Verificació: error de sintaxis línea 95.
Actualmente envían el método de la siguiente forma: resetButton.addeventListener('click', resetGame);
Solución: se agrego mayúscula en método: resetButton.addEventListener('click', resetGame);

Se corrigen las funcionalidades de las respuestas al momento de colocar un número incorrecto y perder, como también iniciar un nuevo juego.

****************************************************************************************************************************************

Se procede con la validación de la funcionalidad de adivinar el número, este no genera ningún tipo de error, sin embargo, se detecta que se genera un random entre un rango de 1 a 10 números, se valida la variable randomNumber en la línea 44 y se verifica que el método Math.random() * 10; que se utiliza genera un random entre 0 a 10 pero utilizando decimales no son enteros, a lo que indica los requisitos que debe ser entre un rango de 1 a 100 utilizando enteros.

0007 Error: declaración en el Método Math.random(); 
Actualmente lo envían de la siguiente manera: Math.random() * 10; Esta estructura se utiliza para devolver un número entre 0 a 10 pero con punto decimal.
Solución: let randomNumber = Math.floor(Math.random() * 100) + 1; Se coloca floor, ya que este permite devolver enteros, y se coloca +1 para que inicie desde 1 a 100

0008 Error: Falta definir que tipo de variable recibe guessField.value línea 58.
Actualmente se envía let userGuess = guessField.value;
Solución: let userGuess = Number(guessField.value); se define como number para convertir lo que ingrese en el inputo a tipo numerico.

0009 Error: declaración en el método Math.random(); lína 114.
Actualmente lo envían así: randomNumber = Math.floor(Math.random()) + 1; falta definir el rango, ya que al resetear el juego solamente toma el uno como el número a adivinar
Solución: randomNumber = Math.floor(Math.random() * 100) + 1; 

0010 Error: frase no corresponde a la respuesta establecida cuando el usuario SI adivina el número antes de 10 intentos, línea 76.
Actualmente muestra la frase: lastResult.textContent = '!!!Pérdistes!!!';
Solución: cambio de la descripción de la frase: lastResult.textContent = 'Felicitaciones! adivinaste el número!';

0011 Error: Color establecido cuando el número es incorrecto, línea 66 no corresponde a los requisitos.
Actualmente envían: lastResult.style.backgroundColor = 'black'; lo establecido en los requisitos debe ser color verde 
Solución: lastResult.style.backgroundColor = 'green'; se agrega color verde a la respuesta al momento de ganar.

****************************************************************************************************************************************

Para cumplir con el requisito establecido en el punto 1 y 2 se crea una validación con expresión regular para identificar si es entero y si fuera diferente a enteros genere una alerta sin
incrementar un intento de prueba

0012 Se crea una validación para que permita aceptar solo números enteros y al momento de ingresar un decimal muestre una alerta sin incrementar los intentos, esta validación también aplica
para el rango de números a ingresar que va de 1 a 100.
 
const regexEntero = /^\d+$/;

  // Verifica si es un número entero y si cumple con el rango
   if (!regexEntero.test(userGuess)) {
    alert("Solo se aceptan números enteros");
    guessField.value = "";
    return;
   } else if(userGuess < 1 || userGuess > 100){
    alert("Rango aceptado de 1 a 100");
    guessField.value = "";
    return;
   }

0013 Para que el programa acepte únicamente valores númericos se  relizo un cambio en el valor de tipo de entra de text a number en el html, línea 31, para evitar ingreso de otros caracteres.
<input type="number"

****************************************************************************************************************************************

Con el testeo de estas pruebas permitió validar las funcionalidades del sistema en base a lo establecido en los requisitos y así mimso al corregir los defectos encontrados el programa funciona de acuerdo a los requisitos establecidos.

