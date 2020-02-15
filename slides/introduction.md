### Introducción: Herramientas

En esta sección vamos a partir de un código fuente muy sencillo y vamos a 
añadirle diversas herramientas para mejorar la calidad del mismo.

^^^^^^

#### Introducción: Herramientas

El objetivo de la integración de estas herramientas dentro de nuestro sistema de 
integración / despliegue contínuo es la

**automatización de su uso**

notes:

Lo que se pretende es que sean el sistema el que haga todas estas comprobaciones de manera 
automática. Buscamos evitar que los miembros del equipo tengan que estar pendientes de 
ejecutar todas estas herramientas cada vez que quieren subir código al repositorio. 

^^^^^^

#### Introducción: Herramientas

* DOxygen: sistema de auto-documentación de código
* Cppcheck: Análisis estático de código
* Warnings Plugin - Next Generation: muestra los warnings de nuestro código
* Cppunit: Test unitarios
* Gcov: Cobertura de tests
* Gprof: Profiling

^^^^^^

#### Introducción: Tarea de estilo libre

Para instalar y probar las herramientas que usamos en esta sección, necesitaremos una 
tarea de estilo libre.

Repositorio: https://github.com/Be-Core-Code/curso-intro-jenkins-modulo-6-sample-repository-with-c-code.git

^^^^^^

#### Introducción: Tarea de estilo libre

![Create Free Style Job Step 1](/slides/images/create_freestyle_job_step_1.png)

^^^^^^

#### Introducción: Tarea de estilo libre

![Create Free Style Job Step 2](/slides/images/create_freestyle_job_step_2.png)

^^^^^^

#### Introducción: Tarea de estilo libre

![Create Free Style Job Step 3](/slides/images/create_freestyle_job_step_3.png)

^^^^^^

#### Introducción: Tarea de estilo libre

![Create Free Style Job Step 4](/slides/images/create_freestyle_job_step_4.png)


^^^^^^

#### Introducción: Tarea de estilo libre

Creamos el proyecto que usaremos en el resto de las secciones