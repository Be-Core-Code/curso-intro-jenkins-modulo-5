### Análisis estático de código: CppCheck

CppCheck es un analizador estátido de código:

* Dead pointers
* Division by zero
* Integer overflows
* Invalid bit shift operands
* y más...

[Ir al proyecto](http://cppcheck.sourceforge.net)

^^^^^^

### CppCheck

El [código del ejemplo](https://github.com/Be-Core-Code/curso-intro-jenkins-modulo-6-sample-repository-with-c-code.git)
contiene una función que CppCheck detecta como errónea y dará un error.

^^^^^^

### CppCheck

Instalar la herramienta:

```bash
> sudo apt install cppcheck
```

^^^^^^

### CppCheck

Verificar que funciona:

```bash
ejemplo-modulo-6 > cppcheck main.c
Checking main.c ...
[main.c:94]: (error) Array 'stack[20]' accessed at index 20, which is out of bounds.
ejemplo-modulo-6 >
```

^^^^^^

### CppCheck: Instalar el plugin

![cppcheck_plugin_installation_step_1](/slides/images/cppcheck_plugin_installation_step_1.png)

^^^^^^

### CppCheck: Configuración global

Este Plugin no requiere de una configuración global como ocurría con DOxygen.

^^^^^^

### CppCheck: Añadir paso para generar el informe

![cppcheck_add_step_to_job_step_1](/slides/images/cppcheck_add_step_to_job_step_1.png)

^^^^^^

### CppCheck: Añadir paso para generar el informe

![cppcheck_add_step_to_job_step_2](/slides/images/cppcheck_add_step_to_job_step_2.png)

notes:

Si miras [el repositorio](https://github.com/Be-Core-Code/curso-intro-jenkins-modulo-6-sample-repository-with-c-code.git)
podrás ver que en `Makefile` del mismo se crearon las siguientes tareas para correr `cppcheck`

```Makefile
cppcheck-xml :
        cppcheck *.c --xml --xml-version=2 --enable=all --inconclusive --language=c *.c 2>reports/cppcheck/report.xml
cppcheck : 
        cppcheck *.c --enable=all --inconclusive --language=c *.c

```

En particular, la tarea `cppcheck-xml` genera un informe en formato XML que es el que usaremos
en el siguiente paso para obtener el informe.

^^^^^^

### CppCheck: Añadir paso para generar el informe

Añadimos una acción para ejecutar después:

![cppcheck_add_step_to_job_step_3-1](/slides/images/cppcheck_add_step_to_job_step_3-1.png)

^^^^^^

### CppCheck: Añadir paso para generar el informe

![cppcheck_add_step_to_job_step_4](/slides/images/cppcheck_add_step_to_job_step_3-2.png)

notes:

En este paso ponemos la ruta del fichero con el informe que hemos utilizado en la tarea `cppcheck-xml` del 
[`Makefile`](https://github.com/Be-Core-Code/curso-intro-jenkins-modulo-6-sample-repository-with-c-code/blob/master/Makefile)


^^^^^^

### CppCheck: Añadir paso para generar el informe

En las opciones avanzadas
![cppcheck_add_step_to_job_step_3-2](/slides/images/cppcheck_add_step_to_job_step_3-3.png)

notes:

Al poner un umbral de 0, la ejecución fallará cuando haya al menos un error o warning en 
cppcheck.

^^^^^^

#### CppCheck: Añadir paso para generar el informe

⚠️ ¡Atención! Si estamos ejecutando Jenkins sobre Java 11, veremos el siguiente error en
el log de la ejecución:

![cppcheck_job_error_with_java_11](/slides/images/cppcheck_add_step_to_job_error_with_java_11.png)<!-- .element: style="height: 45vh " -->

^^^^^^

### CppCheck: Añadir paso para generar el informe

Para instalar Java 8:

```bash 
> sudo apt install openjdk-8-jdk
> sudo update-alternatives --config java
> sudo systemctl restart jenkins
```

Una vez reiniciado, lanzar una nueva ejecución...

^^^^^^

#### CppCheck: Añadir paso para generar el informe

Si no ponemos ningún umbral, la ejecución no fallará a pesar de que se generen errores en cppcheck:

![cppcheck_results](/slides/images/cppcheck_add_step_to_job_cppcheck_results_without_threshold.png)<!-- .element: style="height: 45vh " -->

^^^^^^

#### CppCheck: Añadir paso para generar el informe

Si ponemos un umbral, la ejecución será inestable cuando se generen errores en cppcheck:

![cppcheck_results](/slides/images/cppcheck_add_step_to_job_cppcheck_results_with_threshold.png)<!-- .element: style="height: 45vh " -->

^^^^^^

### CppCheck

[Página del Plugin](https://plugins.jenkins.io/cppcheck/)
