Partiendo de la configuración publicada en este [post](https://comunidad.movistar.es/t5/Soporte-Fibra-y-ADSL/Llamadas-externas-con-Asterisk-PJSIP-no-muestran-identificaci%C3%B3n/m-p/4981712) del foro de Movistar, he ampliado la configuración del fichero extensions.conf para poder realizar llamadas a todo el [Plan Nacional de Numeración](https://avancedigital.mineco.gob.es/es-ES/Servicios/Numeracion/Documents/Guia_Numeracion.pdf)

Además he añadido configuración para que las llamadas entrantes se envíen a todas les extensiones internas.

Para adaptar en la configuración a vuestra centralita, basta con sustituir el número 999999999 por vuestro número de teléfono y reiniciar el servicio de asterisk.

Os dejo también [los pasos y comandos](https://github.com/wifreaks/PJSIP-Movistar/blob/main/Instructions) que uso para compilar Asterisk desde código fuente partiendo de una debian básica, que és el método que yo uso para montar cada centralita.




Espero que sea útil para alguien.
