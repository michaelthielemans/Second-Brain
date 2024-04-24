dns server met child domain.

een dns query naar het child domain sturen maar het record staat niet in de zonefile van het childdomain. 
- op child dns een forwarder?
- op child dns een cond forwarder?
- ???


First domain controller in the forest is it a Global catalog by default? 
At least 1 Global Catalog server in the forest.
Best practice = a global catalog on every site in the forest. -> less lookups that have to cross the wan network



repadmin?

leerpad 6
vraag 1

na reboot veranderd: 

voor het toevoegen van een child -> je moet pref dns pointen naar root dns dc, dus niet naar de 127.0.0.1 want hij moet dc 1 AD kunnen vinden om een child toe te voegen aan dat domain.
na het toevoegen van een nieuw domain
zal op die server automatisch na een reboot de dns settings veranderd zijn.
- pref dns is 127.0.0.1
- alt dns zal dan dc1 zijn


keuze van bridgehead server voor replicatie. de KCC zal dit zelf bepalen wie dat is. 
de keuze wordt gemaakt op basis van een algoritme dat beslist op basis 

application partition enkel op domain replicatie. niet forest wide