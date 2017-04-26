# Canvis de la versió

`Última actualització 26/04/17`

Bird{4|6}-openwrt v0.3

* Actualització general del paquet. Testejat amb l'última versió de Bird Daemon (v1.6.3) i el Firmware LEDE17.01
   * Aplicat estil de codi estandarditzat per protegir-lo i millorar-ne la visualització: ${variable} o \$(_comanda_))
   * Millorades les funcionalitats de `Filters` i `Functions` afegint carpetes especialitzades (/etc/bird{4|6}/{filters|functions}). Creat un procés automàtic per fer la migració d'aquests fitxers per usuaris de les anteriors versions
   * Solucionats alguns problemes que es van introduir a la versió 0.2
   * Reafegits els protocols `Pipe` i `Direct` que havien estat deshabilitats a la versió 0.2
   * Eliminades referències especíques a Bird4/6 als scripts i unificació dels principals scripts fent ús de variables a les crides
   * Millores al Makefile (Ex: mantenir configuració en fer un `sysupgrade`)
   * Alineat el codi de Bird4 i Bird6 (El protocol OSPF serà incorporat en futures versions)
* Millores a la configuració UCI (/etc/config/bird{4|6})
  * Eliminat el codi utilitzat com a exemple a l'anterior versió
  * Afegida configuració crítica a Bird6 (Router\_ID **0xCAFEBABE**)
* Canvis al script `service` (/etc/init.d/bird{4|6})
  * Separat codi de transformació de la configuració UCI a Bird en format llibreria de funcions (bird{4|6}-lib.sh) en previsió de futures implementacions de tests automatitzats
  * Eliminat l'ús de `service` per l'administració del servei Bird a favor dels binaris propis de Bird
     * `service` no retornava informació del resultat de l'execució
     * `service` no retornava informació d'execució i d'error `stout/stderr`
     * L'ús dels binaris bàsics de Bird permet un control millor de les opcions a executar (ex: especificació dels fitxers utilitzats per al PID o Log del servei) així com permet ser executat en segon pla
  * Afegit un sistema de control d'errors i inicialització per millorar la informació que rep l'usuari en canviar la configuració o iniciar el servei
  * Afegida la creació d'un Backup temporal de l'anterior configuració com a part de l'inici del servei (s'actualitza cada inici del servei amb ```service start```)
  * Afegida funcionalitat `status` per tal d'informar de l'estat d'execució del servei Bird
  * Afegides funcions `_quiet` per executar les funcions del servei en format text (utilitzat a la interfíe web - LUCI)
     * Les funcions s'anomenen "_funció\_quiet_" (ex: `restart_quiet`)
* Canvis als scripts de l'interfície web (LUCI)
   * Actualitzat el controlador ("_controller_")
      * Pestanyes reordenades i actualitzat el codi
      * Afegides pestanyes de l'estat del servei, de visualització del Log del sistema i d'edició de `Filters` i `Functions`
    * Afegida pàgina d'estat
      * Mostra l'estat del Servei Bird{4|6} en format text (ús: `status_quiet`)
      * Mostra 3 botons per la interacció amb el servei Bird\* _start/restart/stop_ (ús: `*_quiet`)
    * Afegida pàgina de Log
      * Mostra el fitxer Log configurat per Bird{4|6}. Aquesta pàgina s'actualitza automàticament cada 5 segons
    * Afegida pàgina de `Filters` i `Functions` 
      * Selecció d'un fitxer dels disponibles a /etc/bird\*/{filters o functions}/ o creació d'un de nou utilitzant la data com a part nom
        * Informació: un cop creat un nou fitxer, s'ha de seleccionar el mateix element ```New File```  de la llista fins que no es refresqui la pàgina
      * Càrrega del fitxer en una area de text per editar-lo
      * Guardat dels canvis fets al fitxer
