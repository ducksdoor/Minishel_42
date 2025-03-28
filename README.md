# Minishel_42

-Aqui dejo una pequeña muy pequeña busqueda de informacion que hice en su momento, busque mas y me volvi un poco loco pero bueno, como lo escribí me da pena borrarlo, si ha alguien le es util seria estupendo

## Redirecciones del proyecto

# >
	1: Redirección de salida estándar (stdout): >
	
		Descripción: Redirige la salida de un comando hacia un archivo. Si el archivo no existe, se crea. Si el archivo ya existe, se sobrescribe.

		Sintaxis:
			comando > archivo.txt

# >>
	2: Redirección de salida estándar (stdout) en modo de anexado: >>

		Descripción: Redirige la salida de un comando hacia un archivo, pero anexa la salida al final del archivo si ya existe (no sobrescribe).

		Sintaxis:
			comando >> archivo.txt

# <
	3: Redirección de entrada estándar (stdin): <

	Descripción: Toma la entrada desde un archivo en lugar de desde el teclado.

	Sintaxis:
		comando < archivo.txt

# <<
	4: Here dock: <<

	Descripcion: Permite redirigir múltiples líneas de texto directamente como entrada estándar a un comando, sin tener que escribirlas manualmente o desde un archivo.

	Sintaxis:
		comando >> archivo.txt

Hay mas redirecciones de las cuales no hay que hacer caso para este proyecto

Redirección de error estándar (stderr): 2>
Redirección de error estándar (stderr) en modo de anexado: 2>>
Redirección de salida estándar (stdout) y error estándar (stderr) a un mismo archivo: &>
Redirección de salida estándar (stdout) y error estándar (stderr) a un mismo archivo en modo de anexado: &>>
Descarte de salida: > /dev/null o 2> /dev/null

Como funcionan las redirecciones, da igual la cantidad de > o de < que le metas, solo tiene que ejecutar la ultima. Ademas da igual el orden, va a leer antes de escribir, tecnicamente ejecuta todas.... pero sobre escribe la ultima
con heredock tienes que escribir por orden los heredock por los que va a ir avanzando y sobreescribe a partir de que entre en el ultimo. 

## Referente a $? 

Según la salida, el echo $? tiene que devolver un numero distinto, aqui hay unos ejemplos.

0: El comando se ejecutó correctamente sin errores.

1: Generalmente indica un error general. Puede ser usado para muchas situaciones en las que no hay un código de error más específico.

127: Este valor significa que el comando no se encontró (generalmente cuando intentas ejecutar un comando que no existe o no está instalado en tu sistema).

126: Se usa cuando el comando no tiene permisos para ejecutarse. Es decir, la terminal no tiene permisos de ejecución para ese archivo.

2: Suele indicar un error de sintaxis en el comando, como una opción no válida.

128: Este valor se usa cuando un proceso se termina con una señal específica, como un kill o un comando similar. También se utiliza para indicar errores relacionados con señales, como una interrupción del proceso por una señal.

130: Se utiliza cuando un proceso es interrumpido por un Ctrl+C.

137: Este valor suele indicar que el proceso fue terminado por una señal de terminación, como kill -9.

255: Indica un error grave. A menudo se asocia con la salida de programas que terminan con errores de ejecución no esperados.

En primer lugar tenemos que comprender que hacen todas las funciones que nos permiten usar, seguramente no usemos todas, pero siempre es un buen punto para empezar:

1 Estas ya han sido usadas en otros proyectos anteriores.
printf, malloc, free, write, access, open, read, close, fork, wait, waitpid, wait3, wait4, execve, dup, dup2, pipe, perror, exit, kill,

#### Libreria ####
#include <readline/readline.h>
#include <readline/history.h>

## readline ##
Se utiliza comúnmente para leer líneas de texto desde la entrada estándar o desde un archivo. Esta función facilita la lectura de líneas de manera interactiva, ya que maneja la entrada del usuario, realiza el seguimiento del historial de comandos y proporciona la capacidad de editar líneas de texto.

## rl_clear_history ##
La función rl_clear_history borra todo el historial almacenado hasta el momento en que se llama. Después de llamar a esta función, el historial estará vacío.

