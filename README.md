# Raspberry-pi-4-LCD4inch-Kali-Spanish

LCD4 para Raspberry Pi 4 con Kali

Recientemente compré una Raspberry Pi 4 para jugar con sus nuevas funciones y decidí convertirla en un dispositivo de piratería ético Kali Linux dedicado con un kit de carcasa de pantalla táctil de 4 pulgadas que obtuve de Amazon por un precio bastante bajo.

Configuración del dispositivo con Kali Linux y controladores Dado que las instrucciones lo guían a una imagen prefabricada de Kali Linux que graba en su tarjeta SD y que es una versión anterior de Kali Linux y como no confío en las imágenes prefabricadas, decidí instalar la última versión de Kali Linux. sitio web e instalar los controladores manualmente. Resulta que no es realmente plug and play (como dicen en Amazon).

Después de investigar un poco sobre el dispositivo, me topé con scripts de instalación para estas pantallas que terminan en pánico del kernel cada vez. Agradable.

Luego me topé con este repositorio de Git de un tipo que arregló los scripts originales y alguien que fingió que funcionaba en Kali 2020. Aún así terminé en un pánico de kernel para mí en Kali 2021...

La solución (para mi) para instalar los drivers de pantalla en Kali Linux 2021 Para esto usé: mi Windows, linux or Mac Nmap lector de tarjetas SD y Balena Etcher. Es posible que deba ajustar su subred en consecuencia.

Modificó los pasos un poco más y terminó con esto:

1)Grabe la imagen de disco más reciente del sitio web de Kali Linux en la tarjeta SD (utilicé balenaEtcher con la imagen "kali-linux-2021.1-rpi4-nexmon-64.img.xz")

*** 2)Retire y vuelva a montar la tarjeta SD, copie el archivo config.txt en su computadora.

3)Expulsar la tarjeta SD y ponerla en la raspberry pi

4)Ejecute Nmap para ver sus dispositivos de red actuales (actualice su subred si es necesario): $ sudo nmap -sn 192.168.0.0/24 Si tiene muchos dispositivos conectados y se le hace dificil identificar raspberry pi, va a tener que simplificar su network.

5)Antes de conectar la alimentación USB al Rpi, conecte el cable Ethernet y 6)espere 5 minutos si no tiene otras pantallas adjuntas (como yo) o hasta que reciba un aviso de inicio de sesión si lo tiene

7)Vuelva a ejecutar Nmap, busque el de la Rpi y ssh en él (la contraseña será "kali"): $ ssh kali@your.ip.to.pi 7)Tambien pueden usar putty. Si no lo tiene instalado hay version Windows on ssh.com. Para linux seria: $ sudo apt-get update $ sudo apt-get install -y putty $ putty

8)Instale esta library: $ sudo apt install xserver-xorg-input-libinput

9)Clone este repo: $ git clone https://github.com/danielcshn/LCD-show-kali.git

10)ejecute el script $ LCD-show-kali

11)el mío fue: $ sudo ./MPI4008-show 270 (270 es mode vertical con los USB ports en la parte superior, si lo ponen solo (sudo ./MPI4008-show) sera horizontal con c-type port en la parte superior.)

OK AQUI VIENE EL TRUCO, este paro lo haran cada vez que quieran cambiar la configuracion de su pantalla.

12)cuando le pida "Reboot", presione ctrl+c para detener el proceso y sudo poweroff la Raspberry Pi en su lugar: $ sudo poweroff

13)una vez que la luz ACT (verde) en su Raspberry Pi deje de parpadear, desconecte la alimentación de poder USB

14)retire su tarjeta SD de su Rpi y vuelva a conectarla a su computadora

15)abra el archivo config.txt que se encuentra en el SD card que retiro del Rpi, elimine todo lo que esté arriba de la última sección y reemplácelo con el archivo config.txt original completo que copió anteriormente (paso 2). Reemplacé todo por encima de esto:

If you would like to enable USB booting on your Pi, uncomment the following line.

Boot from microsd card with it, then reboot.

Don't forget to comment this back out after using, especially if you plan to use

sdcard with multiple machines!

16)Expulse la tarjeta SD y vuelva a colocarla en su Raspberry Pi y enciéndala

17)La pantalla debería funcionar junto con el tacto.

