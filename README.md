# SystemMethodsRemover
Removes system ($) methods from the codebase. InterSystems Caché utility.

## What it does?

1. Replaces `.$` with `.<something of your choice>` (`.%` by default)
2. Capitalizes the letter after `$`
3. Replaces references from `%Object` to `%DynamicObject` etc

## Use

Import classes and call one of the entry points: 

`s st = ##class(SMR.Main).RemoveFromAllClasses(Replace, Capitalize)` - for all user classes

`s st = ##class(SMR.Main).RemoveFromSubclassesOf(Class, Replace, Capitalize)` - for subclasses

`s st = ##class(SMR.Main).RemoveFromMatchingClasses(Mask, Replace, Capitalize)` - for LIKE SQL

Arguments:

- `Replace` - what to replace `$` with (`%` by default but, for example, you can specify `$$$`)
- `Capitalize` - capitalize the letter after $ (boolean, yse by default)
- `Class` - class which subclasses the utility would try to convert (including the class)
- `Mask` -  passed into the SQL query `SELECT ID FROM %Dictionary.ClassDefinition Where ID LIKE ?`

More docs are in the code docs. The utility works only in a current namespace.

## Requirements

Works in 2016.2 Field Test or later. 

## Docker    

### Prerequisites
Make sure you have [git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git) and [Docker desktop](https://www.docker.com/products/docker-desktop) installed.
### Installation
Clone/git pull the repo into any local directory
```
$ git clone https://github.com/rcemper/PR_SystemMethodsRemover.git
```
to build and start the container run     
```
$ docker compose up -d && docker compose logs -f
```
All ready to be used.   

To open IRIS Terminal do:   
```
$ docker-compose exec iris iris session iris 
USER>
```
or using **WebTerminal**     
http://localhost:42773/terminal/      

To access IRIS System Management Portal   
http://localhost:42773/csp/sys/UtilHome.csp    
