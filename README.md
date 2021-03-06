# DVSwitch & APPMobile
Creación de DVSwitch Server en Oracle Cloud (VPS Gratuito) y DVSwitch Mobile para radioaficionados.

## Requisitos Previos
Para seguir correctamente esta guía será necesario estar en posesión de algún servidor VPS cloud de pago o parcialmente gratuito como el que se ofrece en este tutorial. En el registro para la obtención de esta versión gratuita de Oracle Cloud será imprescindible tener una tarjeta bancaria para la autenticación de ser una persona física.

**Será necesario tener una licencia vigente de radioaficionado.**

## Creación de una instancia en Oracle Cloud

Entramos en nuestra cuenta de Oracle Cloud y nos dirigimos al menú de nuestra banda izquierda, este es posible desplegarlo mediante el icono con tres línes horizontales, nos dirigimos al apartado de **Recursos informáticos > Instancia**.

<p align="center">
	<img src="https://user-images.githubusercontent.com/104928044/169712856-42d9e12a-dd8c-4329-93fa-98e44ca0ca45.png"
		alt="Panel Instancias"
	style="float: left; margin-right: 10px;" />
</p>

Nos cambiará de ventana e iremos a un menú donde aparecerá un botón de color azul en que nos dirá **Crear instancia**.

<p align="center">
	<img src="https://user-images.githubusercontent.com/104928044/169713055-478d6dea-0cb8-410e-b014-4ab5045dd855.png"
		alt="Crear Instancia"
	style="float: left; margin-right: 10px;" />
</p>

Nos despliega el menú de configuración de la máquina que queremos crear, en primer lugar debemos ofrecer un nombre a nuestra instancia.

<p align="center">
	<img src="https://user-images.githubusercontent.com/104928044/169713232-d5c0a7a9-7d32-42d5-aff0-f989c21c6404.png"
		alt="Nombre Instancia"
	style="float: left; margin-right: 10px;" />
</p>

Omitimos el apartado **Ubicación**, simplemente comprobamos que se encuentra por defecto **Dominio de disponibilidad** en la opción de **Siempre gratis elegible**.

<p align="center">
	<img src="https://user-images.githubusercontent.com/104928044/169713315-5b47b36e-9b5b-4e06-a723-373a43ac1f8d.png"
		alt="Ubicación"
	style="float: left; margin-right: 10px;" />
</p>

Continuamos con **Imagen y unidad**, aquí pinchamos sobre la palabra **Editar** que nos aparece dentro del recuadro blanco arriba a la derecha.

<p align="center">
	<img src="https://user-images.githubusercontent.com/104928044/169713392-bc84a855-97d4-4600-ae5e-d1ef7b3bf5ac.png"
		alt="Imagen y unidad"
	style="float: left; margin-right: 10px;" />
</p>

Pinchamos sobre el botón **Cambiar imagen**.

<p align="center">
	<img src="https://user-images.githubusercontent.com/104928044/169714681-393b19a4-c6d3-469e-b012-96317bac6041.png"
		alt="Cambiar Imagen"
	style="float: left; margin-right: 10px;" />
</p>

Elegimos la imagen de **Canonical Ubuntu** en este momento la versión más reciente 20.04 y pulsamos más abajo en **Seleccionar imagen**.

<p align="center">
	<img src="https://user-images.githubusercontent.com/104928044/169714796-82c4b95d-3762-4edf-8257-c76e2e518da1.png"
		alt="Elección Imagen"
	style="float: left; margin-right: 10px;" />
</p>

Nos dirigimos ahora a la elección de CPU y seleccionamos **Change Shape** (Cambiar forma).

**IMPORTANTE:** En mi caso, al tener otras instancias creadas me ofrecen ciertas CPU con número de núcleos y RAM algo más limitado de manera gratuita. Usando procesadores ARM (Ampere) obtendréis un mayor número de posibilidades de configuración, en este caso vamos a usar AMD con el que he podido testear que todo funciona correctamente, los requisitos recomendables para esta instancia son mínimos, pero podréis ofrecerle vosotros mismos la cantidad de núcleos y RAM que penséis que será la ideal.

El resultado de mi configuración sería la siguiente:
(Insisto, no es la configuración de CPU central que debéis usar, queda a vuestro gusto y necesidades).

<p align="center">
	<img src="https://user-images.githubusercontent.com/104928044/169715250-fd574500-4a22-426a-adef-20426148e5af.png"
		alt="CPU"
	style="float: left; margin-right: 10px;" />
</p>

El apartado de **Red** lo dejamos de serie, os debe salir nombre de **Red virtual en la nube** y **Subred** con letras y numeraciones ya que no le habéis asignado un nombre, pero como no queremos complicarnos así va bien. Solo tenedlo en cuenta.

