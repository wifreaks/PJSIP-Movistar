Partiendo de la configuración publicada en este [post](https://comunidad.movistar.es/t5/Soporte-Fibra-y-ADSL/Llamadas-externas-con-Asterisk-PJSIP-no-muestran-identificaci%C3%B3n/m-p/4981712) del foro de Movistar, he ampliado la configuración del fichero extensions.conf para poder realizar llamadas a todo el [Plan Nacional de Numeración](https://avancedigital.mineco.gob.es/es-ES/Servicios/Numeracion/Documents/Guia_Numeracion.pdf)

Además he añadido configuración para que las llamadas entrantes se envíen a todas les extensiones internas.

Para adaptar en la configuración a vuestra centralita, basta con sustituir el número 999999999 por vuestro número de teléfono y reiniciar el servicio de asterisk.

Os dejo también los pasos y comandos que uso para compilar Asterisk desde código fuente partiendo de una debian básica, que és el método que yo uso para montar cada centralita:

# Clono el repositorio de código fuente de Asterisk
cd /usr/local/src/
sudo git clone https://github.com/asterisk/asterisk.git

# Instalación de dependencias
cd asterisk/
sudo contrib/scripts/install_prereq install
sudo apt-get install unixodbc unixodbc-dev libmyodbc python-dev python-pip python-mysqldb
sudo apt-get install build-essential libncurses5-dev uuid-dev libjansson-dev libxml2-dev libsqlite3-dev
sudo apt-get install  libncurses5-dev uuid-dev libjansson-dev libxml2-dev libsqlite3-dev

# Compilación de código fuente y primer arranque de Asterisk
sudo ./configure --with-pjproject-bundled
make menuselect
sudo make menuselect
sudo make install
sudo make samples
sudo make config
make install-logrotate
asterisk -gvc
sudo asterisk -gvc
sudo systemctl start asterisk
sudo systemctl status asterisk

# Guardo una cópia de los ficheros de configuración de muestra y escribo los nuevos con mi configuración
cd /etc/asterisk/
sudo mv /etc/asterisk/pjsip.conf /etc/asterisk/pjsip.conf.sample
sudo vim.tiny /etc/asterisk/pjsip.conf
sudo mv /etc/asterisk/extensions.conf /etc/asterisk/extensions.conf.sample
sudo vim.tiny /etc/asterisk/extensions.conf

# Reiniciar servicios y verificar
sudo systemctl restart asterisk
sudo systemctl status asterisk
sudo asterisk -r



Espero que sea útil para alguien.
