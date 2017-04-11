# Canvis entre les versions 0.2 i 0.3 del paquet Bird-OpenWRT

`Útima actualització/04/17`

* Actualitzacióneral del paquet. Paquet testejat amb l'úa versió Bird Daemon (v1.6.3) amb el Firmware LEDE17.01-RC1
   * Aplicat estil de codi estandarditzat per protegir-lo i millorar-ne la visualitzacióx: ${variable} o $(_comanda_))
   * Millorades les funcionalitats de `Filters` i `Functions` afegint carpetes especialitzades (/etc/bird\*/{filters|functions}). Creat un procéautomàc per fer la migracióaquests fitxers per usuaris utilitzant la versió2
   * Solucionats alguns problemes que es van introduir a la versió2
   * Reafegits els protocols `Pipe` i `Direct` que havien estat deshabilitats a la versió2
   * Eliminades referèies especíques a Bird4/6 i unificats els principals scripts fent ú variables a les crides
   * Millores al Makefile (Ex: mantenir configuració fer un `sysupgrade)
   * Alineat el codi de Bird4 i Bird6 a excepciól protocol OSPF (pendent)
* Millores a la configuracióI (/etc/config/bird\*)
  * Eliminat el codi utilitzat com a exemple a l'anterior versió* Afegida configuracióíca a Bird6 (Router\_ID _0xCAFEBABE_)
* Canvis al script `service` (/etc/init.d/bird\*)
  * Separat codi de transformació configuracióI a Bird en format llibreria de funcions (bird\*-lib.sh) per futures implementacions de tests unitaris automatitzats
  * Eliminat l'ú `service` per l'administraciól servei Bird a favor dels binaris propis
     * `service` no retorna informaciól resultat de l'execució   * `service` no retorna informacióexecució d'error
     * L'úls binaris de Bird permet un control superior de les opcions a executar (ex: especificacióls fitxers utilitzats per al PID o els LOGs) aixíom permet ser executat en segon pla
  * Afegit un sistema de control d'errors i inicialitzaciór millorar la informacióe rep l'usuari en canviar la configuracióiniciar el servei
  * Afegida la creacióun Backup de l'anterior configuracióm a part de l'inici del servei (aquest fitxer s'actualitza cada inici del servei)
  * Afegida funcionalitat `status` per tal d'informar de l'estat d'execuciól servei Bird
  * Afegides funcions `_quiet` per a executar les funcions del servei en format text (utilitzat a la interfíe web - LUCI)
     * Les funcions s'anomenen "_funcióuiet_" (ex: `restart_quiet`)
* Canvis als scripts de l'interfíe web (LUCI)
   * Actualitzat el controlador ("_controller_")
      * Pestanyes reordenades i actualitzat el codi de control
      * Afegides pestanyes de control de l'estat del servei, de visualitzaciól Log del sistema i d'edició `Filters` i `Functions`
    * Pàna d'estat
      * Mostrar l'estat del Servei Bird\* en format text (ú `status_quiet`)
      * Mostra 3 botons per la interacciób el servei Bird\* _start/restart/stop_ (ú `*_quiet`)
    * Pàna de Log `(En desenvolupament)`
      * Mostrar el fitxer Log configurat per Bird\*. Aquesta pàna s'actualitza automàcament cada 5 segons
    * Pàna de `Filters` i `Functions` `(En desenvolupament)`
      * Seleccióun fitxer dels disponibles a /etc/bird\*/{filters o functions}/ o creacióun utilitzant la data com a nom
      * Carrega del fitxer en una area de text per editar-lo
      * Guardat dels canvis fets al fitxer

