# kenos-config

Configuración remota y versiones publicadas de **KenOs** (launcher para Windows).

- `config.json` — la última versión disponible y de dónde descargar su instalador (con su SHA-256).
  Las copias instaladas de KenOs lo consultan al arrancar y cada 6 horas.
- `config.json.sig` — firma Ed25519 (base64) de los bytes exactos de `config.json`. KenOs rechaza
  cualquier configuración que no esté firmada con la clave del autor, así que editar este
  repositorio sin esa clave no afecta a nadie.
- **Releases** — el instalador `KenOs-Setup-<versión>.exe` de cada versión.

No edites `config.json` sin volver a firmarlo: usa `tools\publish_config.ps1` (cambios a mano) o
`tools\publish_release.ps1` (versión nueva) desde el proyecto de la app. `.gitattributes` impide que
git cambie los saltos de línea (rompería la firma).

## Campos de `config.json`

| Campo | Para qué |
|---|---|
| `revision` | Sube en cada cambio; KenOs nunca aplica una revisión más antigua que la que ya vio. |
| `update.version` | Versión publicada (`AAAA.MM.DD` o `AAAA.MM.DD.N`). |
| `update.build` | Número creciente (`2026102301`); KenOs se actualiza si es mayor que el suyo. |
| `update.notes` | Novedades (las ve el usuario en el aviso). |
| `update.assets.win-x64` | `url` (https) del instalador, `sha256` y `size`. |

Lo rellena `tools\publish_release.ps1` al publicar una versión.
