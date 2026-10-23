# tarjetas

Carpeta `tarjetas/` del repositorio [`exitus-innovacion/public-assets`](https://github.com/exitus-innovacion/public-assets). Contiene el diseño, el comportamiento y los prompts de las tarjetas interactivas que usa la skill **exitus-onboarding** de Claude. Se publica aquí para que cada tarjeta cargue este archivo en lugar de escribirlo completo, y así aparezca casi al instante.

**No contiene datos sensibles:** solo estilos, el código de la tarjeta y los prompts de exportación (los mismos que ya están en la skill).

## Archivos

| Archivo | Para qué |
|---|---|
| `tarjetas.js` | Versión legible, para revisar y editar |
| `tarjetas.min.js` | Versión que carga la skill |
| `prueba.html` | Página para probar la tarjeta en un navegador antes de publicar |

## Publicar por primera vez

1. En el repositorio público `exitus-innovacion/public-assets`, crea la carpeta `tarjetas/` en el primer nivel y sube ahí `tarjetas.js`, `tarjetas.min.js`, `prueba.html` y este `README.md`.
2. Copia el **hash completo del commit** (40 caracteres). En GitHub aparece al dar clic en el commit, o con `git rev-parse HEAD`.
3. Arma la URL sustituyendo `HASH` y ábrela en el navegador para confirmar que se ve el archivo:
   ```
   https://cdn.jsdelivr.net/gh/exitus-innovacion/public-assets@HASH/tarjetas/tarjetas.min.js
   ```
4. Pega esa URL en la skill, en `references/tarjetas-abiertas.md`, en la línea `URL_TARJETAS:` de la sección 0 (la que hoy dice `HASH`), y vuelve a empaquetar e instalar la skill.

Mientras la URL de la skill diga `HASH`, la skill sigue funcionando con la versión completa, solo que más lenta.

## Actualizar

1. Edita `tarjetas/tarjetas.js` y regenera la versión minificada desde la carpeta `tarjetas/`:
   ```
   npx terser tarjetas.js -c -m --comments '/^!/' -o tarjetas.min.js
   ```
2. Prueba con `prueba.html`, haz commit y copia el **nuevo** hash.
3. Actualiza la URL en la skill con el nuevo hash.

Cambia también el número de versión en `window.EXITUS.version` y en el encabezado del archivo.

## Reglas de seguridad

- **Usa siempre el hash del commit en la URL**, nunca `@main` ni `@latest`. Con el hash, lo que carga la tarjeta no puede cambiar aunque alguien modifique el repositorio; solo cambia cuando ustedes actualizan la URL en la skill.
- Cualquier archivo nuevo en `public-assets` también será público: revisen bien lo que se sube a ese repositorio.
- Protege la rama `main` (cambios solo por pull request con revisión) y exige verificación en dos pasos a quienes tengan acceso de escritura.
- No agregues datos de clientes, credenciales ni información interna: el repositorio es público.

## Mantener los prompts sincronizados

Los prompts viven en dos lugares: en este archivo (`window.EXITUS.prompts`) y en la skill (`references/importar-memoria.md` y `references/migrar-proyectos.md`). Si cambian uno, cambien el otro en el mismo ajuste.
