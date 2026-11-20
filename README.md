# Banco de Blackboard → Excel

Página **estática y autocontenida** (`docs/index.html`, un solo archivo) que convierte los ZIP exportados de bancos de preguntas de Blackboard
al Excel con las columnas `tema, ra, question, option_a..d, answer, explanation, image (no tocar)`.

Todo ocurre en el navegador del usuario: los archivos no se suben a ningún servidor, así que sirve tal cual en GitHub Pages.

## Uso
1. Abre la página y arrastra uno o varios ZIP de Blackboard.
2. Revisa el RA (se propone del título del banco) y el tema (solo el número) de cada banco.
3. «Descargar Excel».

## Publicar en GitHub Pages
Sube el repositorio → *Settings → Pages* → «Deploy from a branch» → rama `main`, carpeta `/docs`.
No subas ZIP ni exportaciones de Blackboard (el `.gitignore` ya los excluye).

## Desarrollo
El repositorio publicado solo contiene `docs/index.html` y este README; el código fuente, el build y las pruebas viven en local (están en `.gitignore`).

- El código fuente es `src/index.src.html` (HTML + CSS + JS). No edites `docs/index.html` a mano.
- `uv run python build.py` regenera `docs/index.html` incrustando JSZip 3.10.1 (se descarga una vez de cdnjs al construir; la página final no usa red).
- Prueba con una exportación real (ZIP o carpeta descomprimida):
  `uv run python tests/test_html.py ruta/al/ZIP_o_carpeta`
  (requiere Microsoft Edge; compara el Excel del navegador con `tests/lector_blackboard.py`, una lectura de referencia en Python).

## Formato soportado
Bancos de preguntas (pool QTI de Blackboard) de opción múltiple con 2 a 4 opciones y una sola correcta. Las demás preguntas se omiten con un aviso.
La explicación se toma de la retroalimentación de la respuesta correcta, si existe.
