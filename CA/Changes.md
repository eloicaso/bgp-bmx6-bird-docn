# Canvis entre les versions 0.2 i 0.3 del paquet Bird-OpenWRT

`Útima actualització/04/17`

* Actualització general del paquet. Paquet testejat amb l'última versió de Bird Daemon (v1.6.3) amb el Firmware LEDE17.01-RC1
   * Aplicat estil de codi estandarditzat per protegir-lo i millorar-ne la visualització: ${variable} o $(_comanda_))
   * Millorades les funcionalitats de `Filters` i `Functions` afegint carpetes especialitzades (/etc/bird\*/{filters|functions}). Creat un procés automàtic per fer la migració d'aquests fitxers per usuaris de les anteriors versions
   * Solucionats alguns problemes que es van introduir a la versió 0.2
   * Reafegits els protocols `Pipe` i `Direct` que havien estat deshabilitats a la versió 0.2
   * Eliminades referències especíques a Bird4/6 als scripts i unificació dels principals scripts fent ús de variables a les crides
   * Millores al Makefile (Ex: mantenir configuració en fer un `sysupgrade`)
   * Alineat el codi de Bird4 i Bird6 a excepció del protocol OSPF (pendent)
* Millores a la configuració UCI (/etc/config/bird\*)
  * Eliminat el codi utilitzat com a exemple a l'anterior versió
  * Afegida configuració crítica a Bird6 (Router\_ID _0xCAFEBABE_)
* Canvis al script `service` (/etc/init.d/bird\*)
  * Separat codi de transformació de la configuració UCI a Bird en format llibreria de funcions (bird\*-lib.sh) en previsió de futures implementacions de tests unitaris automatitzats
  * Eliminat l'ús de `service` per l'administració del servei Bird a favor dels binaris propis
     * `service` no retorna informació del resultat de l'execució
     * `service` no retorna informació d'execució i d'error `stout/stderr`
     * L'ús dels binaris bàsics de Bird permet un control superior de les opcions a executar (ex: especificació dels fitxers utilitzats per al PID o la localització del Log) així com permet ser executat en segon pla
  * Afegit un sistema de control d'errors i inicialització per millorar la informació que rep l'usuari en canviar la configuració o iniciar el servei
  * Afegida la creació d'un Backup temporal de l'anterior configuració com a part de l'inici del servei (s'actualitza cada inici del servei)
  * Afegida funcionalitat `status` per tal d'informar de l'estat d'execució del servei Bird
  * Afegides funcions `_quiet` per executar les funcions del servei en format text (utilitzat a la interfíe web - LUCI)
     * Les funcions s'anomenen "_funció\_quiet_" (ex: `restart_quiet`)
* Canvis als scripts de l'interfície web (LUCI)
   * Actualitzat el controlador ("_controller_")
      * Pestanyes reordenades i actualitzat el codi
      * Afegides pestanyes de l'estat del servei, de visualització del Log del sistema i d'edició de `Filters` i `Functions`
    * Afegida pàgina d'estat
      * Mostra l'estat del Servei Bird\* en format text (ús: `status_quiet`)
      * Mostra 3 botons per la interacció amb el servei Bird\* _start/restart/stop_ (ús: `*_quiet`)
    * Afegida pàgina de Log `(En desenvolupament)`
      * Mostra el fitxer Log configurat per Bird\*. Aquesta pàgina s'actualitza automàticament cada 5 segons
    * Afegida pàgina de `Filters` i `Functions` `(En desenvolupament)`
      * Selecció d'un fitxer dels disponibles a /etc/bird\*/{filters o functions}/ o creació d'un de nou utilitzant la data com a part nom
      * Càrrega del fitxer en una area de text per editar-lo
      * Guardat dels canvis fets al fitxer