<p align="center">
	<img src="https://user-images.githubusercontent.com/104928044/169715409-62efc820-9314-48e5-adb6-376591b45bfe.png"
		alt="Red"
	style="float: left; margin-right: 10px;" />
</p>

**Agregar claves SSH** un apartado importante donde la mayoría de personas un poco ajenas al mundo de la informática suelen tener problemas pero es muy simple. Vemos como ya por defecto Oracle Cloud nos ofrece un par de claves que descargar, debemos descargar ambas claves y guardarlas en un lugar seguro.

<p align="center">
	<img src="https://user-images.githubusercontent.com/104928044/169715651-455a9ec9-b4fc-47c8-a4b1-146ff7a0cea6.png"
		alt="Agregar clave ssh"
	style="float: left; margin-right: 10px;" />
</p>

Una vez tengamos las claves descargadas en nuestro equipo, tendremos que cargar la clave **PÚBLICA (.pub)** a nuestro servidor VPS.

<p align="center">
	<img src="https://user-images.githubusercontent.com/104928044/169715835-3befe512-3aba-4c7f-be40-2141508d552c.png"
		alt="Clave pub"
	style="float: left; margin-right: 10px;" />
</p>

Por último, en **Volumen de inicio** marcamos la opción de **Especificar un tamaño de volumen de inicio** que debe de ser de un **mínimo de 50GB** y **Usar cifrado en tránsito** y pulsamos en **Crear**. Este paso dura unos minutos, debemos esperar a que la instancia pase de **APROVISIONANDO** a **EN EJECUCIÓN**.

<p align="center">
	<img src="https://user-images.githubusercontent.com/104928044/169716009-46afadc0-3db3-4c6b-8f83-61b6861d23a9.png"
		alt="Volumen"
	style="float: left; margin-right: 10px;" />
</p>

<p align="center">
	<img src="https://user-images.githubusercontent.com/104928044/169716104-8844e95d-a42b-470f-a6de-8a2100dba160.png"
		alt="Crear"
	style="float: left; margin-right: 10px;" />
</p>

¡Y AL FIN TENEMOS NUESTRA INSTANCIA CREADA! ¿Sencillo verdad?

## Acceso y configuración de nuestra instancia

Para el acceso hacia nuestro servidor utilizaremos la terminal **CMD de Windows**, para ello nos dirigimos a nuestro buscador de Windows y escribimos **CMD** y pinchamos sobre él para abrir la terminal.

<p align="center">
	<img src="https://user-images.githubusercontent.com/104928044/169716537-f2bf3d31-c14d-4942-b456-1475a08bbb8b.png"
		alt="CMD"
	style="float: left; margin-right: 10px;" />
</p>

Como quiero simplificarlo lo máximo posible para que personas no experimentadas en el manejo de comandos de terminales puedan conseguir realizar este tutorial, voy a intentar no entrar mucho en técnicismos.

Vamos a dirigirnos a la carpeta donde tenemos guardado nuestras par de claves que descargamos anteriormente, en mi caso y a modo de ejemplo sencillo (pero no seguro) estarán en mi escritorio.

<p align="center">
	<img src="https://user-images.githubusercontent.com/104928044/169716833-2067d1f9-1c81-4fb5-aece-84303fa014ac.png"
		alt="CMD"
	style="float: left; margin-right: 10px;" />
</p>

Se nos abre la siguiente ventana de color negra en la que nos muestra escrito en blanco **C:\Users\(NOMBRE DE NUESTRO USUARIO DE WINDOWS)**, desde este punto vamos a usar el comando **cd** seguido de la ruta que nos lleva a nuestro escritorio, pero para asegurarnos usaremos **dir**, este nos mostrará todas carpetas y archivos del directorio en el que nos encontramos.

dir + tecla enter

<p align="center">
	<img src="https://user-images.githubusercontent.com/104928044/169717085-c04f3350-68d1-4459-a78c-6a2b7bbab0d4.png"
		alt="dir"
	style="float: left; margin-right: 10px;" />
</p>

En mi caso el nombre de mi escritorio de encuentra en inglés **(Desktop)**, pero muy probablamente el de vosotros se encuentre como **(Escritorio)**. Por lo que para dirigirnos a este lugar debemos escribir lo siguiente:

En mi caso:
~~~
cd Desktop
~~~
Muy probablemente en el de vosotros:
~~~
cd Escritorio
~~~

Y pulsamos **Enter**.

Comprobamos de nuevo si nos encontramos en el directorio correcto con el comando **dir** y vemos si se encuentran nuestro par de claves en ese lugar.

<p align="center">
	<img src="https://user-images.githubusercontent.com/104928044/169717337-50df68d8-e802-40f9-a675-d1f817bb42c5.png"
		alt="dir"
	style="float: left; margin-right: 10px;" />
</p>

