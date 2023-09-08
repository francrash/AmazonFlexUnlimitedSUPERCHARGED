Amazon Flex Ilimitado SOBRECARGADO
Este trabajo está basado en el trabajo realizado por @mdesilva. El repositorio original de Amazon Flex Unlimited
 se puede encontrar en https://github.com/mdesilva/AmazonFlexUnlimited .

SUPERCHARGED actualmente agrega la siguiente funcionalidad al script:

Tabla de contenido
Nuevas funciones en Amazon Flex Unlimited SUPERCHARGED
ntfy.sh Notificaciones
Elija qué notificaciones recibir y qué mensajes imprimir
Corre infinitamente
Detectar CAPTCHA
Intervalo de actualización aleatorio
Detener el script en un momento determinado
Iniciar script en un momento determinado
Parámetros de límite de velocidad
Experimental: método para filtrar los almacenes deseados
Léame original.md
Flexión ilimitada
Automatice la búsqueda y aceptación de trabajos de Amazon Flex Driver
Uso
Solución de problemas
ntfy.sh Notificaciones
A través de la aplicación gratuita ntfy para Android e iOS, el script ahora proporciona notificaciones automáticas.

Configure "ntfyChannel" en config.json en el tema ntfy.sh que creó en su aplicación y sus notificaciones se entregarán allí.

Elija qué notificaciones recibir y qué mensajes imprimir
Es posible personalizar qué notificaciones recibir y qué mensajes imprimir en el terminal.

Modifique la entrada "notificaciones" en config.json para notificaciones o "registro" para lo que se imprimirá.

Las diferentes categorizaciones contienen los siguientes mensajes:

Aviso: Al iniciarse la búsqueda de bloques, la búsqueda de bloques se detiene.
Información: Por cada intento, le indica si encontró una lista y cuántos segundos debe dormir antes de volver a intentarlo.
Éxito: En la aceptación del bloque.
Error: sobre errores y captchas.
Corre infinitamente
Establezca "retryLimit" en 0 en config.json para que el script se ejecute infinitamente. Sólo sale si encuentra un CAPTCHA.

Detectar CAPTCHA
A partir de 2023, Amazon ahora pide a los usuarios sospechosos de bots que confirmen que 
son humanos completando un CAPTCHA en la aplicación Flex. Si el script encuentra esto, le enviará 
una notificación ntfy y cerrará el script por completo.

Intervalo de actualización aleatorio
"refreshInterval" en config.js se ha dividido en dos:

"refreshIntervalMin"
"refreshIntervalMax"
Ambos son flotantes y el tiempo de sueño entre dos intentos se encuentra seleccionando un número aleatorio entre los valores mínimo y máximo.

Detener el script en un momento determinado
Puede forzar que el script se detenga a una hora y un minuto determinados configurando la configuración 
"stopRunAt" en config.json en la hora deseada.

Por ejemplo, si desea que se detenga a las 5:22 p. m., cambie "stopRunAt" de falso a "17:22".
 Tenga en cuenta que si inicia el script después de que haya pasado el tiempo, se detendrá a esa hora del día siguiente.

Si no desea que el script se detenga en un momento determinado, establezca "stopRunAt" en falso.

Iniciar script en un momento determinado
Puede iniciar el script y no hacer que comience la búsqueda de bloques 
hasta una hora y un minuto determinados configurando la configuración "startRunAt" en config.json en la hora deseada.

Por ejemplo, si desea que comience a las 5:22 p. m., cambie "startRunAt" de falso a "17:22". 
Tenga en cuenta que si inicia el script después de que haya pasado el tiempo, comenzará la búsqueda de bloques a esa hora del día siguiente.

Si desea que el script se inicie inmediatamente, establezca "startRunAt" en falso.

Parámetros de límite de velocidad
El mecanismo de prevención de límite de velocidad predeterminado consiste en una pausa de 30 minutos la primera vez que se encuentra el límite de velocidad, luego 30 * la cantidad de veces que se encuentra un límite de velocidad. Cuando esto se ha multiplicado 4 veces (30 * 4 = 120), vuelve a ser 30 minutos.

Cambie "rateLimit.increment" por la cantidad de minutos, "rateLimit.maxTimesIncrement" por la cantidad máxima de veces para multiplicar el incremento antes de volver al incremento * 1.

Entonces, si quiero que solo se detenga durante 15 minutos y solo aumente hasta un máximo de 45 minutos (15 * 3) antes de reiniciar, configuraría la configuración de la siguiente manera:

...
  "rateLimit": {
    "increment": 15,
    "maxTimesIncrement": 3
  }
...
Experimental: método para filtrar los almacenes deseados
La forma en que este script eligió originalmente si se debía considerar una determinada oferta fue enviando las identificaciones de los almacenes deseados al punto final getOffer. En cambio, es posible recuperar todas las ofertas, pero aceptar solo aquellas que tengan la identificación de almacén correcta.

