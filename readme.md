# PRACTICA GIT

## ¿Qué comando utilizaste en el paso 11? ¿Por qué?

En el paso 11 se pide deshacer los cambios del ultimo commit perdiendo los cambios en el working copy, git reset preserva los cambios al no ser que se utilice --hard y HEAD~1 nos mueve al cambio anterior por lo tanto el comando a utilizar es `Git reset --hard HEAD~1`

## ¿Qué comando o comandos utilizaste en el paso 12? ¿Por qué?

En el paso 12 nos piden rehacer el cambio que hemos eliminado en el paso 11, para ello podemos usar `git reflog` para obtener el id del cambio que hemos eliminado.

```
c91ff16 (HEAD -> styled, main) HEAD@{0}: reset: moving to HEAD~1
f37706e HEAD@{1}: commit: Modified: git-nuestro.md 'Added markdown styling'
c91ff16 (HEAD -> styled, main) HEAD@{2}: checkout: moving from main to styled
c91ff16 (HEAD -> styled, main) HEAD@{3}: commit (initial): Add and populate git-nuestro.md with unstyled content
```
 
 Una vez tenemos el id en este caso f37706e podemos usar `git reset --hard f37706e` o `git reset --hard HEAD@{1}` en este caso también podríamos ahorrarnos la utilización de reflog usando `git reset --hard ORIG_HEAD`
 
##  El merge del paso 13, ¿Causó algún conflicto? ¿Por qué?

El merge del paso 13( styled <- main ) no se puede realizar `Already up to date` debido a que styled es parent de main y ya contiene los cambios de este.

## El merge del paso 19, ¿Causó algún conflicto? ¿Por qué?

Si, los archivos contienen cambios en las mismas lineas y git no es capaz de realizar el merge de forma automática requiriendo al usuario solventar los conflictos antes de realizar el commit.


## El merge del paso 21, ¿Causó algún conflicto? ¿Por qué?

No genera conflicto ya que es un merge fast-forward

## ¿Qué comando o comandos utilizaste en el paso 25?

Para dibujar el diagrama se puede utilizar `git log --oneline --all --graph` este sería el resultado:

```
* 78de9b4 (title) Modify: git-nuestro.md 'Added markdown styled title'
*   2fd302c (HEAD -> main, styled) Merge branch 'htmlify' into styled
|\  
| * 215545b (htmlify) Modified: git-nuestro.md 'Convert markdown syntax to html'
* | f37706e Modified: git-nuestro.md 'Added markdown styling'
|/  
* c91ff16 Add and populate git-nuestro.md with unstyled content
``` 

Usando alias y parámetros como `--decorate` y `--format` se pueden obtener outputs personalizados que modifiquen la cantidad y la forma en que se muestra la información, por ejemplo:

![alt text](https://raw.githubusercontent.com/Sergio-Amo/practica-git-1/main/images/step25.png)

## El merge del paso 26, ¿Podría ser fast forward? ¿Por qué?

Si, al no haber bifurcaciones el merge podría haberse realizado simplemente moviendo el puntero de main a title.

##  ¿Qué comando o comandos utilizaste en el paso 27?

Para deshacer los cambios sin perder los cambios del working copy he utilizado `git reset HEAD~1`

##  ¿Qué comando o comandos utilizaste en el paso 28?

Para descartar los cambios en el working copy utilizo `git restore git-nuestro.md` en caso de no estar disponible (versiones antiguas de git) se puede utilizar `git checkout -- git-nuestro.md`

##  ¿Qué comando o comandos utilizaste en el paso 29?

Para eliminar la rama title se usa `git branch -D title`

##  ¿Qué comando o comandos utilizaste en el paso 30?

Como dije anteriormente se puede usar reflog para buscar la ID del commit que queremos recuperar y usar `git reset --hard ID` en este caso voy a optar por usar ORIG_HEAD ya que no se han realizado operaciones que muevan HEAD desde que se deshizo el commit, por lo tanto un `git reset --hard ORIG_HEAD` nos lleva de vuelta al estado cuando el merge fue realizado.


##  ¿Qué comando o comandos usaste en el paso 32?
Para volver al commit inicial podemos usar `reflog` para obtener el id una vez lo tengamos deberemos tener en cuenta cual es nuestro objetivo, si, por ejemplo, solo queremos compilar el proyecto podemos usar `git checkout c91ff16` para movernos en un estado `detached HEAD` al commit inicial.

En otros casos puede ser mejor utilizar `git reset --hard c91ff16`

##  ¿Qué comando o comandos usaste en el punto 33?
Para volver al estado final y tras haberme movido en `detached HEAD` al commit inicial puedo volver a el usando `git checkout main

Si hubiese optado por realizar un `git reset --hard <ID commit inicial>` optaría por utilizar `git reset --hard ORIG_HEAD` o buscaría la id del commit final utilizando `reflog` para posteriormente utilizar `git reset --hard f6e588c`
