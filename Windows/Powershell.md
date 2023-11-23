#powershell #windows
## Version and .NET
- powershell is by default case insensitive
- starting from powershell 6.0 it uses .NET CORE = opensource and platform independend (linux, mac, unix compatible)
- powershell 7.x is now able to run on almost all linux distro's
## Object oriented
Objects are stored in memory as tables.
#### why object oriented?
> - windows itself is object oriented -> easy to communicate with ps
> - working , filtering, formatting, sorting,... objects is easiers than flat text.
> - Less code to write to accomplish the same
> - you can easily perform actions on objects with methods

- object class - the blueprint of an object should look like
- instance = a entity that has been created from an object class 
- methods = things you can **do** with an object
- properties (attributes)
- collection = multiple objects together

example:
> The 'get-process' cmd-let is a function that will return a list of objects with all their properties.
> when executing such command all the object with all their properties will be stored in memory. by default powershell will show you the most interesting properties unless you specify to list a specific property in you command.

#### Retrieving properties from objects

```powershell
(objectname).propertyname
```
- The objectname can be the object / instance that is stored into a variable ($var1).property
- It can be a function that will return one or more objects/instances (gip).property
### get-version of powershell
```powershell
get-host | select-object version
```
## Cmdlet naming conventions

verb-noun -property argument
get-command -totalcount 2

### Wildcards

| symbol | function|
|--|--|
| * | all chars possible unspecified amount|
|\[a-c] | 1 char that can be in the range of chars from a to c |
| ? | exactly 1 random char |


## Help , Search cmdlets  and their methods and attributes
```powershell
get-help get-process -detailed
get-help get-process -online
get-process -?  --> is the same
get-process -? -online
```

```powershell
get-command -verb get -noun proc[e-i]*
get-command -verb ge? -noune ?rocess
```
### get all the methods and properties available on a command
```powershell
get-process | get-member -membertyp property
get-process | get-member -membertyp method
```

## Getting property of one or more object

```powershell
(get-process).starttime
```

``` powershell
$var1=get-process
($var1).starttime
```

```powershell
get-process | foreach-object{$_.starttime}
```

## Edit object with methods

>[!warn] For cmdlets that produce a single object
```powershell
$date = get-date
$date2 = ($date).add-date(2)
```

>[!warn] Using a variable: If the result of the cmdlet provides multiple objects, these objects are seen together as 1 array. This is not always what we want.
```powershell
$var1=get-date
$var1.addays(2)
$var1.gettype()  --> system.Array
```

>[!warn] For cmdlets that produce multiple objects user the FOREACH
```powershell
get-process | ForEach-Object {$_.gettype()}
```

>[!warn] multiple commands
```powershell
get-process; get-service
```
get-process | ForEach-Object {$_.gettype() }
```powershell
get-process | select-object -property name,id -first 5 -last 7
abbriviated notation:
get-process | select-object name,id -first 5 last 7
```

## Filtering and sorting the result: where-object

#### Filtering
```powershell
get-process | where-object {$_.processname -like "*xbox*"}
```

```powershell
Get-DnsClient | ? connectionspecificsuffix
```
> the '' ?  '' will check of the specified column has a value , if so there is output

-ge


#### Sorting
```powershell
get-process | sort-object -descending -> by default ascending is used
```

### Regular expression



## Cmdlets: Files/folders:

| cmdlet | alias |function |
|--|--|--|
| get-childitem | gc | list dir|
|get-location | gl | print working dir |
|set-locatin | sl | change dir cd |
|copy-item | copy | copy file or folder |
|remove-item | del | |
|move-item | move | |
|rename-item | rn | |
|new-item | ni | |
|get-content file.txt| / | show the content of a file|
|add-content file.txt| / | add content to a text file|
|set-content file.txt| / | add and overwrite content of a file|


## Cmdlets: Networking

| cmdlet | descr |
|--|--|
| get-netadapter | get layer 2 info of networkcard|
|get-netipinterface | get layer 3 info of networkinterface |
|get-netipaddress | get all ip configured on system |
|get-netipconfiguraton | alias gip , nice overview of ip config|

### DNS cmdlets
firsts install the dns module in powershell
```powershell
PS C:\> Import Module DnsClient
```

```powershell
Resolve-DnsName -name domainname
Get-DnsClientCache
```

## Cmdlets: Control panel

Get-ControlPanelItem

## Working with API’s and modules

get-module
import-module
find-module -> searching modules from the psgallery online

## Pipelines and formatting

get-process | select-object -property name,handles,...  

```powershell
$list1 = 1,1,1,2,2,2,3,3,3,4,4,4,2,2
$list1 | select-object -unique
```

##### Measuring / counting objects
```powershell
get-childitem | measure-object
get-process | measure-object
```
##### Grouping objects
```powershell
get-process | group company
```
## Aliases
### Built-in aliases
>Get all aliases
```powershell
get-alias
```
> Or other method
```Powershell
ps-drive alias:
get-childitem
```
> for example built in aliases are:
```powershell
get-process = ps
get-childitem = gci
```
### User-defined aliases
>create a new alias
```powershell
set-alias aliasname cmdlet ->can overwrite an existing alias
new-alias aliasname cmdlet ->this will give an error if the alias already exists
```

>[!remark] In order to create an alias of a cmdlet that uses properties you need to create a function for it !

```powershell
set-alias gcg get-command -verb get --> this will not work

function gcg {get-command -verb get}

```

>[!error] After closing the shell the self made alias is no longer available!
>How to solve it?
> Export/import the ALL aliases : builtin + userdefined
>	`export-alias** path filename`
>	`import-alias** -path path`
> 	Export/import only a specific alias
> 	`export-alias -path alias.txt -name aliasname`
> 	Using power-shell profiles

## Profiles
Profile config files are applied from least specific to most specific.

check your current profile
echo $pshome

the standard location of the profile is saved into the variable `$profile

`test-path $profile

create new profile
```powershell
new-item -path $profile -type file -force
```

edit the profile config file with notepad

```powershell
notepad $profile
```

```notepad
#adding new aliases
set-alias gd get-date
```

restart powershell to apply the new profile settings

## Exporting objects/cmdlets

•       Convertto-Html: put the information in html format
•       Convertto-Xml: put the information in xml format
•       Convertto-Csv: put the information in csv format
•       Export-CSV: = the same as Convertto-Csv except that it keeps the Csv strings in a file
•       Out-File: places the information in a file
•       Input item: simulates opening files
## Input and Output:

read-host
write-host
write-output
## Execution policy
```powershell
set-executionpolicy remotesigned


```
## History
get-history

hoofdstuk 12 niet op examen