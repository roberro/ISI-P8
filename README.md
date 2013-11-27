Plataphorma
===========

Meteor pet project created to teach my students the following Meteor functionality: 

* Collection's publish/subscribe 
* Deps.autorun 
* Meteor.methods/call 
* Integration of non-Meteor code in compatibility folder (HTML5 games Alien Invasion and Froot Wars)
* Usage of allow to control client access to collections

![ScreenShot](/screenshot.png)


Plataphorma offers the possibility to run 2 different HTML5 games: Alien Invasion and Froot Wars. 

On the right side of the screen the best players of each game are shown, updated in real time each time a signed in player finishes a game. If no game is selected, the best players overall are shown.

On the left side of the screen a chatroom for the current game is available. Only signed in users can post messages. If no game is selected a general chatroom is shown.

The original code of the two HTML5 games integrated in this project is available here:
* Alien Invasion: https://github.com/cykod/AlienInvasion
* Froot Wars: http://www.wrox.com/WileyCDA/WroxTitle/Professional-HTML5-Mobile-Game-Development.productCd-1118301323,descCd-DOWNLOAD.html

Bootstrap style (file bootstrap.min.css) provided by http://bootswatch.com


Running the project
-------------------

A live version of this code is running here: http://plataphorma.meteor.com

To run the project locally, clone the repo and run ```meteor``` inside it. You can see in .meteor/packages that this Meteor project uses these packages:
* ```meteor remove autopublish```
* ```meteor remove insecure```
* ```meteor add bootstrap```
* ```meteor add accounts-ui```
* ```meteor add accounts-password```

1) Click en boton de juego.
Cuando haces click en uno de los juegos hace visible ese contenedor (donde aparece el juego, el chat y la mejor puntuacion de ese juego) y esconde el otro contenedor. 
Hace una llamada a set con el id del juego para que el servidor inicialize el codigo de ese contenedor.
El servidor carga las 5 mejores puntuaciones de ese juego, los 10 ultimos mensajes.
Una vez que estamos dentro de ese contenedor tenemos ejecutando deps.autorun que nos reejecuta el codigo de ese juego, por si hemos introducido una puntuacion nueva o un mensaje en el chat y lo guarda en el servidor. Ademas tenemos otro deps.autorun que llama a set para actualizar el estado de los mensajes y puntuacion, si lo ha modificado alguien.

2) Se escribe un mensaje chat sin estar autenticado.
Si escribimos un mensaje sin estar autenticados, comprueba que no nos hemos registrado Meteor.userId() y como no estamos registrados, hacemos visible el mensaje que tenemos en la etiqueta "#login-error".

3) Se escribe un mensaje chat estando autenticado.
Comprueba si estamos registrados, cogemos el nombre del usuario que escribe el mensaje Meteor.user()._id y el mensaje $('#message').
Inserta en Messages el Nombre, mensaje, fecha y nombre del juego.

4)	Se termina una partida con puntuacion maxima sin estar autenticado.
Cuando finaliza y manda la puntuacion, comprueba que ha llegado con el nombre de un usuario. Si no llega con nombre no hace nada.

5)	Se termina una partida con puntuacion maxima estando autenticado.
Comprueba que ha llegado con un nombre de usuario, como tiene nombre de usuario, lo inserta en la variable Matches con el nombre de usuario, fecha, puntos y nombre del juego.

6) ¿Que sale en consola cuando te autenticas (sign in)?
Sale el identificador null y luego el de tu usuario.
7)	¿Que sale en la consola cuando te sales (sign out)?
Sale el identificador de tu usuario y luego null.
