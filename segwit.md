<p align="center">
  <img src="img_segwit/220px-Segwit.svg.png?raw=true" alt="Logo Segwit"/>
</p>
Este documento cuenta la historia de segwit (testigo segregado), desde su concepción hasta su activación 

#### Comienzos
Segwit fue desarrollado en ["The Elements Project"](https://github.com/ElementsProject/elementsproject.org "The Elements Project") con Pieter Wuille ([@pwuille](https://twitter.com/pwuille "Pieter Wuille")) como investigador principal, su implementación en Bitcoin suponía un hard fork, posteriormente Luke Dashjr ([@LukeDashjr](https://twitter.com/LukeDashjr "Luke Darshjr")) propuso la forma de implementarlo como soft fork y tras esto se preparó el BIP para integrarlo en Bitcoin.

#### ¿Qué es segwit?
Segwit es una actualización del protocolo Bitcoin que modifica la estructura de las transacciones, guarda toda la información susceptible de ser maleable en un nuevo campo "witness data". El id de la transacción se calcula sin contar con este campo por lo que posteriormente no se puede modificar.

<p align="center">
  <img src="img_segwit/transaction.png?raw=true" alt="Transacción Segwit"/>
</p>


#### Propuesta Diciembre 2015 ([bip141](https://github.com/bitcoin/bips/blob/master/bip-0141.mediawiki "BIP141"))

Segwit fue propuesto mediante un BIP (Bitcoin Improvement Proposals) por Eric Lombrozo ([@eric_lombrozo](https://twitter.com/eric_lombrozo "Eric Lombrozo")), Johnson Lau ([@johnsonlau01](https://twitter.com/johnsonlau01 "Johnson Lau")) y Pieter Wuille ([@pwuille](https://twitter.com/pwuille "Pieter Wuille"))

Es un soft fork, es decir, los clientes no actualizados pueden coexistir con las versiones actualizadas.

La descripción de segwit se divide en 5 BIP:
 - [BIP141](https://github.com/bitcoin/bips/blob/master/bip-0141.mediawiki "BIP141") - Activado el 24 de Agosto de 2017
   - Descripción general
 - [BIP142](https://github.com/bitcoin/bips/blob/master/bip-0142.mediawiki "BIP142") - Reemplazado por el BIP143
   - Describe el formato nativo de las direcciones de pay-to-witness-public-key-hash (P2WPKH) y pay-to-witness-script-hash (P2WSH).
 - [BIP143](https://github.com/bitcoin/bips/blob/master/bip-0143.mediawiki "BIP143") - Activado el 24 de Agosto de 2017
   - Entra en detalle en la verificación de transacciones en segwit y como resuelve el crecimiento cuadrático del hash de firmas.
 - [BIP144](https://github.com/bitcoin/bips/blob/master/bip-0144.mediawiki "BIP144") - Activado el 24 de Agosto de 2017
   - Trata el cambio en los mensajes de red provocados por segwit.
 - [BIP145](https://github.com/bitcoin/bips/blob/master/bip-0143.mediawiki "BIP145")
   - Cubre los cambios en la llamada JSON-RPC *getblocktemplate* al cliente bitcoin core.

#### [Mejoras](https://bitcoincore.org/en/2016/01/26/segwit-benefits/ "Mejoras Segwit (en)")
  - Soluciona la maleabilidad de las transacciones. ([¿En qué consiste la maleabilidad?](https://bitcointalk.org/index.php?topic=465427.msg5145366#msg5145366 "Maleabilidad de las transacciones"))
  - Aumenta el tamaño del bloque a 4MB en situación ideal, sobre los 2MB en condiciones normales.
  - Facilita la inclusión de nuevos opcodes o modificación de los existentes mediante versionado de scripts. 
  - Facilita el desarrollo de soluciones de segunda capa.
  - Escalado lineal de las operaciones sighash. La cantidad de datos sobre los que se calcula el hash o comprueba la firma crece cuadráticamente el número de inputs no segwit de una transacción. ([The Megatransaction: Why Does It Take 25 Seconds?](http://rusty.ozlabs.org/?p=522 "La Megatransacción"))
  - Firma de los input. Anteriormente los input no se firmaban lo que suponía un problema para las carteras hardware que tenían que buscar las cantidades de los input en los output gastados con el tiempo que eso supone. 
  - Mayor seguridad en multifirma con P2SH
  - Reduce el crecimiento de los UTXO (Salidas de transacciones no gastadas)

#### Críticas
  - Jeff Garzik ([@jgarzik](https://twitter.com/jgarzik "Jeff Garzik")) consideró insuficiente a SegWit como solución de escalado.
  - Mike Hearn, desarrollador principal del cliente [Bitcoin XT](https://bitcoinxt.software/ "Bitcoin XT") calificó a SegWit como "un truco contable", [dejó el desarrollo de Bitcoin poco después](https://blog.plan99.net/the-resolution-of-the-bitcoin-experiment-dabb30201f7).
  - Jonathan Toomim, desarrollado del cliente [Bitcoin Classic](https://bitcoinclassic.com/ "Bitcoin Classic") comentó que SegWit era "feo y raro", sugirió que sería mejor implementarlo como hard fork.
  - Peter Todd ([@peterktodd](https://twitter.com/peterktodd "Peter Todd")) tenía sus dudas en particular en lo respectivo a minería. [[1](https://petertodd.org/2016/segwit-consensus-critical-code-review#peer-to-peer-networking)] [[2](https://www.mail-archive.com/bitcoin-dev@lists.linuxfoundation.org/msg03178.html)]

#### Entorno
Mientras SegWit se desarrollaba en la comunidad Bitcoin había tensiones en cuanto al tamaño del bloque (1MB), varios mineros y compañias Bitcoin encabezados por Bitcoin Classic preparaban un hard fork para aumentar el tamaño a 2 MB. [[1]](https://web.archive.org/web/20160129090054/https://bitcoinclassic.com/ "HF 2MB") 

El 21 de Febrero de 2016 en una reunión en Hong Kong entre varios desarrolladores de Bitcoin Core, operadores de agrupaciones mineras y miembros de la industria Bitcoin para discutir el problema de escalabilidad se llegó a un acuerdo conocido como ["El acuerdo de la mesa redonda de Bitcoin"](https://medium.com/@bitcoinroundtable/bitcoin-roundtable-consensus-266d475a61ff "El acuerdo de la mesa redonda de Bitcoin"), ese acuerdo consistió en estos puntos:
  - SegWit se está desarrollando como soft fork y se lanzará en los próximos 2 meses.
  - Se trabajará públicamente junto a toda la comunidad de desarrolladores del protocolo Bitcoin en un hard fork basado en las mejoras de SegWit. Los desarrolladores de Bitcoin Core tendrán una implementación de dicho hard fork para presentar 3 meses después del lanzamiento de SegWit.
  - Este hard fork incluirá características que se están tratando como aumentar el tamaño de los datos no testigos (non witness) a los 2 MB y sólo será adoptado si hay un acuerdo de la mayoría la comunidad Bitcoin.
  - Los mineros utilizarán SegWit cuando el hard fork se implemente en el cliente Bitcoin Core.
  - Solo se utilizarán sistemas compatibles con el consenso de Bitcoin Core que contendrán SegWit y el hard fork.
  - Se seguirán investigando tecnologías para usar el espacio en los bloques más eficientemente como las firmas [Schnorr.](https://bitcoinmagazine.com/articles/the-power-of-schnorr-the-signature-algorithm-to-increase-bitcoin-s-scale-and-privacy-1460642496/ "Firmas Schnorr")

Meses más tarde, en Julio de 2016 tuvo lugar una [reunión](https://bitcoinmagazine.com/articles/bitcoin-miners-and-developers-meet-in-california-to-improve-communications-1470158657/ "Reunión Julio") entre desarrolladores de Bitcoin Core y operadores de agrupaciones mineras en California. Los desarrolladores de Bitcoin Core salieron de la reunión convencidos de que SegWit sería activado por los mineros.

#### Lanzamiento
SegWit se incluyó en la versión 0.13.1 del cliente [Bitcoin Core](https://github.com/bitcoin/bitcoin "Bitcoin Core"), también se implementó en otros clientes como [Knots](https://github.com/bitcoinknots/bitcoin "Bitcoin Knots") o [Bcoin](https://github.com/bcoin-org/bcoin "Bcoin")

Para activar SegWit se utilizó un método llamado ["VersionBits"](https://github.com/bitcoin/bips/blob/master/bip-0009.mediawiki "BIP9") diseñado para minimizar interrupciones en la red. El 95% de los mineros tenían que señalizar su conformidad para que SegWit se activara en la red Bitcoin. Esta señalización iba a comenzar el 15 de Noviembre de 2016.

Se animó a los usuarios a que actualizaran el cliente lo que hicieron la mayoría. 

Todo apuntaba a que SegWit se activaría en breve, pero no fue así.

Varios de los participantes de la reunión de Hong Kong [cambiaron de opinión](https://bitcoinmagazine.com/articles/the-status-of-the-hong-kong-hard-fork-an-update-1479843521/ "Cambios de opinión").

Un hard fork significa que el protocolo que se es válido deja de serlo tras el momento del hard fork, los desarrolladores ven un peligro en este tipo de actualización y es que todos los clientes deben ir a la nueva versión si hay usuarios que no están de acuerdo pueden quedarse en la versión "vieja" del protocolo y provoca una bifurcación. Para evitar esto se propuso un ["soft-hardfork".](https://petertodd.org/2016/forced-soft-forks "soft-hardfork")

Lo malo del soft-hardfork era que se podía aplicar sin que los usuarios pudieran hacer nada, les obligaba a seguir las normas aunque no estuvieran de acuerdo o crear una nueva red. Para evitar esta situación los desarrolladores buscaban la manera de tener confirmación por parte de la comunidad de Bitcoin. Para ello se propusieron 2 soluciones basadas en los bitcoin que controlaban los usuarios, estas soluciones se llamaron "señalización con moneda" (coin-signaling). La primera de las soluciones permitía a los usuarios agregar un dato en las transacciones señalizando su conformidad con el fork, si todas las transacciones durante un periodo de tiempo señalizaban el fork se consideraba que la comunidad lo aprobaba. La segunda solución en la que estuvo trabajando [Peter Todd](https://twitter.com/peterktodd "Peter Todd") permitía a los usuarios mostrar su posición sin necesidad de realizar transacciones, lo explicó [en su blog.](https://petertodd.org/2016/hardforks-after-the-segwit-blocksize-increase)

La señalización de apoyo a Segwit por parte de los mineros era escasa y el consorcio minero chino [F2Pool](https://www.f2pool.com/ "F2Pool") hizo un movimiento que varios desarrolladores [consideraron una ruptura de acuerdo](https://www.reddit.com/r/btc/comments/47dbeh/f2pool_why_not_take_a_cue_from_slush_and_offer/d0chqph/ "Ruptura de acuerdo").

[Jihan Wu](https://twitter.com/JihanWu "Jihan Wu") co-CEO de Bitmain dijo que sólo activaría SegWit si se hacía el hardfork de aumento del tamaño del bloque, otros consorcios como F2Pool, HaoBTC o bitcoin.com [tampoco señalizaron el apoyo](https://bitcoinmagazine.com/articles/where-bitcoin-mining-pools-stand-on-segregated-witness-1480086424/) a SegWit.

#### [UASF (User Activated Soft Fork)](http://www.uasf.co/ "User Activated Soft Fork")
En Febrero de 2017 [shaolinfry](https://twitter.com/shaolinfry "shaolinfry") propuso [[1]](https://www.mail-archive.com/bitcoin-dev@lists.linuxfoundation.org/msg04703.html "Propuesta UASF")[[2]](https://bitcointalk.org/index.php?topic=1805060.0 "Propuesta UASF") una activación provocada por los nodos completos, la mayoría económica.

Shaolinfry propuso cambiar el estándar de activación de soft fork que hasta ese momento era la activación por poder de cómputo a una activación provocada por todos los usuarios. 

Una activación de soft fork por parte del usuario tendría un "día de comienzo de activación" en el que los nodos comenzarían a forzar la activación en una fecha posterior, si la mayoría económica forzase dicha activación haría que la minería le siguiera.

La idea empezó a coger fuerza y cuando [Samson Mow](https://twitter.com/Excellion "Samson Mow") montó [un fondo de recompensas](https://twitter.com/excellion/status/844349077638676480) parecía que la propuesta se convertiría en realidad.

#### ASICBOOST
La primera semana de Abril de 2017 [Gregory Maxwell](https://github.com/gmaxwell) explicó que había encontrado [ASICBOOST](https://themerkle.com/what-is-asicboost/ "ASICBOOST") implementado en algunos chip de minado, esta tecnología daba una ventaja en el minado a estos chip. SegWit haría incompatible esta manera de utilizar ASICBOOST. Bitmain [admitió](https://blog.bitmain.com/en/regarding-recent-allegations-smear-campaigns/) que había implementado esta tecnología patentada en sus chip, aunque dijo no utilizarla en la red de producción de Bitcoin. 

Esta noticia generó mayor interés por parte de la comunidad en activar SegWit.

#### [BIP148](https://github.com/bitcoin/bips/blob/master/bip-0148.mediawiki "BIP148")
La propuesta de UASF se discutió en un [canal creado para ello en el slack de Bitcoin Core](https://bitcoincore.slack.com/ "Slack Bitcoin Core") y shaolinfry propuso el [BIP148](https://github.com/bitcoin/bips/blob/master/bip-0148.mediawiki "BIP148").

La propuesta no tuvo mucho éxito, ninguno de los mayores exchanges se unieron y se oyeron [opiniones en contra](https://twitter.com/spair/status/852160130296762369) como la del CEO de [bitpay](https://bitpay.com/ "bitpay") [Stephen Pair](https://twitter.com/spair "Stephen Pair").

[Gregory Maxwell](https://github.com/gmaxwell) también dijo que el BIP148 [le parecía una mala idea](https://lists.linuxfoundation.org/pipermail/bitcoin-dev/2017-April/014152.html).

Parecía que UASF había fracasado pero alguien comenzó a trabajar en una alternativa: [BIP149](https://github.com/bitcoin/bips/blob/master/bip-0149.mediawiki "BIP149")

#### El acuerdo de Nueva York
El debate sobre el aumento del tamaño del bloque continuaba, otro cliente, [Bitcoin Unlimited](https://www.bitcoinunlimited.info/ "Bitcoin Unlimited"), que apoyaba incrementar el tamaño mediante un hardfork se hizo popular entre la minería, con el apoyo de Bitmain todo indicaba que se iba a realizar el hard fork.

Por esta razón [Barry Silbert](https://twitter.com/barrysilbert "Barry Silbert") organizó una reunión aprovechando el evento ["Consensus 2017"](https://www.coindesk.com/events/consensus-2017/ "Consensus 2017"), se invitó a gente de la industria Bitcoin incluyendo minería, pero no desarrolladores de Bitcoin Core. 

El resultado de esta reunión se conoce como ["el acuerdo de Nueva York"](https://medium.com/@DCGco/bitcoin-scaling-agreement-at-consensus-2017-133521fe9a77) en el que los participantes se comprometieron a una solución que satisfacía a la parte que quería un hard fork y a la parte que quería SegWit. Basada en una idea de [Sergio Demian Lerner](https://twitter.com/SDLerner "Sergio Demian Lerner") la propuesta fue la siguiente:
 - Activar SegWit cuando más del 80% de los bloques señalen con un 4 en el bit. 
 - Activar el hardfork que aumenta a 2MB el tamaño del bloque tras 6 meses.
[No todo el mundo estuvo de acuerdo con esta reunión](https://en.bitcoin.it/wiki/Segwit_support), estas condiciones eran incompatibles con lo propuesto por los desarrolladores Bitcoin Core cuyo código ya estaba en la mayoría de los nodos de los usuarios.

Mientras, BIP148 había perdido mucho soporte en favor del BIP149 pero no todo el mundo había renunciado al UASF. 

La propuesta de shaolinfry incluía la posibilidad de abortar la activación de SegWit si una mayoría no la aceptaba antes de una fecha concreta pero un grupo de usuarios tenía otra idea. Gente como [Luke Dashjr](https://twitter.com/LukeDashjr "Luke Darshjr")) estaban [considerando la posibilidad ](https://www.reddit.com/r/Bitcoin/comments/6c55t4/lukejr_miners_can_do_bip148_masf_or_users_will_do/) de activar el soft fork independientemente del apoyo. 

Sobre mediados de Mayo, [Alphonse Pace](https://twitter.com/alpacasw "Alphonse Pace") publicó [este artículo](https://bitcoinmagazine.com/articles/op-ed-user-activated-soft-forks-and-intolerant-minority/) sobre la "minoría intolerante", estar teoría presupone que incluso una minoría económica podría hacer que los mineros activaran SegWit ya que sino perderían parte de sus usuarios innecesariamente.

Tras esto y alimentado por el escándalo AsicBoost, el BIP148 empezó a ganar adeptos, se comenzó a calificar al 1 de Agosto como ["El día de la independencia de Bitcoin".](https://twitter.com/excellion/status/869106641290973184)

El problema era el BIP148 era incompatible con "el acuerdo de Nueva York". 

Fue [James Hilliard](https://twitter.com/james_hilliard) ingeniero de [Myrig](https://myrig.com/) el que propuso una solución como BIP, el [BIP91](https://github.com/bitcoin/bips/blob/master/bip-0091.mediawiki "BIP91") que haría compatibles todas las opciones. Mientras la mayoría de los mineros activasen este BIP antes del 1 de Agosto, todos los nodos formarían parte de la misma red. Había poco tiempo ya que la propuesta fue a finales de Mayo, pero [Jeff Garzik](https://twitter.com/jgarzik "Jeff Garzik")) se comprometió a sacar el cliente con esta propuesta implementada semanas antes del 1 de Agosto.

#### La activación

A mediados de Julio la minería Bitcoin [había perdido la primera fecha límite del BIP148](https://bitcoinmagazine.com/articles/bitcoin-miners-miss-first-bip-148-deadline/) lo que puso nervioso al mercado, posiblemente provocada por este nerviosismo la minería comenzó a señalizar su apoyo al BIP91 y el 20 de Julio se fijó para activarse 2 días más tarde.

Con BIP91 fijado sólo era cuestión de tiempo que lo hiciera SegWit, esto ocurrió el 9 de Agosto. Bitcoin activaría SegWit 2 semanas más tarde. 

###### Fuentes:
 - [The long road to SegWit](https://bitcoinmagazine.com/articles/long-road-segwit-how-bitcoins-biggest-protocol-upgrade-became-reality/ "The long road to SegWit")
 - [SegWit explicado](https://es.cointelegraph.com/explained/segwit-explained "SegWit explicado")
 - [Segregated Witness: a fork too far](https://medium.com/the-publius-letters/segregated-witness-a-fork-too-far-87d6e57a4179 "Segregated Witness: a fork too far")
 - [Segregated witness and deploying it for Bitcoin](https://prezi.com/lyghixkrguao/segregated-witness-and-deploying-it-for-bitcoin/ "Segregated witness and deploying it for Bitcoin")
 - [Segwit in Bitcoin: Lessons Learned (PDF)](https://scalingbitcoin.org/milan2016/presentations/D2%20-%201%20-%20Greg%20Sanders.pdf "Segwit in Bitcoin: Lessons Learned")
 - [The Elements Project: Segregated Witness](https://www.elementsproject.org/elements/segregated-witness/ "The Elements Project: Segregated Witness")
 - [UASF.co](http://www.uasf.co/ "UASF")
 - [Bitcoin miners miss the first BIP 148 "deadline"](https://bitcoinmagazine.com/articles/bitcoin-miners-miss-first-bip-148-deadline/ "Bitcoin miners miss the first BIP 148 deadline")
 - Presentación de SegWit de Pieter Wuille ([@pwuille](https://twitter.com/pwuille "Pieter Wuille"))."Scaling Bitcoin", Hong Kong 14-Dic-2015 [-VIDEO-](https://www.youtube.com/watch?v=NOYNZB5BCHM)
 - [What is ASICBOOST?](https://themerkle.com/what-is-asicboost/ "What is ASICBOOST?")
 - [Op Ed: Here's Why All Rational Miners Will Activate SegWit Through BIP148](https://bitcoinmagazine.com/articles/op-ed-heres-why-all-rational-miners-will-activate-segwit-though-bip148/ "Op Ed: Here's Why All Rational Miners Will Activate SegWit Through BIP148")
 - [UASF BIP148 Scenarios and Game Theory](https://medium.com/@jimmysong/uasf-bip148-scenarios-and-game-theory-9530336d953e "UASF BIP148 Scenarios and Game Theory")
 - [Why I support BIP148](https://medium.com/@elombrozo/why-i-support-bip148-4b4c0a9feb4d "Why I support BIP148")
