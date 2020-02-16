### CMocka: Tests Unitarios en C

Para demostrar cómo ejecutar los tests y mostrar los resultados en Jenkins,
usaremos [`CMocka`](https://cmocka.org)

notes:

¿Porqué hemos seleccionado este framework de testing en C? Los motivos han sido prácticos y pedagógicos principalmente:

* Es un framework utilizado en varios proyectos de software libre de renombre como puede ser Samba o Open VPN
* Genera directamente la salida en un formato XML que jenkins entiende. Cppunit requiere transformar el XML para que
  Jenkins lo pueda leer
* Es sencillo de utilizar e integrar en el código que usamos en los ejemplos, lo que hace que no
  tengamos que dedicarle demasiado tiempo a pensar en CMocka y dediquemos nuestra energía a ver cómo
  integrarlo en Jenkins, que es el objetivo de este curso.
  
En el [este enlace](https://stackoverflow.com/a/65845) tienes una lista con varios otros frameworks que puedes investigar.

^^^^^^

#### CMocka: Tests Unitarios en C

[El repositorio de ejemplo](https://github.com/Be-Core-Code/curso-intro-jenkins-modulo-6-sample-repository-with-c-code.git) 
ya tiene creados dos sencillos test unitarios de la función `is_armstrong_number`.

Para poder correrlos necesitamos hacer los siguiente:

```bash
> sudo apt install libcmocka-dev libcmocka0
> make tests
```
^^^^^^
#### CMocka: Instalar el plugin

No hace falta instalar el plugin, sólo ejecutar los tests y exportar los resultados en el
formato adecuado:

```Makefile
tests-xml: clean armstrong.o stack.o
        gcc tests/test_is_armstrong_number.c armstrong.o stack.o -lm -lcmocka -o tests/build/test_is_armstrong_number
        CMOCKA_XML_FILE=reports/cmocka/%g.xml CMOCKA_MESSAGE_OUTPUT=xml ./tests/build/test_is_armstrong_number
```

^^^^^^

#### CMocka: Añadir paso para ejecutar los tests

![Add make tests-xml step](/slides/images/cmocka_add_step_to_job_step_1.png)

notes:

Si miras [el repositorio](https://github.com/Be-Core-Code/curso-intro-jenkins-modulo-6-sample-repository-with-c-code.git)
podrás ver que en `Makefile` del mismo se crearon las siguientes tareas para correr `cmocka`

```Makefile
tests: clean armstrong.o stack.o
        gcc tests/test_is_armstrong_number.c armstrong.o stack.o -lm -lcmocka -o tests/build/test_is_armstrong_number
        CMOCKA_MESSAGE_OUTPUT=stdout CMOCKA_XML_FILE='' ./tests/build/test_is_armstrong_number

tests-xml: clean armstrong.o stack.o
        gcc tests/test_is_armstrong_number.c armstrong.o stack.o -lm -lcmocka -o tests/build/test_is_armstrong_number
        CMOCKA_XML_FILE=reports/cmocka/%g.xml CMOCKA_MESSAGE_OUTPUT=xml ./tests/build/test_is_armstrong_number
```

En este paso utilizamos la tarea tests-xml.

^^^^^^

#### CMocka: Añadir acción para ejecutar después

![add post action](/slides/images/cmocka_add_step_to_job_step_2.png)

^^^^^^

#### CMocka: Añadir acción para ejecutar después

![add post action](/slides/images/cmocka_add_step_to_job_step_3.png)

^^^^^^

#### CMocka: Resultados

![cmocka_results](/slides/images/cmocka_results_build_status_page.png)


notes:

En este caso, vemos que los tests están pasando y no se ha producido errores. Haciendo click sobre
podremos ver el detalle de los tests.

Una nota adicional sobre esta captura de pantalla. Mientras preparaba las diapositivas para este módulo,
a medida que iba añadiendo las diferentes herramientas al proyecto (docygen, cppcheck, warnings y cmocka)
he ido añadiendo pasos a la tarea de Jenkins y refactorizando el código fuente. Puedes ver todas
estas refactorizaciones mirando [la historia del repositorio](https://github.com/Be-Core-Code/curso-intro-jenkins-modulo-6-sample-repository-with-c-code/commits/master).

En esta diapositiva se puede observar, además de que los tests están pasando, 
**que los cambios introducidos en el código han resuelto todos los warnings que estaba
dando cppcheck** y mejorando con ello la calidad de nuestro código:

![cppcheck warnings fixed](/slides/images/cmocka_results_build_status_page_cppcheck.png)
 

