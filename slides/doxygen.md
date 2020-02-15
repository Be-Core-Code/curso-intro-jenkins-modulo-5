### DOxygen

Generar documentación para nuestro código.

^^^^^^

#### DOxygen

Instalamos la herramienta en el maestro:

```bash
> sudo apt install doxygen graphviz
...
> doxygen --version
1.8.13
> 
```

^^^^^^

#### DOxygen

Clonar [el repositorio](https://github.com/Be-Core-Code/curso-intro-jenkins-modulo-6-sample-repository-with-c-code.git)
si no lo has clonado todavía.

^^^^^^

#### DOxygen

Generar la documentación para verificar que la instalación de DOxygen funciona correctamente

```bash
> doxygen
...
Generating alphabetical compound index...
Generating hierarchical class index...
Generating graphical class hierarchy...
Generating member index...
Generating file index...
Generating file member index...
Generating example index...
finalizing index lists...
writing tag file...
Running dot...
lookup cache used 7/65536 hits=9 misses=7
finished...
``` 
^^^^^^

#### DOxygen

![doxygen_main_c_file_documentation](/slides/images/doxygen_main_c_file_documentation.png)

^^^^^^

#### DOxygen: Instalar el plugin de DOxygen

![doxygen_plugin_installation_step_1](/slides/images/doxygen_plugin_installation_step_1.png)

^^^^^^

#### DOxygen: Configuración global

Ir a "Jenkins" -> "Global Tool Configuration"

![Global DOxygen Configuration](/slides/images/global_doxygen_configuration.png)

^^^^^^

#### DOxygen: Añadir paso para generar la documentación

Ir a la configuración de la tarea `modulo-6`

![doxygen_add_step_to_job_step_1](/slides/images/doxygen_add_step_to_job_step_1.png)

^^^^^^

#### DOxygen: Añadir paso para generar la documentación

![doxygen_add_step_to_job_step_2](/slides/images/doxygen_add_step_to_job_step_2.png)


^^^^^^

#### DOxygen: Añadir paso para generar la documentación

Añadimos una acción para ejecutar después:

![doxygen_add_step_to_job_step_3](/slides/images/doxygen_add_step_to_job_step_3.png)

^^^^^^

#### DOxygen: Añadir paso para generar la documentación

Añadimos una acción para ejecutar después:

![doxygen_add_step_to_job_step_4](/slides/images/doxygen_add_step_to_job_step_4.png)

^^^^^^

#### DOxygen: Añadir paso para generar la documentación

Lanzamos una ejecución de la tarea y...

![doxygen_view_build_generated_documentation](/slides/images/doxygen_view_build_generated_documentation.png)

