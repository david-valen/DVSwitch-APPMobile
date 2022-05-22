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


