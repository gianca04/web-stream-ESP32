# ESP32-CAM Web Server Example

## Introducción
Este proyecto utiliza la placa AI Thinker ESP32-CAM para crear un servidor web que transmite video en tiempo real. El código está diseñado para inicializar la cámara, conectarse a una red WiFi y servir el stream de video en el puerto `81/stream`.

## Requisitos
- Placa AI Thinker ESP32-CAM.
- Arduino IDE instalado.
- Cable USB para programación.
- Credenciales de red WiFi.

## Configuración del Arduino IDE
1. **Instalar soporte para ESP32:**
   - Abre Arduino IDE.
   - Ve a `Archivo > Preferencias`.
   - En el campo "URL adicionales para gestor de tarjetas", agrega:
     ```
     https://dl.espressif.com/dl/package_esp32_index.json
     ```
   - Haz clic en "OK".
   - Ve a `Herramientas > Placa > Gestor de tarjetas`.
   - Busca "esp32" e instálalo.

2. **Seleccionar la placa:**
   - Ve a `Herramientas > Placa` y selecciona `AI Thinker ESP32-CAM`.

3. **Configurar opciones adicionales:**
   - Configura las siguientes opciones en el menú `Herramientas`:
     - `Upload Speed`: 115200.

4. **Cargar el código:**
   - Conecta la placa ESP32-CAM al ordenador mediante un adaptador USB a serial.
   - Abre el archivo `CameraWebServer.ino` en Arduino IDE y haz clic en el botón de "Subir" para cargar el código.
   - Presiona los botones `RST` y `FLASH` simultáneamente.
   - Cuando el código empiece a compilar, suelta el botón `RST`.
   - Una vez que el código empiece a subir, suelta el botón `FLASH`. Durante este proceso, deberías ver una luz azul en la placa.
   

## Uso del servidor web
1. **Conectar a la red WiFi:**
   - Al iniciar el ESP32-CAM, se te pedirá ingresar el SSID y la contraseña de tu red WiFi mediante el monitor serie.

2. **Acceder al stream:**
   - Una vez conectado, el ESP32-CAM mostrará su dirección IP en el monitor serie.
   - Abre un navegador web y accede a:
     ```
     http://<direccion_ip>:81/stream
     ```
   - Aquí podrás ver el stream de video en tiempo real.

## Documentación del código
### Configuración de la cámara
El archivo `CameraWebServer.ino` contiene la configuración de la cámara y el servidor web. Algunos puntos importantes:
- **Configuración de la cámara:**
  - Se utiliza el formato de píxel `PIXFORMAT_JPEG` para el streaming.
  - La calidad JPEG se ajusta según la disponibilidad de PSRAM.
- **Ajustes del sensor:**
  - Si el sensor es OV3660, se ajusta la saturación, brillo y orientación.
- **Puerto del stream:**
  - El stream de video se sirve en el puerto `81/stream`.

### Conexión WiFi
El código solicita el SSID y la contraseña de la red WiFi mediante el monitor serie.

### Servidor web
El servidor web se inicializa con la función `startCameraServer()` y utiliza la dirección IP local del ESP32-CAM.

## Notas adicionales
- Asegúrate de seleccionar la partición adecuada en el menú de herramientas para evitar problemas de memoria.
- Si tienes problemas de conexión, verifica las credenciales de WiFi y la configuración de la placa.

## Exponer el stream a Internet
Para exponer el stream de video a Internet, puedes utilizar la herramienta `ngrok`. Sigue estos pasos:

1. **Instalar ngrok:**
   - Descarga e instala `ngrok` desde su sitio oficial: [https://ngrok.com/](https://ngrok.com/).

2. **Ejecutar ngrok:**
   - Abre una terminal y ejecuta el siguiente comando:
     ```
     ngrok http 192.168.250.145:81
     ```
     Asegúrate de reemplazar `192.168.250.145` con la dirección IP local de tu ESP32-CAM.

3. **Obtener la URL pública:**
   - Una vez que `ngrok` esté ejecutándose, te proporcionará una URL pública que puedes compartir para acceder al stream desde cualquier lugar.

### Nota importante
- Solo puede haber un cliente conectado al stream en un momento dado. Si otro cliente intenta conectarse, el stream podría interrumpirse.
- Asegúrate de que tu red WiFi permita conexiones externas y que el ESP32-CAM esté configurado correctamente.