Para realizar el acceso mediante la conexión SSH hacia nuestro servidor mediante par de claves debemos tener en cuenta este paso:

<p align="center">
	<img src="https://user-images.githubusercontent.com/104928044/170970958-648d23cf-5a9f-411e-92a8-20351026c3ca.png"
		alt="dir"
	style="float: left; margin-right: 10px;" />
</p>

Tendremos que irnos al apartado de **"Recursos informáticos > Instancias > Detalles de la instancia"** y comprobar el usuario e IP pública que nos han asignado para la conexión, en este caso el usuario es **"ubuntu"** y la IP pública **"152.67.71.249"**. (Es muy importante que esta IP no la demos a conocer, mediante esta dirección cualquier posible atacante podrían tumbarnos el servidor o incluso tener acceso a él si no se ha implementado un nivel de seguridad al menos básico).

En esta guía no entraremos en detalles a la hora de bastionar un servidor Cloud ya que podría ser tan extenso que daría para otro apartado más, pero es importante tener en cuenta este tipo de consejos de un principio para usuarios totalmente nóveles.

Sigamos entonces, ahora construiremos el comando que nos dará acceso a nuestro servidor ya teniendo los datos esenciales de acceso y nuestra clave privada para la conexión:

<p align="center">
	<img src="https://user-images.githubusercontent.com/104928044/170973050-8f23985a-8936-4918-8113-188a0783539c.png"
		alt="ssh"
	style="float: left; margin-right: 10px;" />
</p>

Nos realizará una cuestión, en la que nos dice si queremos seguir con la conexión y escribimos **"yes"**.

**[PUEDES OMITIR ESTA PARTE SI NO TE APARECE EL SIGUIENTE MENSAJE]**

**ADVERTENCIA:** Es posible que nos salga la siguiente alerta en la que nos dice que nuestra clave privada no se encuetra protegida (Debemos protegerla en un sitio seguro y recomendable bajo algún tipo de clave o encriptación) nosotros realizaremos un remedio **"NO ejemplar"** pero que nos servirá para continuar:

<p align="center">
	<img src="https://user-images.githubusercontent.com/104928044/170973671-ac9547c8-935b-45ea-948c-81fd55d0cba2.png"
		alt="Permisos"
	style="float: left; margin-right: 10px;" />
</p>

Nos dirigimos en Windows a nuestro archivo de clave privada, recordad (la que finaliza con la extensión **".key"**) y realizaremos lo siguiente:

<p align="center">
	<img src="https://user-images.githubusercontent.com/104928044/170974156-9fa62cb9-69aa-4e26-80f7-d6fabe31b59b.png"
		alt="key"
	style="float: left; margin-right: 10px;" />
</p>

Haremos click derecho sobre el archivo **".key"** y seleccionamos **"Propiedades"**.

<p align="center">
	<img src="https://user-images.githubusercontent.com/104928044/170974728-fa835283-ee18-479d-88b9-22a7c75c0030.png"
		alt="propiedades key"
	style="float: left; margin-right: 10px;" />
</p>

Veremos los usuarios que tienen permisos sobre este archivo y nos dirigimos a **"Opciones avanzadas"**.

<p align="center">
	<img src="https://user-images.githubusercontent.com/104928044/170975299-0f657d24-9fdd-4072-b46f-ef0970921cc5.png"
		alt="opciones avanzadas"
	style="float: left; margin-right: 10px;" />
</p>

Abajo nos aparecerá un botón en el que nos dice **"Deshabilitar herencia"** pinchamos sobre este y se nos abrirá otra nueva ventana en la que seleccionaremos **"Quitar todos los permisos heredados de este objeto"**.

Ahora en la misma ventana donde ya no nos aparecen todos los usuarios que tenían permisos anteriormente pulsamos sobre **"Agregar"**.

<p align="center">
	<img src="https://user-images.githubusercontent.com/104928044/170976109-baf49ec4-e8bf-491c-a896-ea37cf19a644.png"
		alt="herencia"
	style="float: left; margin-right: 10px;" />
</p>

<p align="center">
	<img src="https://user-images.githubusercontent.com/104928044/170976194-917cedb5-13ae-49e2-87a6-ce69f0e294a6.png"
		alt="herencia"
	style="float: left; margin-right: 10px;" />
</p>

Realizamos click sobre **"Seleccionar una entidad de seguridad"** y se nos abrirá una nueva ventana.

<p align="center">
	<img src="https://user-images.githubusercontent.com/104928044/170976708-cd706efa-321d-4b9e-9532-ab9f95310491.png"
		alt="Entidad Seguridad"
	style="float: left; margin-right: 10px;" />
</p>

Donde se muestra la flecha roja, debemos añadir nuestro usuario de Windows y seleccionar en **"Comprobar nombres"**, si todo está correcto pulsamos sobre aceptar.