Establezca "filterForWarehouse" en falso para habilitar el nuevo método. Todavía no tiene ninguna influencia real sobre la funcionalidad del script, pero en el futuro podrá proporcionarle una descripción general de las ofertas disponibles y no aceptadas que el script encuentre durante su ejecución.

Léame original.md
Este es el README.md original de @mdesilva.

Flexión ilimitada
Automatice la búsqueda y aceptación de trabajos de Amazon Flex Driver
Este es un intento de automatizar la selección de trabajos de conductor de Amazon Flex. 
Intenté automatizar este proceso para un cliente y funcionó bien. La única advertencia de 
configuración es que debe ejecutar el programa en una máquina conectada a Internet por cable; 
la tecnología inalámbrica no es lo suficientemente rápida para competir con los tontos clickers 
por los que los conductores de Flex se engañan para que paguen ( https://www.cnbc.com/2020/02/09/amazon-flex-drivers-use-bots-to-get -más-trabajo.html). 
Estos clickers requieren que los conductores miren sus teléfonos todo el día y observen cómo el 'fantasma' 
del clicker hace clic en el botón "Actualizar"
 para buscar trabajos, pero a una velocidad 1000x de lo que pueden hacer con sus pulgares. 
 Este es un software estúpido del que sólo los ignorantes caerán; 
 El verdadero software automatiza un proceso completo sin ninguna intervención, 
 conocimiento o conciencia humana continua. Mi objetivo final era que cualquier conductor de 
 Amazon Flex solo levantara su teléfono para HACER los trabajos que este programa aceptaba en su nombre; 
 nunca más tendrían que buscar trabajo.

Nota : Realicé ingeniería inversa en la API de Amazon Flex ejecutando Charles Proxy en mi iPhone
 mientras hacía una variedad de cosas en la aplicación Flex (por ejemplo, iniciar sesión, buscar trabajos,
  aceptar un trabajo, rechazar un trabajo). Puede hacer lo mismo si necesita actualizar la API de ingeniería inversa en este programa.

Descargo de responsabilidad 1 : ejecute este programa bajo su propia responsabilidad. No soy responsable de la cancelación de la cuenta Flex
 ni de las sanciones impuestas por Amazon como resultado del uso de este programa.

Descargo de responsabilidad 2 : intenté ejecutar esto en un servidor AWS y no funcionó, 
posiblemente porque Flex bloquea todas las conexiones entrantes desde los centros de datos 
para evitar la automatización a gran escala. Pero tal vez funcione en centros de datos que no son propiedad de AWS.

Uso
DEBES tener Python 3 instalado. Las versiones inferiores a 3 no funcionarán.
Clone el repositorio en la máquina que utilizará para ejecutar el programa (la máquina debe estar conectada a Internet por cable para 
obtener mejores resultados).
Instale dependencias usando pip : pip install -r requirements.txt.
Establecer username y passworden config.json .
Modifique el resto de config.json para cumplir con sus requisitos de búsqueda de empleo. Ya viene con algunos valores predeterminados. 
Complete desiredWarehousessi 
desea restringir su búsqueda de empleo a ciertos almacenes. Si elige esta opción, desiredWarehousesdebe haber una lista de cadenas de 
identificadores de almacén internos . 
De lo contrario, déjelo desiredWarehousescomo una lista vacía.
Complete el desiredWeekdaysfiltro en config.json si desea restringir su búsqueda de empleo a ciertos días de la semana.
 De lo contrario, puede dejarla desiredWeekdayscomo una lista vacía. desiredWeekdaysdebe ser una lista de cadenas 
 (sin distinguir entre mayúsculas y minúsculas) correspondientes a los días de la semana (es decir, "domingo", "lunes", etc.).
 Cada cadena debe incluir al menos las tres primeras letras del día.
Para determinar los ID de almacén internos de los almacenes para los que es elegible, ejecute el siguiente comando: python3
 app.py getAllServiceAreasOpython3 app.py --w

Aquí obtendrá una tabla de todas las áreas de servicio (almacenes) 
para las que es elegible. La columna de la izquierda indica el nombre del área de servicio 
y la columna de la derecha es la identificación del almacén interno utilizado por Amazon.
 Copie todos los identificadores del área de servicio a los que desea restringir su búsqueda 
 como cadenas en el campo Almacenes deseado en config.json.

p.ej

{
...
"desiredWarehouses": ["9c332725-c1be-405f-87c5-e7def58595f6", "5fa41ec8-44ae-4e91-8e48-7be008d72e8a"]],
...
}
Opcionalmente, configure notificaciones por SMS de aceptaciones de trabajos de Amazon Flex completando los twilioparámetros en config.json .
Corre python app.py. Alternativamente, intente python3 app.py.
Solución de problemas
No se puede autenticar en Amazon Flex. Intente completar el desafío de verificación en dos pasos en (url)
Haga clic en la URL y complete el desafío de verificación en dos pasos. Después de llegar a una página que dice:

¿Buscando algo? Lo lamentamos. La dirección web que ingresó no es una página que funciona en nuestro sitio.

Has completado con éxito el desafío de verificación en dos pasos . Regrese a su terminal y vuelva a ejecutar el programa.