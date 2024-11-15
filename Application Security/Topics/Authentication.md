
De programmeur kan best een fixed tijd of delay in de inlog procedure zetten
best elke login request even lang laten duren. Het is mogelijk indien men tracht in te loggen met een onbestaande user dat de database query sneller is uitgevoerd doen wanneer de user login name wel correct is maar het wachtwoord fout. Dan moet ook het wachtwoord gecontrolleerd worden dus dit kan langer duren.

Dus controleren hoe lang het duurt wanneer er een response word terug gestuurd
als de login fout is moet het systeem het wachtwoord niet controleren en dus sneller een response. 
de response neemt toe als de username correct is maar het wacht woord toch fout.