Una vez ya tengamos nuestro usuario seleccionado, marcamos con el ratón en la casilla de **"Control total"**, aplicamos y aceptamos en todas las ventanas anteriores.

<p align="center">
	<img src="https://user-images.githubusercontent.com/104928044/170977167-95a6fc89-4350-4395-b249-8830ab9419c3.png"
		alt="control total"
	style="float: left; margin-right: 10px;" />
</p>

De nuevo realizamos el intento de conexión como anteriormente explicamos y podemos comprobar que ya tenemos acceso a nuestro servidor mediante nuestro par de claves.

<p align="center">
	<img src="https://user-images.githubusercontent.com/104928044/170977912-7046b161-3b7a-4895-848f-efd99aaecd6b.png"
		alt="acceso"
	style="float: left; margin-right: 10px;" />
</p>

**[FIN DE LA PARTE QUE PUEDES OMITIR SI NO TE APARECE EL MENSAJE DE ADVERTENCIA]**

## Cambiar acceso de par de claves a un acceso mediante usuario y contraseña (Método mucho más inseguro).

Como temo que muchas de las personas que veréis esta guía vais a preferir este método más tradicional pero más inseguro, os lo voy a intentar explicar de la forma más sencilla posible y segura.

En primer lugar realizamos una actualizacion de nuestros repositorios:

~~~
sudo apt update -y && sudo apt upgrade -y
~~~

Instalaremos **Fail2ban** esta aplicación nos protegerá aquellos puertos que tengamos abiertos ante varios intentos fallidos y que posteriormente serán baneados para evitar posibles ataques de fuerza bruta.

~~~
sudo apt install fail2ban -y
~~~

Nos dirigimos al siguiente directorio en el que tendremos que modificar una serie de parámetros importantes dentro de esta herramienta, aunque es muy personalizable según las necesidades que cada uno vaya a requerir.

~~~
cd /etc/fail2ban
~~~

<p align="center">
	<img src="https://user-images.githubusercontent.com/104928044/170983006-9523ab14-dfb7-43b0-a8c4-5822bc76ad54.png"
		alt="fail2ban"
	style="float: left; margin-right: 10px;" />
</p>

Vamos a realizar una copia de seguridad de nuestro archivo de configuración que viene por defecto **"jail.conf"**.

~~~
sudo cp jail.conf jail.local
~~~

<p align="center">
	<img src="https://user-images.githubusercontent.com/104928044/174291393-0ee2d066-8e29-4094-8ce9-563d61846c32.png"
		alt="fail2ban"
	style="float: left; margin-right: 10px;" />
</p>

Abrimos el archivo de configuración con el siguiente comando:

~~~
sudo nano jail.local
~~~

Nos dirigimos al apartado [DEFAULT] y descomentaremos las siguientes líneas (Borrar '#' de delante), os debe de quedar algo así:

<p align="center">
	<img src="https://user-images.githubusercontent.com/104928044/170997353-baa88d9f-d340-4e3d-9972-9f6e5bd25b00.png"
		alt="fail2ban"
	style="float: left; margin-right: 10px;" />
</p>

Para guardar esta configuración debemos pulsar **"Control + O" y "Enter"** y para salir **"Control + X"**.

Hemos configurado para que haga un baneo básico gradual, cada cierto numero de equivocaciones será baneado un tiempo que este se prolongará más a cada número de intentos fallidos que realice.

Para aplicarlos cambios en este archivo realizaremos el siguiente comando:

~~~
sudo systemctl restart fail2ban.service
~~~

Vamos ahora a configurar nuestro puerto SSH de entrada que no será el que viene por defecto [22] ya que seremos muy propensos a ataques automatizados con ese puerto.

Nos dirigimos al directorio donde encontramos el archivo de configuración de SSH:

~~~
cd /etc/ssh
~~~

<p align="center">
	<img src="https://user-images.githubusercontent.com/104928044/170998583-5274520e-562c-45aa-bede-757c69a0e87f.png"
		alt="ssh"
	style="float: left; margin-right: 10px;" />
</p>

Abrimos el archivo **"sshd_config"**:

~~~
sudo nano sshd_config
~~~

Una vez se nos despligue este archivo, debemos configurar dos parámetros, uno será el puerto por el que tendremos acceso por SSH y permitir la autenticación mediante contraseña:

Cambiamos el puerto por defecto:

<p align="center">
	<img src="https://user-images.githubusercontent.com/104928044/170999386-e18ca01d-44be-4d6e-aea7-f354d112e689.png"
		alt="puertos"
	style="float: left; margin-right: 10px;" />
</p>

Permitimos la autenticación por contraseña:

<p align="center">
	<img src="https://user-images.githubusercontent.com/104928044/170999474-5d870967-d3e7-48ff-9434-36351eb3a73d.png"
		alt="authpass"
	style="float: left; margin-right: 10px;" />
