# QXRND - PocketMine-MP Pterodactyl Egg

Egg de Pterodactyl para servidores Minecraft Bedrock basados en **QXRND - PocketMine-MP**. Permite seleccionar PM4, PM5 o PM6 mediante la variable `VERSION` durante la instalación.

## Versiones disponibles

| Opción | Repositorio | Runtime | Release actual | Asset |
|---|---|---:|---|---|
| `PM4` | [QXRND/PocketMine-MP-PM4](https://github.com/QXRND/PocketMine-MP-PM4) | PHP 8.1 | [v4.26.0-qxrnd.1](https://github.com/QXRND/PocketMine-MP-PM4/releases/tag/v4.26.0-qxrnd.1) | [`PocketMine-MP.phar`](https://github.com/QXRND/PocketMine-MP-PM4/releases/download/v4.26.0-qxrnd.1/PocketMine-MP.phar) |
| `PM5` | [QXRND/PocketMine-MP-PM5](https://github.com/QXRND/PocketMine-MP-PM5) | PHP 8.2 | [v5.44.5-qxrnd.2](https://github.com/QXRND/PocketMine-MP-PM5/releases/tag/v5.44.5-qxrnd.2) | [`PocketMine-MP.phar`](https://github.com/QXRND/PocketMine-MP-PM5/releases/download/v5.44.5-qxrnd.2/PocketMine-MP.phar) |
| `PM6` | [QXRND/PocketMine-MP-PM6](https://github.com/QXRND/PocketMine-MP-PM6) | PHP 8.3 | [qxrnd-26.44.7](https://github.com/QXRND/PocketMine-MP-PM6/releases/tag/qxrnd-26.44.7) | [`PocketMine-MP.phar`](https://github.com/QXRND/PocketMine-MP-PM6/releases/download/qxrnd-26.44.7/PocketMine-MP.phar) |

PM5 utiliza API 5.44.5, Bedrock 1.26.44 y protocolo 2168. Su PHAR reducido evita errores de espacio durante la descompresión inicial en Pterodactyl.

PM6 corresponde a la distribución **QXRND - PocketMine-MP API 6.0.0**, compatible con Minecraft Bedrock **1.26.44** y protocolo **2168**. Su PHAR está reducido para disminuir el uso de disco durante la descompresión inicial en Pterodactyl.

## Instalación en Pterodactyl

En el panel de Pterodactyl, abre **Nests**, selecciona o crea el nest de Minecraft Bedrock y utiliza **Import Egg** para cargar [`egg-ryxmc.json`](./egg-ryxmc.json). Al crear el servidor, selecciona la variable **Version to install** y elige `PM4`, `PM5` o `PM6`.

La instalación descarga el binario PHP correspondiente, crea la ruta estándar `bin/php7/bin/php` y guarda el PHAR como `PocketMine-MP.phar`. El comando de inicio utilizado por el egg es:

```text
./bin/php7/bin/php ./PocketMine-MP.phar --no-wizard --disable-ansi
```

Si una instalación anterior falló o el servidor conserva un PHAR antiguo, utiliza **Reinstall Server** después de importar la versión actualizada del egg. Cambiar la variable y pulsar **Start** no vuelve a ejecutar el instalador.

## Gamemode shortcuts

PM5 and PM6 include the same quick gamemode commands:

| Command | Gamemode |
|---|---|
| `gma` | Adventure |
| `gmsp` | Spectator |
| `gmc` | Creative |
| `gms` | Survival |

Each shortcut executes the corresponding `gamemode` command for the command sender and uses the normal gamemode permissions.

## Actualizaciones

PM4 y PM5 consultan automáticamente el último release disponible en sus repositorios QXRND y buscan un asset llamado exactamente `PocketMine-MP.phar`. Para actualizar cualquiera de esas ramas, publica un nuevo release con ese nombre de asset.

PM6 utiliza el release fijado por el egg para mantener estable la distribución API 6.0.0 / Bedrock 1.26.44. Después de publicar una nueva versión PM6, actualiza la URL del release en `egg-ryxmc.json` y vuelve a importar el egg.

## Soporte y autoría

El autor del egg y de la distribución es **DevPapo**. Para soporte, escribe a **admin@scon.host** o entra en [Discord](https://discord.gg/qhUXn72rGB).

## Repositorio

El egg completo está disponible en [QXRND/PocketMine-MP-Egg](https://github.com/QXRND/PocketMine-MP-Egg).

> PocketMine-MP y Minecraft son marcas de sus respectivos propietarios. Este proyecto no está afiliado ni aprobado por Mojang.

## Licencia

Consulta el archivo [`LICENSE`](./LICENSE) incluido en el repositorio para conocer los términos aplicables al egg y sus archivos asociados.
