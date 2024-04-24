#windows #powershell 
# Powershell written in C# and is object oriented
-> windows itself is also object oriented.
New powershell is build upon .NET core -> ook bruikbaar in linux, mac

### Object oriented structure:

get-process
-> geeft het resultaat in een table met objecten
-> deze objecten hebben hun eigen properties
-> op elk object kunnen methodes uitgevoerd worden.
 
alle objecten samen vormen een collectie

### How to get all the methods and properties of a cmdlet
-> get-member <name_of_cmdlet>

```
get-help
get-command -noun ...
get-command -verb ...
```

#### Running multiple cmdlets at once.
`get-process; get-service`

## filtering

get-process | where-object {$_.processname -like "*xbox*"}

### sorting

get-process | sort-object -descending
## Selecting properties
 