## rl_on_new_line ##
Esta función se utiliza para indicar a Readline que el cursor ha cambiado a una nueva línea y que cualquier proceso en segundo plano (background job) que se estaba ejecutando debe suspenderse. Específicamente, rl_on_new_line se encarga de realizar las acciones necesarias cuando se detecta que la aplicación ha impreso un carácter de nueva línea ('\n').

## rl_replace_line ##


## rl_redisplay ## 


## add_history ##
Añade una linea al historial.


#### Libreria ####
#include <signal.h>

## signal ## --No me termino de enterar de como funciona--
En el lenguaje de programación C, la función signal se utiliza para manejar señales del sistema. Las señales son eventos asíncronos que pueden ser generados por el sistema operativo o por otros procesos. Estas señales pueden indicar eventos como la terminación de un proceso, la recepción de una interrupción de teclado (por ejemplo, Ctrl+C), entre otros.
El prototipo de la función es:
### void (*signal(int signum, void (*handler)(int)))(int); ###
	signum: Es el número de la señal que se desea manejar.
	handler: Es un puntero a la función que manejará la señal. 
La función devuelve un puntero a la función anterior que manejaba la señal, o SIG_ERR en caso de error.

## sigaction ##
La función sigaction en el lenguaje de programación C se utiliza para establecer y modificar las acciones asociadas a una señal específica. A diferencia de la función signal que tiene una interfaz más simple, sigaction proporciona un control más detallado sobre cómo se manejan las señales.
el prototipo sería:
### int sigaction(int signum, const struct sigaction *act, struct sigaction *oldact); ###
	signum: Es el número de la señal que se desea manejar.
	act: Es un puntero a una estructura struct sigaction que contiene información sobre la nueva acción a tomar cuando se recibe la señal.
	oldact: Es un puntero a una estructura struct sigaction que, si no es NULL, se llena con información sobre la acción anterior que estaba asociada a la señal.
	La extructura sigaction tiene varios datos, los mas importantes son:
		struct sigaction {
    	void     (*sa_handler)(int);
    	void     (*sa_sigaction)(int, siginfo_t *, void *);
    	sigset_t   sa_mask;
    	int        sa_flags;
    	void     (*sa_restorer)(void);
		};
			sa_handler: Puntero a la función de manejo de la señal. Es la alternativa al uso de funciones de manejo directo en signal. Ambos no deben especificarse simultáneamente.
			sa_sigaction: Puntero a una función de manejo extendida que puede tener acceso a información adicional sobre la señal.
			sa_mask: Un conjunto de señales adicionales que se bloquearán durante la ejecución del manejador de señales.
			sa_flags: Varios indicadores que controlan el comportamiento de la señal.
			sa_restorer: Puntero a una función utilizada por algunas arquitecturas y sistemas operativos específicos.



#### Libreria ####
#include <unistd.h>

## getcwd ##
se utiliza para obtener el nombre del directorio de trabajo actual (current working directory, cwd) y almacenarlo en un búfer proporcionado por el usuario.
### char *getcwd(char *buf, size_t size); ###
	buf: Es un puntero al búfer donde se almacenará el nombre del directorio de trabajo actual.
	size: Es el tamaño del búfer proporcionado por el usuario (buf).
	La función devuelve un puntero al búfer que contiene el nombre del directorio de trabajo actual, o NULL en caso de error.

## chdir ##
se utiliza para cambiar el directorio de trabajo actual. El directorio de trabajo actual es el directorio en el sistema de archivos desde el cual se ejecutan las rutas relativas.
### int chdir(const char *path); ###
	path: Es una cadena que especifica la ruta del directorio al cual se desea cambiar. La función devuelve 0 si tiene éxito y -1 en caso de error.


#### Libreria ####
#include <sys/stat.h>

## stat ##






lstat, fstat, unlink, 
opendir, readdir, closedir, strerror, 
isatty, ttyname, ttyslot, ioctl, getenv, tcsetattr,
tcgetattr, tgetent, tgetflag, tgetnum, tgetstr,
tgoto, tputs
