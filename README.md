
# Balena RPI Radio
<img src=".img/pacifico.club.jpg" width="100" height="100">

Este proyecto levanta una radio en un Raspberri Pi usando balena.io para orquestrar 5 servicios en un docker-compose.
- icecast (el que hace el stream) https://icecast.org/
- mpd (el que toca las canciones) https://wiki.archlinux.org/index.php/Music_Player_Daemon
- proxy (el balanceador que sale por el puerto 80) http://www.haproxy.org/
- sima (el dj) https://kaliko.me/mpd-sima/
- ympd (la intefaz visual) https://ympd.org/

## Que hacer si quiero pasar música a Pacifico.club
0. Ingresar a https://console.cloud.google.com/apis/library/drive.googleapis.com y verificar si esta habilitada el app de google drive. Puede ser necesario que crees una cuenta y un proyecto en google cloud.
1. debes obtener un token de google drive desde google. Ingresa en esta web https://developers.google.com/oauthplayground, selecciona select & authorize apis > Drive API v3 > https://www.googleapis.com/auth/drive > click en AUTHORIZE API, luego debes elegir con cual perfil seguir. Cualquiera sirve ;)
![alt text](.img/45789039-3567-4b79-bd1d-632cca2cb1f8.png)

2. Luego en el step 2 hacer click en el boton “Exchange authorization code for token”, y en la respuesta de la derecha copiar el valor de access_token, este lo usaremos como token para conectarnos con gdrive
![alt text](.img/90fc7ab3-dffb-4f1d-b121-2688baf8791a.png)

3. Con el token ya puedes acceder al dashboard de balena y seleccionar el unico device bajo la app pacifico-club, deberas buscar el terminal al costado inferior derecho y seleccionar mpd para abrir sesion
![alt text](.img/2772c823-ff92-4cb4-be99-7505b0c62fe0.png)

4. Agrega música al dispositivo

5. Desde YMPD (http://ympd.8151fa637af0a1247e7e55337f53e140.balena-devices.com) se debe clickear UPDATE DB y luego play a algún tema, así veras los temas desde ympd
![alt text](.img/628186e7-346f-4c83-b4a5-e27a850d038a.png)


## ¿Que hacer si YMPD no se puede conectar MPD
Debes reiniciar MPD desde balena.io

## ¿Que pasa si todo falla?
Revisar la conección de internet, si todo falla se puede crear una instancia desde 0 (ver abajo)

## Crear un nuevo device en balena
crear carpetas en mpd
```
mkdir -p /var/lib/mpd/playlists && mkdir -p /var/lib/mpd/database
```
darles los permisos necesarios
```
chmod g+w /var/lib/mpd/music /var/lib/mpd/playlists /var/lib/mpd/database
```
pasar música desde google drive al dispositivo
```
cd /var/lib/mpd/music
./gdrive download --recursive —skip {DRIVE_FOLDER_ID} --access-token {DRIVE_API_TOKEN}
````

## Creditos
Este proyecto es mantenido por Nicolas Justiniano y Pablo Rubio

