# PenaltyGuard · LigaSAN

Prototipo de consulta del Reglamento General Unificado de la Liga Deportiva Barrial Cochapamba Norte. React + TypeScript + Vite + Tailwind CSS + React Router + Lucide. Sin servidor, cuentas ni base de datos.

## Ejecutar

Requiere Node.js 22 o superior y pnpm 11 (o npm).

```sh
pnpm install
pnpm dev
```

Con npm: `npm install` y `npm run dev`. Abre la dirección que imprime Vite.

## Comprobar y compilar

```sh
pnpm test
pnpm build
pnpm preview
```

La compilación genera `dist/`. `pnpm-workspace.yaml` permite únicamente el script de instalación de esbuild. El archivo de bloqueo fija las versiones instaladas.

## Fuente y estructura

- `public/reglamento.pdf`: copia íntegra del PDF proporcionado (51 páginas).
- `public/escudo.png`: imagen institucional extraída de la portada y convertida de JPEG2000 a PNG.
- `data/pages.json`: extracción por página con pypdf; conserva el texto para auditar.
- `src/reglamento.json`: 90 artículos numerados y 3 bloques de preámbulo/disposiciones. Incluye capítulos, secciones, tipo, número y páginas de origen. Numeración del anexo independiente y artículos con letras conservados. Los artículos 62 y 63 conservan su derogación.
- `tests/reglamento.test.mjs`: verifica numeración, unicidad, cobertura línea por línea, orden del texto y fundamentos disciplinarios.

Solo se eliminan números de página independientes y espacios al final de línea. Las cabeceras estructurales se conservan como metadatos. El texto normativo no se sustituye por resúmenes. Los saltos de línea y los espacios internos proceden del PDF. Las tablas se muestran como texto extraído; para su maquetación oficial, usa el PDF. La auditoría de cobertura no sustituye una revisión editorial institucional.

Las explicaciones de sanciones y FAQ son ayudas de lectura diferenciadas del texto original. No se presentan explicaciones de todos los artículos como validadas por la Liga. La sanción concreta requiere revisar circunstancias, agravantes, fases definitivas y el procedimiento aplicable.

## Funcionalidades

Inicio; lector por capítulos; artículos expandibles; anterior/siguiente; enlaces directos; copia de enlace; favoritos; búsqueda con normalización de tildes y filtro de capítulo/tema; sanciones con filtros de sujetos y tipo; FAQ con categorías; PDF original; menú móvil; tema claro/oscuro. Favoritos y preferencias se guardan localmente. Los enlaces `art-35` y `anexo-1` distinguen los dos bloques normativos.

## Publicar en Netlify

1. Ejecuta `pnpm install`, `pnpm test` y `pnpm build`.
2. En Netlify, crea un proyecto mediante despliegue manual y carga la carpeta `dist/` (incluye `_redirects` para rutas React).
3. Si conectas un repositorio: comando `pnpm build`, directorio de publicación `dist`, Node 22 o superior.
4. Comprueba `/reglamento/art-35` entrando directamente y `/reglamento.pdf`.

## Publicar en Vercel

1. Sube el código a un repositorio propio e impórtalo en Vercel.
2. Selecciona Vite, comando `pnpm build`, directorio `dist`, Node 22 o superior.
3. Se incluye `vercel.json` con rutas SPA y acceso a archivos estáticos.
4. Ejecuta el despliegue y verifica los enlaces directos y el PDF.

Publicado en producción: https://penaltyguard-ligasan.netlify.app/

Repositorio: https://github.com/Torrecitaz/PenaltyGuard

Netlify está conectado a la rama `main` y ejecuta `pnpm build`, publicando `dist/`. Los cambios enviados a `main` generan despliegues automáticos. Panel: https://app.netlify.com/projects/penaltyguard-ligasan/overview

Despliegue inicial verificado: commit `184dea9145ffe0b3d83c3d520fbbbaa2bb51fa22`.

## Alcance

Herramienta informativa. El texto oficial prevalece. No registra sanciones, emite resoluciones, tramita impugnaciones, cobra pagos ni integra SADCAF. No usa IA generativa ni servicios pagos. No hay autenticación. El texto del PDF es una fuente de datos, no instrucciones ejecutables.