</p>

Para guardar esta configuración debemos pulsar **"Control + O" y "Enter"** y para salir **"Control + X"**.

Es importante antes de aplicar los cambios dar una contraseña al usuario **"ubuntu"** con el comando "passwd" de no darle una contraseña previamente, el usuario no tendrá credenciales y no podremos acceder a nuestro servidor.

~~~
sudo passwd ubuntu
~~~

<p align="center">
	<img src="https://user-images.githubusercontent.com/104928044/171000273-8cde1617-5645-4507-84fc-528b2807b6c4.png"
		alt="passwd"
	style="float: left; margin-right: 10px;" />
</p>

Debéis saber que aunque cuando escribáis no se os muestre la contraseña realmente estáis escribiendo, es simplemente por seguridad por lo que no se os muestra y pulsáis enter para pasar de nuevo a confirmar la contraseña anteriormente ofrecida.

Reiniciamos y aplicamos los cambios con el comando:

~~~
systemctl restart sshd.service
~~~

<p align="center">
	<img src="https://user-images.githubusercontent.com/104928044/171000897-dd276f51-ab11-4671-b0af-c0d27c4a12dc.png"
		alt="sshdserv"
	style="float: left; margin-right: 10px;" />
</p>

Nos pedirá de nuevo la contraseña que le ofrecimos al usuario para confirmar los cambios y listo.

Por último, nos queda abrir el nuevo puerto de entrada por SSH que tendrá nuestro servidor para ellos debemos de irnos a la web de Oracle Cloud en el apartado de **"Recursos informáticos > Instancias > Detalles de la instancia"**:

<p align="center">
	<img src="https://user-images.githubusercontent.com/104928044/171001412-8282002d-6693-42c3-b239-2ca947d4f8bc.png"
		alt="detalles"
	style="float: left; margin-right: 10px;" />
</p>

Pinchamos sobre el nombre de la **"Subred"** que le tengamos asignada.

<p align="center">
	<img src="https://user-images.githubusercontent.com/104928044/171001887-c655e07f-469e-48c7-996e-fb4b7fb21e27.png"
		alt="subred"
	style="float: left; margin-right: 10px;" />
</p>

De nuevo hacemos click sobre **"Default Security List for principal"**.

<p align="center">
	<img src="https://user-images.githubusercontent.com/104928044/171001992-6428ea30-22bf-4ceb-a7ba-4771647617a6.png"
		alt="subred"
	style="float: left; margin-right: 10px;" />
</p>

Y añadimos una nueva regla de entrada.
 
<p align="center">
	<img src="https://user-images.githubusercontent.com/104928044/171002238-6c61d820-885a-4b3d-af3d-e2ba5f0955c3.png"
		alt="regla entrada"
	style="float: left; margin-right: 10px;" />
</p>

<p align="center">
	<img src="https://user-images.githubusercontent.com/104928044/171002526-f8135601-51d1-4641-b106-466825b2a5f0.png"
		alt="regla entrada"
	style="float: left; margin-right: 10px;" />
</p>

Guardamos esta regla de entrada y lo que estaremos indicando es que desde cualquier IP por protocolo TCP y con destino al puerto 22422 le permitamos la conexión.

Pero eso no es todo, nos falta algo importante, añadir nuestra regla en la tabla de IP Tables. 

~~~
sudo iptables -I INPUT 6 -m state --state NEW -p tcp --dport [PUERTO] -j ACCEPT
sudo netfilter-persistent save
~~~

De esta forma ya tendríamos todo completado y ya nos debería de permitir el acceso mediante usuario y clave a la hora desde un nuevo CMD realizar la conexión con nuestro servidor de la siguiente manera:

~~~
ssh -p [PUERTO] [USUARIO]@[TU IP PÚBLICA]
~~~

<p align="center">
	<img src="https://user-images.githubusercontent.com/104928044/171006448-5dd7c21c-0c31-48a2-8631-13185863ca62.png"
		alt="ssh"
	style="float: left; margin-right: 10px;" />
</p>

¡LISTO!

# Instalación de DVSwitch

Comenzamos con lo importante, una vez nos encontremos dentro de de nuestro servidor a través de nuestra ventana CMD, lo primero que debemos realizar es una actualización de nuestros repositorios para ello debemos de ejecutar el siguiente comando:

~~~
sudo apt update -y && sudo apt upgrade -y
~~~

<p align="center">
	<img src="https://user-images.githubusercontent.com/104928044/170979761-70901091-c064-408d-8664-2f6b242e7420.png"
		alt="update & upgrade"
	style="float: left; margin-right: 10px;" />
</p>

Esta actualización nos demorará varios minutos, tened paciencia.

Una vez tengamos todo actualizado, es hora de ponernos manos a la obra con la instalación de DVSwitch Server.
Para comenzar descargaremos el archivo de instalación de los repositorios con el siguiente comando:

