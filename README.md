# DVSwitch & APPMobile
Creación de DVSwitch Server en Oracle Cloud (VPS Gratuito) y DVSwitch Mobile para radioaficionados.

## Requisitos Previos
Para seguir correctamente esta guía será necesario estar en posesión de algún servidor VPS cloud de pago o parcialmente gratuito como el que se ofrece en este tutorial. En el registro para la obtención de esta versión gratuita de Oracle Cloud será imprescindible tener una tarjeta bancaria para la autenticación de ser una persona física.

Será necesario tener una licencia vigente de radioaficionado y estar registrado en la red de Brandmeister.

## Creación de una instancia en Oracle Cloud

Entramos en nuestra cuenta de Oracle Cloud y nos dirigimos al menú de nuestra banda izquierda, este es posible desplegarlo mediante el icono con tres línes horizontales, nos dirigimos al apartado de **Recursos informáticos > Instancia**.

![image](https://user-images.githubusercontent.com/104928044/169712856-42d9e12a-dd8c-4329-93fa-98e44ca0ca45.png)

Nos cambiará de ventana e iremos a un menú donde aparecerá un botón de color azul en que nos dirá **Crear instancia**.

![image](https://user-images.githubusercontent.com/104928044/169713055-478d6dea-0cb8-410e-b014-4ab5045dd855.png)

Nos despliega el menú de configuración de la máquina que queremos crear, en primer lugar debemos ofrecer un nombre a nuestra instancia.

![image](https://user-images.githubusercontent.com/104928044/169713232-d5c0a7a9-7d32-42d5-aff0-f989c21c6404.png)

Omitimos el apartado **Ubicación**, simplemente comprobamos que se encuentra por defecto **Dominio de disponibilidad** en la opción de **Siempre gratis elegible**.

![image](https://user-images.githubusercontent.com/104928044/169713315-5b47b36e-9b5b-4e06-a723-373a43ac1f8d.png)

Continuamos con **Imagen y unidad**, aquí pinchamos sobre la palabra **Editar** que nos aparece dentro del recuadro blanco arriba a la derecha.

![image](https://user-images.githubusercontent.com/104928044/169713392-bc84a855-97d4-4600-ae5e-d1ef7b3bf5ac.png)

Pinchamos sobre el botón **Cambiar imagen**.

![image](https://user-images.githubusercontent.com/104928044/169714681-393b19a4-c6d3-469e-b012-96317bac6041.png)

Elegimos la imagen de **Canonical Ubuntu** en este momento la versión más reciente 20.04 y pulsamos más abajo en **Seleccionar imagen**.

![image](https://user-images.githubusercontent.com/104928044/169714796-82c4b95d-3762-4edf-8257-c76e2e518da1.png)

Nos dirigimos ahora a la elección de CPU y seleccionamos **Change Shape** (Cambiar forma).

**IMPORTANTE:** En mi caso, al tener otras instancias creadas me ofrecen ciertas CPU con número de núcleos y RAM algo más limitado de manera gratuita. Usando procesadores ARM (Ampere) obtendréis un mayor número de posibilidades de configuración, en este caso vamos a usar AMD con el que he podido testear que todo funciona correctamente, los requisitos recomendables para esta instancia son mínimos, pero podréis ofrecerle vosotros mismos la cantidad de núcleos y RAM que penséis que será la ideal.

El resultado de mi configuración sería la siguiente:
(Insisto, no es la configuración de CPU central que debéis usar, queda a vuestro gusto y necesidades).

![image](https://user-images.githubusercontent.com/104928044/169715250-fd574500-4a22-426a-adef-20426148e5af.png)

El apartado de **Red** lo dejamos de serie, os debe salir nombre de **Red virtual en la nube** y **Subred** con letras y numeraciones ya que no le habéis asignado un nombre, pero como no queremos complicarnos así va bien. Solo tenedlo en cuenta.

![image](https://user-images.githubusercontent.com/104928044/169715409-62efc820-9314-48e5-adb6-376591b45bfe.png)

**Agregar claves SSH** un apartado importante donde la mayoría de personas un poco ajenas al mundo de la informática suelen tener problemas pero es muy simple. Vemos como ya por defecto Oracle Cloud nos ofrece un par de claves que descargar, debemos descargar ambas claves y guardarlas en un lugar seguro.

![image](https://user-images.githubusercontent.com/104928044/169715651-455a9ec9-b4fc-47c8-a4b1-146ff7a0cea6.png)

Una vez tengamos las claves descargadas en nuestro equipo, tendremos que cargar la clave **PÚBLICA (.pub)** a nuestro servidor VPS.

![image](https://user-images.githubusercontent.com/104928044/169715835-3befe512-3aba-4c7f-be40-2141508d552c.png)

Por último, en **Volumen de inicio** marcamos la opción de **Especificar un tamaño de volumen de inicio** que debe de ser de un **mínimo de 50GB** y **Usar cifrado en tránsito** y pulsamos en **Crear**. Este paso dura unos minutos, debemos esperar a que la instancia pase de **APROVISIONANDO** a **EN EJECUCIÓN**.

![image](https://user-images.githubusercontent.com/104928044/169716009-46afadc0-3db3-4c6b-8f83-61b6861d23a9.png)

![image](https://user-images.githubusercontent.com/104928044/169716104-8844e95d-a42b-470f-a6de-8a2100dba160.png)

¡Y AL FIN TENEMOS NUESTRA INSTANCIA CREADA! ¿Sencillo verdad?

## Acceso y configuración de nuestra instancia

Para el acceso hacia nuestro servidor utilizaremos la terminal **CMD de Windows**, para ello nos dirigimos a nuestro buscador de Windows y escribimos **CMD** y pinchamos sobre él para abrir la terminal.

![image](https://user-images.githubusercontent.com/104928044/169716537-f2bf3d31-c14d-4942-b456-1475a08bbb8b.png)

Como quiero simplificarlo lo máximo posible para que personas no experimentadas en el manejo de comandos de terminales puedan conseguir realizar este tutorial, voy a intentar no entrar mucho en técnicismos.

Vamos a dirigirnos a la carpeta donde tenemos guardado nuestras par de claves que descargamos anteriormente, en mi caso y a modo de ejemplo sencillo (pero no seguro) estarán en mi escritorio.

![image](https://user-images.githubusercontent.com/104928044/169716833-2067d1f9-1c81-4fb5-aece-84303fa014ac.png)

Se nos abre la siguiente ventana de color negra en la que nos muestra escrito en blanco **C:\Users\(NOMBRE DE NUESTRO USUARIO DE WINDOWS)**, desde este punto vamos a usar el comando **cd** seguido de la ruta que nos lleva a nuestro escritorio, pero para asegurarnos usaremos **dir**, este nos mostrará todas carpetas y archivos del directorio en el que nos encontramos.

dir + tecla enter

![image](https://user-images.githubusercontent.com/104928044/169717085-c04f3350-68d1-4459-a78c-6a2b7bbab0d4.png)

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

![image](https://user-images.githubusercontent.com/104928044/169717337-50df68d8-e802-40f9-a675-d1f817bb42c5.png)

Para realizar el acceso mediante la conexión SSH hacia nuestro servidor mediante par de claves debemos tener en cuenta este paso:

![image](https://user-images.githubusercontent.com/104928044/170970958-648d23cf-5a9f-411e-92a8-20351026c3ca.png)

Tendremos que irnos al apartado de **"Recursos informáticos > Instancias > Detalles de la instancia"** y comprobar el usuario e IP pública que nos han asignado para la conexión, en este caso el usuario es **"ubuntu"** y la IP pública **"152.67.71.249"**. (Es muy importante que esta IP no la demos a conocer, mediante esta dirección cualquier posible atacante podrían tumbarnos el servidor o incluso tener acceso a él si no se ha implementado un nivel de seguridad al menos básico).

En esta guía no entraremos en detalles a la hora de bastionar un servidor Cloud ya que podría ser tan extenso que daría para otro apartado más, pero es importante tener en cuenta este tipo de consejos de un principio para usuarios totalmente nóveles.

Sigamos entonces, ahora construiremos el comando que nos dará acceso a nuestro servidor ya teniendo los datos esenciales de acceso y nuestra clave privada para la conexión:

![image](https://user-images.githubusercontent.com/104928044/170973050-8f23985a-8936-4918-8113-188a0783539c.png)

Nos realizará una cuestión, en la que nos dice si queremos seguir con la conexión y escribimos **"yes"**.

**[PUEDES OMITIR ESTA PARTE SI NO TE APARECE EL SIGUIENTE MENSAJE]**

**ADVERTENCIA:** Es posible que nos salga la siguiente alerta en la que nos dice que nuestra clave privada no se encuetra protegida (Debemos protegerla en un sitio seguro y recomendable bajo algún tipo de clave o encriptación) nosotros realizaremos un remedio "NO ejemplar" pero que nos servirá para continuar:

![image](https://user-images.githubusercontent.com/104928044/170973671-ac9547c8-935b-45ea-948c-81fd55d0cba2.png)

Nos dirigimos en Windows a nuestro archivo de clave privada, recordad (la que finaliza con la extensión ".key") y realizaremos lo siguiente:

![image](https://user-images.githubusercontent.com/104928044/170974156-9fa62cb9-69aa-4e26-80f7-d6fabe31b59b.png)

Haremos click derecho sobre el archivo ".key" y seleccionamos **"Propiedades"**.

![image](https://user-images.githubusercontent.com/104928044/170974728-fa835283-ee18-479d-88b9-22a7c75c0030.png)

Veremos los usuarios que tienen permisos sobre este archivo y nos dirigimos a **"Opciones avanzadas"**.

![image](https://user-images.githubusercontent.com/104928044/170975299-0f657d24-9fdd-4072-b46f-ef0970921cc5.png)

Abajo nos aparecerá un botón en el que nos dice **"Deshabilitar herencia"** pinchamos sobre este y se nos abrirá otra nueva ventana en la que seleccionaremos **"Quitar todos los permisos heredados de este objeto"**.

Ahora en la misma ventana donde ya no nos aparecen todos los usuarios que tenían permisos anteriormente pulsamos sobre **"Agregar"**.

![image](https://user-images.githubusercontent.com/104928044/170976109-baf49ec4-e8bf-491c-a896-ea37cf19a644.png)

![image](https://user-images.githubusercontent.com/104928044/170976194-917cedb5-13ae-49e2-87a6-ce69f0e294a6.png)

Realizamos click sobre **"Seleccionar una entidad de seguridad"** y se nos abrirá una nueva ventana.

![image](https://user-images.githubusercontent.com/104928044/170976708-cd706efa-321d-4b9e-9532-ab9f95310491.png)

Donde se muestra la flecha roja, debemos añadir nuestro usuario de Windows y seleccionar en **"Comprobar nombres"**, si todo está correcto pulsamos sobre aceptar.

Una vez ya tengamos nuestro usuario seleccionado, marcamos con el ratón en la casilla de "Control total", aplicamos y aceptamos en todas las ventanas anteriores.

![image](https://user-images.githubusercontent.com/104928044/170977167-95a6fc89-4350-4395-b249-8830ab9419c3.png)

De nuevo realizamos el intento de conexión como anteriormente explicamos y podemos comprobar que ya tenemos acceso a nuestro servidor mediante nuestro par de claves.

![image](https://user-images.githubusercontent.com/104928044/170977912-7046b161-3b7a-4895-848f-efd99aaecd6b.png)

**[FIN DE LA PARTE QUE PUEDES OMITIR SI NO TE APARECE EL MENSAJE DE ADVERTENCIA]**

## Cambiar acceso de par de claves a un acceso mediante usuario y contraseña (Método mucho más inseguro).

Como temo que muchas de las personas que veréis esta guía vais a preferir este método más tradicional pero más inseguro, os lo voy a intentar explicar de la forma más sencilla posible y segura.

En primer lugar realizamos una actualizacion de nuestros repositorios:

~~~
sudo apt update -y && sudo apt upgrade -y
~~~

He instalaremos **Fail2ban** esta aplicación nos protegerá aquellos puertos que tengamos abiertos ante varios intentos fallidos y que posteriormente serán baneados para evitar posibles ataques de fuerza bruta.

~~~
sudo apt install fail2ban -y
~~~

Nos dirigimos al siguiente directorio en el que tendremos que modificar una serie de parámetros importantes dentro de esta herramienta, aunque es muy personalizable según las necesidades que cada uno vaya a requerir.

~~~
cd /etc/fail2ban
~~~

![image](https://user-images.githubusercontent.com/104928044/170983006-9523ab14-dfb7-43b0-a8c4-5822bc76ad54.png)

Vamos a realizar una copia de seguridad de nuestro archivo de configuración que viene por defecto **"jail.conf"**.

~~~
sudo cp jail.conf jail.backup.conf
~~~

![image](https://user-images.githubusercontent.com/104928044/170983798-ffff2600-4774-4a68-9034-ca7d2926781d.png)

Abrimos el archivo de configuración con el siguiente comando:

~~~
sudo nano jail.conf
~~~

Nos dirigimos al apartado [DEFAULT] y descomentaremos las siguientes líneas (Borrar '#' de delante), os debe de quedar algo así:

![image](https://user-images.githubusercontent.com/104928044/170997353-baa88d9f-d340-4e3d-9972-9f6e5bd25b00.png)

Para guardar esta configuración debemos pulsar **"Control + O" y "Enter"** y para salir **"Control + X"**.

Hemos configurado para que haga un baneo básico gradual, cada cierto numero de equivocaciones será baneado un tiempo que este se prolongará más a cada número de intentos fallidos que realice.

Vamos ahora a configurar nuestro puerto SSH de entrada que no será el que viene por defecto [22] ya que seremos muy propensos a ataques automatizados con ese puerto.

Nos dirigimos al directorio donde encontramos el archivo de configuración de SSH:

~~~
cd /etc/ssh
~~~

![image](https://user-images.githubusercontent.com/104928044/170998583-5274520e-562c-45aa-bede-757c69a0e87f.png)

Abrimos el archivo **"sshd_config"**:

~~~
sudo nano sshd_config
~~~

Una vez se nos despligue este archivo, debemos configurar dos parámetros, uno será el puerto por el que tendremos acceso por SSH y permitir la autenticación mediante contraseña:

Cambiamos el puerto por defecto:

![image](https://user-images.githubusercontent.com/104928044/170999386-e18ca01d-44be-4d6e-aea7-f354d112e689.png)

Permitimos la autenticación por contraseña:

![image](https://user-images.githubusercontent.com/104928044/170999474-5d870967-d3e7-48ff-9434-36351eb3a73d.png)

Para guardar esta configuración debemos pulsar **"Control + O" y "Enter"** y para salir **"Control + X"**.

Es importante antes de aplicar los cambios dar una contraseña al usuario **"ubuntu"** con el comando "passwd" de no darle una contraseña previamente, el usuario no tendrá credenciales y no podremos acceder a nuestro servidor.

~~~
sudo passwd ubuntu
~~~

![image](https://user-images.githubusercontent.com/104928044/171000273-8cde1617-5645-4507-84fc-528b2807b6c4.png)

Debéis saber que aunque cuando escribáis no se os muestre la contraseña realmente estáis escribiendo, es simplemente por seguridad por lo que no se os muestra y pulsáis enter para pasar de nuevo a confirmar la contraseña anteriormente ofrecida.

Reiniciamos y aplicamos los cambios con el comando:

~~~
systemctl restart sshd.service
~~~

![image](https://user-images.githubusercontent.com/104928044/171000897-dd276f51-ab11-4671-b0af-c0d27c4a12dc.png)

Nos pedirá de nuevo la contraseña que le ofrecimos al usuario para confirmar los cambios y listo.

Por último, nos queda abrir el nuevo puerto de entrada por SSH que tendrá nuestro servidor para ellos debemos de irnos a la web de Oracle Cloud en el apartado de **"Recursos informáticos > Instancias > Detalles de la instancia"**:

![image](https://user-images.githubusercontent.com/104928044/171001412-8282002d-6693-42c3-b239-2ca947d4f8bc.png)

Pinchamos sobre el nombre de la **"Subred"** que le tengamos asignada.

![image](https://user-images.githubusercontent.com/104928044/171001887-c655e07f-469e-48c7-996e-fb4b7fb21e27.png)

De nuevo hacemos click sobre **"Default Security List for principal"**.

![image](https://user-images.githubusercontent.com/104928044/171001992-6428ea30-22bf-4ceb-a7ba-4771647617a6.png)
 
 Y añadimos una nueva regla de entrada.
 
 ![image](https://user-images.githubusercontent.com/104928044/171002238-6c61d820-885a-4b3d-af3d-e2ba5f0955c3.png)

![image](https://user-images.githubusercontent.com/104928044/171002526-f8135601-51d1-4641-b106-466825b2a5f0.png)

Guardamos esta regla de entrada y lo que estaremos indicando es que desde cualquier IP por protocolo TCP y con destino al puerto 22422 le permitamos la conexión.

Pero eso no es todo, nos falta algo importante, añadir nuestra regla en la tabla de IP Tables. 

~~~
sudo iptables -I INPUT 6 -m state --state NEW -p tcp --dport 22422 -j ACCEPT
sudo netfilter-persistent save
~~~

De esta forma ya tendríamos todo completado y ya nos debería de permitir el acceso mediante usuario y clave a la hora desde un nuevo CMD realizar la conexión con nuestro servidor de la siguiente manera:

~~~
ssh -p 22422 ubuntu@152.67.71.249
~~~

![image](https://user-images.githubusercontent.com/104928044/171005697-2a843e82-3dc4-4078-9804-5385a77dc997.png)

¡LISTO!

# Instalación de DVSwitch

Comenzamos con lo importante, una vez nos encontremos dentro de de nuestro servidor a través de nuestra ventana CMD, lo primero que debemos realizar es una actualización de nuestros repositorios para ello debemos de ejecutar el siguiente comando:

~~~
sudo apt update -y && sudo apt upgrade -y
~~~

![image](https://user-images.githubusercontent.com/104928044/170979761-70901091-c064-408d-8664-2f6b242e7420.png)

Esta actualización nos demorará varios minutos, tened paciencia.


