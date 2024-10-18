geen azure op het examen.

aws platform met documentatie en labs blijft maar een half jaar open.

voor de opdracht moet er tijdens het aanmaken van de service een dedicated subnet gekozen worden.


openstack is een opensource 




## project pe2

config.py

maak een rds en je an daar een connection string opvragen, deze kan je dan in de docker environment variable meegeven.
via task definition de environment vaiariables meegeven
### wsgi servers
web server gateway interface, it handles incoming http request and sends them to the python application

- gunicorn
	- gunicorn app:app
	- gunicorn help


of 

met een python bassed container moet er nog een wsgi server geinstalleerd worden in de container. Dit is omdat flask niet geoptimaliseerd is voor http request handling. het is een wsgi server die dit wel kan. 

nginx als basis container gebruiken en dan de gunicorn mod installeren. Kijk of python hierop staat. daarna kan de code op 

x-forwarder moet ook wanneer je een loadbalancer gebruikt.