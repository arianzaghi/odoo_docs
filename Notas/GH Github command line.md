> [[Github]]

Tags: 
Status: 
Related: 

___
# GH Github command line

## Conectar cuenta de GitHub

**Iniciamos sesion con nuestra cuenta de GitHub**
> En la terminal del pycharm
```sh
gh auth login
```

**Seguimos el proceso de inicio de sesión**
1. Github.com
2. HTTPS
3. Authenticate with credentials Yes
4. Paste authentication token
![[Pasted image 20250219154603.png]]
## Comando para nueva PR

```sh
gh_new_pr "[HU8898]: Nueva PR"
```

![[Pasted image 20250219155914.png]]

**Que incluye**
- `git add .`
- git commit -m "{{RAMA}}"
- Crea PR con el nombre de la historia
- Si no hay cambios, no despliega el docker `[skip actions]`