~~~
wget http://dvswitch.org/buster
~~~

<p align="center">
	<img src="https://user-images.githubusercontent.com/104928044/174059352-f5ae3673-81a4-4f8b-bf0c-2db3d4c6fef9.png"
		alt="buster"
	style="float: left; margin-right: 10px;" />
</p>

A continuación, daremos permisos de ejecución al archivo **"buster"** recientemente obtenido y lo ejecutaremos.

~~~
sudo chmod +x buster
sudo ./buster
~~~

<p align="center">
	<img src="https://user-images.githubusercontent.com/104928044/174059751-d1a18abc-bd6b-4aa7-b887-90eecdadbe1a.png"
		alt="buster"
	style="float: left; margin-right: 10px;" />
</p>

Ya teniendo los repositorios correctamente descargados, iniciamos la instalación de DVSwitch Server de la siguiente manera:

~~~
sudo apt install dvswitch-server
~~~

<p align="center">
	<img src="https://user-images.githubusercontent.com/104928044/174060310-a1e53541-814a-4123-9109-6b25c593ef02.png"
		alt="dvswitchserver"
	style="float: left; margin-right: 10px;" />
</p>

En este punto debemos esperar unos minutos a que se realice toda la instalación y realizaremos un reinicio de nuestro servidor VPS mediante:

~~~
sudo reboot
~~~

Nos expulsará de la terminal de nuestro VPS. no os preocupéis, ahora simplemente debéis esperar unos minutos a que el servidor tenga tiempo de reiniciarse y volvéis a acceder de la misma manera que anteriormente explicamos a través de nuestro CMD de Windows.

~~~
ssh -p [PUERTO] [USUARIO]@[TU IP PÚBLICA]
~~~

Introducimos la contraseña y volveremos a estar dentro de nuestro VPS.

Ahora solo debemos de escribir las sigles **"dvs"** en nuestra terminal y pulsar **"enter"** para activar el script.

Nos mostrará una ventana en la que nos dirá si queremos cambiar el idioma de nuestra aplicación, en mi caso, lo cambiaré a Español, para ello elegiremos la opción de **"Yes"** y nos mostrará una lista con varios idiomas, nos desplazamos con las flechas de teclado hasta la opción que decidamos y con la tecla de **"TAB"** (Tabulador), señalaremos la opción de **"Ok"** para confirmar nuestra selección y pulsamos **"Enter"**.

<p align="center">
	<img src="https://user-images.githubusercontent.com/104928044/174062839-ab8fc1f8-2be3-4435-af5a-dc4d30c088e0.png"
		alt="dvs"
	style="float: left; margin-right: 10px;" />
</p>

Nos mostrará el menú principal de la herramienta donde podremos configurar todos los apartados, pero en este caso iremos al grano y os explicaré las configuraciones básicas y esenciales para comenzar a hacerlo funcional.

<p align="center">
	<img src="https://user-images.githubusercontent.com/104928044/174063077-92142d89-646b-4afb-a0b8-092eff11c6e8.png"
		alt="dvs"
	style="float: left; margin-right: 10px;" />
</p>

Elegimos la opción **"01 Configuración inicial"**, recordad, marcáis el apartado con las flechas y con **"TAB"+"Enter"** confirmáis la opción.

<p align="center">
	<img src="https://user-images.githubusercontent.com/104928044/174063353-7cbbf76e-44dc-4867-be10-80bed4b65b32.png"
		alt="config ini"
	style="float: left; margin-right: 10px;" />
</p>

Tened en cuenta que para el uso de esta herramienta será necesario tener una licencia vigente de radioaficionado, indicativo e ID de DMR. Elegimos la opción de **"Yes"**.

<p align="center">
	<img src="https://user-images.githubusercontent.com/104928044/174063758-ad818d5d-7e6a-4cd1-95f3-549ca5f8c1cc.png"
		alt="yes"
	style="float: left; margin-right: 10px;" />
</p>

En esta ventana introducimos nuestro indicativo, seguimos.

<p align="center">
	<img src="https://user-images.githubusercontent.com/104928044/174064308-7a5ba338-8290-40cd-9985-fb98dfe65ebf.png"
		alt="id"
	style="float: left; margin-right: 10px;" />
</p>

