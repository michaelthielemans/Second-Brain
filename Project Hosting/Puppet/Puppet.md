puppetclient <-> server architecture
agent <-> master
client -> push naar server

- declarative language for expressing system configuration
Tel how to system config should like like
NOT how or what has to be changed.

SSL communication between master en agent
-> need for certificates
-> ip address, hostname, certificate name moet correct zijn.




Agent stuurt periodiek FACTS naar de puppet master.

Master stuurt CATALOG naar puppet-client




manifest files zijn in declarative language en zijn de recepten hoe er iets moet uitzien.