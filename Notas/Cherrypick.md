> [[Programación sin docker]]

Tags: 
Status: 
Related: 

___

# Cherrypick

> Lo utilizamos para pasar commits de una rama a otra
> (Se usa cuando no tenemos docker)

1. Comprobamos los commits que corresponden a nuestra rama

```sh
git log --oneline | grep HU50684
8febe81 [HU50684]: Programa de puntos
124d8e5 [HU50684]: Programa de puntos
3bd90f5 [HU50684]: Programa de puntos
```

2. Pasamos a la rama a la que queremos añadir nuestros commits

```sh
git checkout {{BRANCH}} && git pull
```

3. Hacemos el cherry pick indicando los commits de ABAJO a arriba

> [!DANGER] IMPORTANTE
> Poner los commits de abajo a arriba

```sh
git cherry-pick 3bd90f5 124d8e5 8febe81
```

4. Unimos los commits en un solo commit

```sh
	git rebase -i HEAD~{{NUM_COMMITS}}
```

5. Dejamos la primera linea como está (primer commit) y al resto de commits les cambiamos `pick` por `f`
	- pick 12312321
	- f 123213321
	- f 123213213

1. Subimos cambios al repo

```sh
git push
```