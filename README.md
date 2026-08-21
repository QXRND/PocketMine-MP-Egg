# PocketMine-MP Pterodactyl Egg

Egg de Pterodactyl para servidores Minecraft Bedrock basados en PocketMine-MP. Incluye PM4, PM5 y PM6; PM6 utiliza la compilación personalizada de RyxMC.

## Versiones disponibles

La variable `VERSION` permite seleccionar:

- `PM4`: instala el canal PM4 oficial.
- `PM5`: instala el canal estable oficial.
- `PM6`: instala la compilación personalizada RyxMC para Bedrock 26.44/protocolo 2168.

## Importación

En el panel de Pterodactyl, abre **Nests**, selecciona o crea el nest de Minecraft Bedrock y usa **Import Egg** para cargar `egg-ryxmc.json`.

Después selecciona la variable `Version to install` al crear el servidor. Para la versión personalizada usa `PM6`.

## Soporte

El autor del egg es **DevPapo**. Para soporte, escribe a **admin@scon.host** o entra en [Discord](https://discord.gg/qhUXn72rGB).

## Nota sobre PM6

PM6 descarga el PHAR desde el release personalizado de [QXRND/PocketMine-MP](https://github.com/QXRND/PocketMine-MP/releases/tag/ryxmc-26.44) y utiliza el binario PHP PM5 compatible con el runtime personalizado de PMMP.