--- Bueno aqui les dejo otro LCDs que talves apliquen al suyo ---

2.4” RPi Display (MPI2401):

Driver install:

sudo ./LCD24-show

WIKI:

CN: http://www.lcdwiki.com/zh/2.4inch_RPi_Display EN: http://www.lcdwiki.com/2.4inch_RPi_Display

2.4” RPi Display For RPi 3A+ (MPI2411):

Driver install:

sudo ./LCD24-3A+-show

WIKI:

CN: http://www.lcdwiki.com/zh/2.4inch_RPi_Display_For_RPi_3A+ EN: http://www.lcdwiki.com/2.4inch_RPi_Display_For_RPi_3A+

2.8” RPi Display (MPI2801):

Driver install:

sudo ./LCD28-show

WIKI:

CN: http://www.lcdwiki.com/zh/2.8inch_RPi_Display EN: http://www.lcdwiki.com/2.8inch_RPi_Display

3.2” RPi Display (MPI3201):

Driver install:

sudo ./LCD32-show

WIKI:

CN: http://www.lcdwiki.com/zh/3.2inch_RPi_Display EN: http://www.lcdwiki.com/3.2inch_RPi_Display

MHS-3.2” RPi Display (MHS3232):

Driver install:

sudo ./MHS32-show

WIKI:

CN: http://www.lcdwiki.com/zh/MHS-3.2inch_Display EN: http://www.lcdwiki.com/MHS-3.2inch_Display

3.5” RPi Display(MPI3501):

Driver install:

sudo ./LCD35-show

WIKI:

CN: http://www.lcdwiki.com/zh/3.5inch_RPi_Display EN: http://www.lcdwiki.com/3.5inch_RPi_Display

3.5” HDMI Display-B(MPI3508):

Driver install:

sudo ./MPI3508-show

WIKI:

CN: http://www.lcdwiki.com/zh/3.5inch_HDMI_Display-B EN: http://www.lcdwiki.com/3.5inch_HDMI_Display-B

MHS-3.5” RPi Display(MHS3528):

Driver install:

sudo ./MHS35-show

WIKI:

CN: http://www.lcdwiki.com/zh/MHS-3.5inch_RPi_Display EN:http://www.lcdwiki.com/MHS-3.5inch_RPi_Display

MHS-3.5” RPi Display-B(MHS35XX):

Driver install:

sudo ./MHS35B-show

WIKI:

CN: http://www.lcdwiki.com/zh/MHS-3.5inch_RPi_Display-B EN:http://www.lcdwiki.com/MHS-3.5inch_RPi_Display-B

4.0" HDMI Display(MPI4008):

Driver install:

sudo ./MPI4008-show

WIKI:

CN: http://www.lcdwiki.com/zh/4inch_HDMI_Display-C EN: http://www.lcdwiki.com/4inch_HDMI_Display-C

MHS-4.0" HDMI Display-B(MHS4001):

Driver install:

sudo ./MHS40-show

WIKI:

CN: http://www.lcdwiki.com/zh/MHS-4.0inch_Display-B EN: http://www.lcdwiki.com/MHS-4.0inch_Display-B

5.0” HDMI Display(Resistance touch)(MPI5008):

Driver install:

sudo ./LCD5-show

WIKI:

CN: http://www.lcdwiki.com/zh/5inch_HDMI_Display EN: http://www.lcdwiki.com/5inch_HDMI_Display

5inch HDMI Display-B(Capacitor touch)(MPI5001):

Driver install:

sudo ./MPI5001-show

WIKI:

CN: http://www.lcdwiki.com/zh/5inch_HDMI_Display-B EN: http://www.lcdwiki.com/5inch_HDMI_Display-B

7inch HDMI Display-B-800X480(MPI7001):

Driver install:

sudo ./LCD7B-show

WIKI:

CN: http://www.lcdwiki.com/zh/7inch_HDMI_Display-B EN: http://www.lcdwiki.com/7inch_HDMI_Display-B

7inch HDMI Display-C-1024X600(MPI7002):

Driver install:

sudo ./LCD7C-show

WIKI:

CN: http://www.lcdwiki.com/zh/7inch_HDMI_Display-C EN: http://www.lcdwiki.com/7inch_HDMI_Display-C
