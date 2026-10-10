# ClickSales Updates

Repositorio público de distribución de instaladores y metadatos firmados de ClickSales. No contiene código fuente privado ni datos de clientes.

El actualizador de ClickSales solo confía en releases estables con un manifiesto Ed25519 válido para la clave pública integrada en la aplicación. El manifiesto incluye la versión, el tag, el nombre, el tamaño y SHA-512 del instalador.

## Publicar una versión

1. Genera y valida el instalador Windows NSIS desde el repositorio privado `elx19/ClickSales`. Adjunta a un borrador de release de este repositorio `ClickSales-Setup.exe` y el `latest.yml` generado por electron-builder.
2. Comprueba el tag `vMAJOR.MINOR.PATCH`, la versión de `latest.yml`, la arquitectura y el instalador en una máquina limpia.
3. Ejecuta manualmente la acción **Sign and publish stable update** con ese tag. La acción verifica el binario y el metadato NSIS, crea `update-manifest.json` y su firma Ed25519 usando el secreto `CLICKS_UPDATE_PRIVATE_KEY`, los adjunta y publica el release.
4. Verifica la release pública descargándola desde una instalación de QA de la versión anterior. No publiques versiones de producción hasta cerrar las puertas de auditoría del repositorio privado.

El secreto de firma nunca se guarda en este repositorio ni se imprime en los logs. Las releases publicadas son inmutables desde el flujo normal; publica una versión corregida con un número mayor, no reemplaces una ya distribuida.