Aquí debemos de introducir nuestro ID de DMR. (Esta ID se obtiene desde la web de [radioid.net](https://radioid.net/))

<p align="center">
	<img src="https://user-images.githubusercontent.com/104928044/174064873-2fc2ac16-4181-402a-8766-8b7219e3950d.png"
		alt="id"
	style="float: left; margin-right: 10px;" />
</p>

En la siguiente ventana nos requiere la misma ID, pero en la que debemos de añadirle dos dígitos más pudiendo estar estos entre los intervalos de (00 hasta 99), de esta manera evitamos la duplicidad de nuestra ID, así pudiendo usar la misma más un sufijo en multitud de dispositivos alternativos a uno principal.

<p align="center">
	<img src="https://user-images.githubusercontent.com/104928044/174078273-4255d096-8b46-4a73-95e2-678f023eb04e.png"
		alt="id"
	style="float: left; margin-right: 10px;" />
</p>

El módulo Dstar lo dejaremos por defecto en **"B"** ya que para nuestro objetivo ahora mismo no nos es necesario.

<p align="center">
	<img src="https://user-images.githubusercontent.com/104928044/174078568-9bd478fc-f89f-4b77-a081-df6276c4bf37.png"
		alt="B"
	style="float: left; margin-right: 10px;" />
</p>

ID NXDN, lo dejaremos vacío y seguimos hacia la siguiente ventana.

<p align="center">
	<img src="https://user-images.githubusercontent.com/104928044/174079133-ca4da7f2-a2b8-4fb2-950f-9723fee7d2f5.png"
		alt="nxdn"
	style="float: left; margin-right: 10px;" />
</p>

Este apartado es importante, debemos configurar el puerto por el que pasará todo nuestro tráfico, vamos a poner como ejemplo **"51051"** pero esto va a gustos y preferencias de cada uno de vosotros.

<p align="center">
	<img src="https://user-images.githubusercontent.com/104928044/174079227-61d33c13-c880-4952-b4ec-fc3360508007.png"
		alt="nxdn"
	style="float: left; margin-right: 10px;" />
</p>

Elegimos el servidor de Brandmeister España y pulsamos en **"Ok"**.

<p align="center">
	<img src="https://user-images.githubusercontent.com/104928044/174080854-47054e6d-5e1f-4645-a01f-4e27bcded943.png"
		alt="ok"
	style="float: left; margin-right: 10px;" />
</p>

Como bien nos indica el apartado introduciremos nuestra contraseña que tenemos asociada a nuestra cuenta de Brandmeister (No es obligatorio el uso de esta red, esta se trata de una red privada en la que para su uso debemos realizar un registro y obtener estas credenciales de acceso). En este caso, realizaremos la conexión mediante otra red, que posteriormente explicaremos.

<p align="center">
	<img src="https://user-images.githubusercontent.com/104928044/174081979-63309b38-f8cd-4713-a55a-b93c23c306f3.png"
		alt="dmr"
	style="float: left; margin-right: 10px;" />
</p>

Para este apartado he estado realizando varias pruebas con un servidor AMBE pero desde Oracle Cloud y mediante varias pruebas no he podido conseguir que el tráfico de la comunicación pase por este mismo para mejorar muy notablemente la calidad de audio, por lo que lo haremos funcionar mediante la opción **"4. Sin codificador de voz de hardware"** en la utilizaremos un **software Vocoder**.

<p align="center">
	<img src="https://user-images.githubusercontent.com/104928044/174082036-c102c18e-3bf5-470a-8938-dcb8b5898f0c.png"
		alt="vocoder"
	style="float: left; margin-right: 10px;" />
</p>

Pulsamos sobre **"Yes"** y todos los ajustes comenzarán a aplicarse.

<p align="center">
	<img src="https://user-images.githubusercontent.com/104928044/174082166-838e6694-7ae0-47d6-bdc5-07a113ca6374.png"
		alt="yes"
	style="float: left; margin-right: 10px;" />
</p>

Ya la configuración inicial la tendríamos totalmente configurada y lista, pero **no olvidemos que hemos decidido en este ejemplo usar el puerto 51051** para tramitar toda la información de nuestro servidor, asi que debemos ponernos manos a la obra desde la web de Oracle Cloud para abrir nuestro puerto y crear la regla necesaria para iptables.

Configuración de la **apertura** del **puerto 51051** en **Oracle Cloud**:

<p align="center">
	<img src="https://user-images.githubusercontent.com/104928044/174084936-9df595a4-7ab7-4914-927d-350631ca91a8.png"
		alt="yes"
	style="float: left; margin-right: 10px;" />
</p>

Regla que debemos introducir en nuestra iptables:

~~~
sudo iptables -I INPUT 7 -m state --state NEW -p udp --dport [PUERTO] -j ACCEPT
sudo netfilter-persistent save
~~~

De esta manera ya tendríamos toda la configuración inicial lista. Pasamos a la configuración en nuestro teléfono móvil.

# Instalación y configuración de DVSwitch Mobile

De acuerdo, entiendo que hasta este punto podréis estar un poco saturados, pero tranquilos, hemos llegado a la parte más sencilla el final. Debemos dirigirnos a Google Play y buscar dentro de la tienda **"DVSwitch Mobile"** y la descargamos en nuestro terminal.

<p align="center">
	<img src="https://user-images.githubusercontent.com/104928044/174095701-51cc48d0-3a9b-4873-8f17-3554b71493cc.png"
		alt="dvswitch mobile"
	style="float: left; margin-right: 10px;" />
</p>

Abrimos la aplicación y nos dirigimos a la pestaña **"Accounts"**:

<p align="center">
	<img src="https://user-images.githubusercontent.com/104928044/174112691-f06df3bf-29a7-40f1-9f92-e1bc9a4246a6.png"
		alt="accounts"
	style="float: left; margin-right: 10px;" />
</p>

Veremos todos los huecos para configurar vacíos, con lo que pinchamos sobre uno de ellos:

<p align="center">
	<img src="https://user-images.githubusercontent.com/104928044/174096654-0eba4f45-44d7-4250-b729-64a73d3ff7b2.png"
		alt="config"
	style="float: left; margin-right: 10px;" />
</p>

Debemos modificar el protocolo con el que vamos a trabajar para ello pulsamos sobre la pestaña de **"Protocol"** y lo cambiaremos a **"USRP"**:

<p align="center">
	<img src="https://user-images.githubusercontent.com/104928044/174097238-a0b966a5-e3a2-4d79-9267-a80c520da16f.png"
		alt="proto"
	style="float: left; margin-right: 10px;" />
</p>

<p align="center">
	<img src="https://user-images.githubusercontent.com/104928044/174097201-7d0f8303-0248-4ff1-8eff-059288d5167c.png"
		alt="proto"
	style="float: left; margin-right: 10px;" />
</p>

En hostname debemos de introducir la IP pública de nuestro servidor VPS, pero como consejo más práctico creo que lo mejor será usar un **DNS gratuito** con el que le podamos asignar un nombre a esa IP para poder recordarla de una manera más sencilla. Tenemos a nuestra disposición la web de **DuckDNS**, es muy práctica y solo tardamos 1 minutos en realizar todo el proceso:

Nos dirigimos a la web de https://www.duckdns.org/, nos registramos mismamente con una cuenta de Gmail y nos abrirá un menú como el siguiente:

<p align="center">
	<img src="https://user-images.githubusercontent.com/104928044/174098363-60ffa47d-57df-4af5-b7b9-d86ad5325cea.png"
		alt="duck dns"
	style="float: left; margin-right: 10px;" />
</p>

En este menú añadiremos el nombre que queremos para nuestra dirección, a modo de ejemplo, he puesto **"mobile-radio"**.

Una vez añadido el nombre de dominio debemos asignarle la IP pública a la que debe estar asociada este dominio.

<p align="center">
	<img src="https://user-images.githubusercontent.com/104928044/174098889-56dfd0d6-2000-4885-9049-81c3259c80c1.png"
		alt="duck dns"
	style="float: left; margin-right: 10px;" />
</p>

Estupendo, ahora volvemos a nuestro teléfono y introduciremos todos los datos necesarios:

<p align="center">
	<img src="https://user-images.githubusercontent.com/104928044/174101070-31498f29-07d4-48c1-ba9f-7e4e1089ed70.png"
		alt="mobile"
	style="float: left; margin-right: 10px;" />
</p>

Una vez tengamos todos los parámetros configurados pulsaremos sobre **"Save"**.

Ahora vamos a configurar nuestra conexión a través de **YSF** y la red de **EUROPELINK** como ejemplo, vosotros podréis utilizar la que más os guste.

<p align="center">
	<img src="https://user-images.githubusercontent.com/104928044/174113084-b54524ee-d4d2-4653-97dd-8fdde9b52814.png"
		alt="mobile"
	style="float: left; margin-right: 10px;" />
</p>

Manteniendo pulsada la letra **"A"** podemos elegir el modo por el que queremos salir:

<p align="center">
	<img src="https://user-images.githubusercontent.com/104928044/174102645-37b60431-18f2-47db-8137-35b7a1d02fef.png"
		alt="mobile"
	style="float: left; margin-right: 10px;" />
</p>

Manteniendo la **"B"** podremos elegir que Talkgroup de YSF queremos utilizar, voy a elegir EUROPELINK por ejemplo. Podemos incluso utilizar el dashboard de EUROPELINK (http://europelink.pa7lim.nl/) para observar todo el movimiento del tráfico que existe en la red y los compañeros que se encuentran transmitiendo.

<p align="center">
	<img src="https://user-images.githubusercontent.com/104928044/174129303-54ab397c-3ba2-4ea2-a32f-76c627146f7c.png"
		alt="mobile"
	style="float: left; margin-right: 10px;" />
</p>

<p align="center">
	<img src="https://user-images.githubusercontent.com/104928044/174104199-185ae963-8266-4b1b-9568-6e9ef07e5e62.png"
		alt="mobile"
	style="float: left; margin-right: 10px;" />
</p>
