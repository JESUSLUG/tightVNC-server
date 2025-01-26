# Instalación y Configuración de TigerVNC Server con GNOME Desktop

Este repositorio contiene las instrucciones para instalar y configurar TigerVNC Server junto con GNOME Desktop en un entorno Linux. A continuación, se detallan los pasos necesarios para realizar la instalación y configuración.

## Requisitos Previos

- Un sistema operativo Linux (Ubuntu, Debian, CentOS, etc.).
- Acceso de superusuario (sudo) para instalar paquetes.
- Conexión a Internet para descargar paquetes.

## Instalación de TigerVNC Server

1. **Actualizar el sistema:**
   ```bash
   sudo apt-get update
   sudo apt-get upgrade
   ```

2. **Instalar TigerVNC Server:**
   ```bash
   sudo apt-get install tigervnc-standalone-server tigervnc-common
   ```

## Configuración de TigerVNC Server

1. **Configurar la contraseña de VNC:**
   ```bash
   vncpasswd
   ```
   Se te pedirá que ingreses y confirmes una contraseña para el servidor VNC.

2. **Editar el archivo `xstartup`:**
   Crea o edita el archivo `~/.vnc/xstartup` y añade el siguiente contenido:

   ```bash
   #!/bin/sh

   unset SESSION_MANAGER
   unset DBUS_SESSION_BUS_ADDRESS

   [ -x /etc/vnc/xstartup ] && exec /etc/vnc/xstartup
   [ -r $HOME/.Xresources ] && xrdb $HOME/.Xresources

   export XKL_XMODMAP_DISABLE=1
   export XDG_CURRENT_DESKTOP="GNOME-Flashback:Unity"
   export XDG_MENU_PREFIX="gnome-flashback-"

   gnome-session --session=gnome-flashback-metacity --disable-acceleration-check &
   ```

   Guarda y cierra el archivo.

3. **Hacer ejecutable el archivo `xstartup`:**
   ```bash
   chmod +x ~/.vnc/xstartup
   ```

## Instalación de GNOME Desktop

1. **Instalar GNOME Desktop:**
   ```bash
   sudo apt-get install gnome-session-flashback
   ```

   Si prefieres el entorno completo de GNOME, puedes instalar:
   ```bash
   sudo apt-get install ubuntu-gnome-desktop
   ```

## Iniciar el Servicio VNC Server

1. **Iniciar el servidor VNC en el puerto 5900:**
   ```bash
   vncserver :0
   ```

   Esto iniciará el servidor VNC en el puerto 5900. Puedes conectarte a él utilizando un cliente VNC como `TigerVNC Viewer` o `RealVNC`.

2. **Detener el servidor VNC:**
   Si necesitas detener el servidor VNC, puedes usar el siguiente comando:
   ```bash
   vncserver -kill :0
   ```

## Conexión al Servidor VNC

1. **Instalar un cliente VNC en tu máquina local:**
   - [TigerVNC Viewer](https://tigervnc.org/)
   - [RealVNC](https://www.realvnc.com/en/connect/download/viewer/)

2. **Conectar al servidor VNC:**
   - Abre el cliente VNC.
   - Ingresa la dirección IP de tu servidor seguida del puerto `:0` (por ejemplo, `192.168.1.100:0`).
   - Ingresa la contraseña que configuraste con `vncpasswd`.

## Notas Adicionales

- **Firewall:** Asegúrate de que el puerto 5900 esté abierto en el firewall de tu servidor.
- **Autostart:** Si deseas que el servidor VNC se inicie automáticamente al arrancar el sistema, puedes agregar el comando `vncserver :0` a tu archivo de inicio (por ejemplo, `.bashrc` o un script de inicio).

## Soporte

Si encuentras algún problema o tienes alguna pregunta, no dudes en abrir un issue en este repositorio.

---

¡Gracias por seguir esta guía! Esperamos que te sea útil para configurar tu servidor VNC con GNOME Desktop.
