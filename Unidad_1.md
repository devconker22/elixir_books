# ¿Qué es Elixir?
Podríamos definir Elixir como un lenguaje funcional con capacidad de
meta-programación. La mayor parte del lenguaje Elixir está definido en
Elixir. El lenguaje permite construcciones muy flexibles como veremos a
lo largo de los siguientes capítulos.

# Características de Elixir
Para definir Elixir hemos nombrado muchas de las características de que
dispone el lenguaje. En este sentido me gustaría separar lo que nos
permite realizar el lenguaje de lo que nos permite realizar su máquina
virtual (BEAM) y es común a todos los lenguajes compilados y que se
ejecutan sobre ella.

## Características de BEAM
Comenzando desde la base podemos decir que BEAM es una máquina
virtual desarrollada y mantenida en producción por muchas empresas
desde hace muchos años.

### Tolerancia a fallos
El código se aisla completamente en unidades mínimas de
ejecución llamadas procesos. Un proceso es iniciado y debido a
un fallo puede ser terminado. Al mantener cada proceso aislado
y sin memoria compartida BEAM nos garantiza la consistencia en
la memoria interna de cada uno de los procesos no afectados
por el error. 

### Alto Nivel de Concurrencia
Al no existir memoria compartida los recursos no son compartidos
en ningún momento. El modelo de protección de sección crítica
se basa en mantener la unidad de ejecución conjutamente con
los datos que maneja y ningún otro código puede acceder a esa
información directamente. 

### Alta Capacidad
BEAM define unos procesos internos mucho más ligeros que
los proporcionados por el sistema operativo. Esto nos permite
generar tantos procesos como necesitemos. De hecho la mayoría de
sistemas operativos limita el número de procesos a 65536 (16 bits)
mientras que los procesos que pueden ser creados en BEAM son
un poco más de 134 millones.

### Tiempo Real Blando
Al no contener memoria compartida el recolector de basura de
BEAM no necesita bloquear ningún proceso para poder actuar.
Esto se traduce en la eliminación de cortes en el funcionamiento
normal de la máquina virtual y poder trabajar en tiempo real
blando. 

### Actualización en Caliente
BEAM es de las únicas máquinas virtuales que dispone de un
sistema seguro para el cambio de código en caliente. Permite
modificar el código de un módulo aún manteniendo una copia antigua para los procesos que aún se mantienen en ejecución e ir
migrando de forma segura a la nueva versión del módulo sin tirar
el sistema.

## Características de Elixir
En la definición adelantamos muchas de las características de Elixir como
lenguaje. Una de sus grandes potencias es la meta-programación que
nos ayuda a evitar repetir una y otra vez los mismos códigos y reduce
al mínimo las típicas plantillas de código a completar cuando se usan
frameworks.

### Lenguaje Dinámico
Es de tipado dinámico y no es fuertemente tipado. Los tipos
son opcionales y con fines de comprobación y documentación. Al
igual que en Erlang podemos definirlos como una especificación
adicional. Veremos esto más adelante.




### Productividad
Al escribir código que genera código permite eliminar la necesidad
de escribir muchas partes repetitivas y agregar construcciones
específicas en lógica de negocio facilitándonos y reduciendo la
generación de código. 

### Extensibilidad
A través de la definición de macros, guardas, funciones, sigilos
y sobretodo protocolos nos permite agregar muchas más
construcciones al lenguaje. 

### Concurrencia
Dada por BEAM. A través de comportamientos definidos desde la
base a través de OTP el lenguaje construye elementos permitiendo
mantener la base de paso de mensajes, mantener la sección crítica
y facilitar la generación de miles y millones de procesos.

# Historia de BEAM
Joe Armstrong asistió a la conferencia de Erlang Factory de Londres, en
2010, donde explicó la historia de la máquina virtual de Erlang. En sí,
es la propia historia de Erlang/OTP. La idea de Erlang surgió por la necesidad de Ericsson de acotar un
problema que había surgido en su plataforma AXE, que estaba siendo
desarrollada en PLEX, un lenguaje propietario.

# Comenzando la idea de Elixir
El nombre de Elixir no tiene un origen definido. José Valim dijo en la
Elixir Conf de 2014 que no tuvo una razón específica para elegir el
nombre. No obstante y gracias a su símil con la mezcla de elementos para
la fabricación de elixires los programadores se atribuyen el nombre de
alquimistas, la herramienta de construcción el nombre de mix (mezclar) y
el gestor de paquetes hex (maleficio). Además del nombre de conocidas
librerías como poison (veneno) para el tratamiento de JSON o distillery
(destilería) para el empaquetado de un lanzamiento.


# Desarrollos con Elixir
A nivel empresarial Elixir es usado por empresas tan grandes como
Adobe, AdRoll, Lexmark, PagerDuty, Pinterest o Slack.
Dado su origen el principal uso de Elixir está en la elaboración de
servicios web y websocket para servicios en Internet. Uno de los
grandes frameworks que posibilita y facilita esta adopción es Phoenix
Framework.

