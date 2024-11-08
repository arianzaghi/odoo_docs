> [[git_client_mirror.sh]]

Tags: 
Status: 
Related: 

___

# Error en Client Mirror - Commit borrado

Si ocurre que tenemos en un cliente un commit de un modulo que ha sido eliminado de github, al hacer el client mirror se quedará parado a mitad
```bash
./git_client_mirror.sh coralim.txt
HEAD is now at bf1ba7f Translated using Weblate (Swedish)
HEAD is now at 8dd9a8f Translated using Weblate (Swedish)
HEAD is now at d71318d Translated using Weblate (Italian)
HEAD is now at d653d27 Translated using Weblate (Italian)
HEAD is now at e73826e7 Translated using Weblate (Italian)
HEAD is now at 3cb4f2a Added translation using Weblate (Italian)
HEAD is now at 27748ff Translated using Weblate (Swedish)
HEAD is now at e375b13c [BOT] post-merge updates
HEAD is now at 0ae718c Translated using Weblate (Italian)
HEAD is now at a7ee6de Translated using Weblate (Swedish)
HEAD is now at 47c0618 [ADD]: generic_security_restriction
HEAD is now at 25a351b [HU44659]: MIG_base_uncontrolled_pnt (#6)
HEAD is now at 9738dd9 Translated using Weblate (Italian)
HEAD is now at f4cd8ac [BOT] post-merge updates
HEAD is now at a7ee6de Translated using Weblate (Swedish)
HEAD is now at 671aa63 Translated using Weblate (Italian)
HEAD is now at 8cfb5f4 Translated using Weblate (Spanish)
HEAD is now at c60b8ee [BOT] post-merge updates
HEAD is now at d1728b4 [BOT] post-merge updates
HEAD is now at 9fd43cb Translated using Weblate (Italian)
HEAD is now at 3e0a372 Translated using Weblate (French)
```

## Pasos

### 1. Localizar la dependencia que falla
Tenemos que buscar en `client.txt` la línea que va después de la que nos ha dado el fallo, en nuestro caso: `3e0a372`
```bash
community-data-files:d1728b403ae4fa5e496a158a18665bb458369074
connector:9fd43cb133c918320bce21fcf647320cc5b094fa
contract:3e0a37242a43a679fcc09685ae32aadacfec0edb
core:b770d0490faeee281cbfcd3ab683b9cd37f57b85 # ESTA LINEA DA PROBLEMA
credit-control:0d2c1ca892f5438d9f45f88c17847c83033c3456
```

### 2. Buscamos el repo clonado en nuestro equipo que da fallo

```bash
ssh corali
```