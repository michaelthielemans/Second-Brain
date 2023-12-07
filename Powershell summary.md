
# Powershell is geschreven in C# and is object oriented
-> windows itself is also object oriented.
Nieuwe versies van powershell is op .NET core gebasseerd -> ook bruikbaar in linux, mac

voorbeeld.


get-process
-> geeft het resultaat in een table met objecten
 -> deze objecten hebben hun eigen properties
 -> op elk object kunnen methodes uitgevoerd worden.
 
alle objecten samen vormen een collectie

get all methods and properties of a cmdlet
get-member 'cmdlet'

```
get-help
get-command -noun ...
get-command -verb ...
```

#### multiple cmdlets
`get-process; get-service`
