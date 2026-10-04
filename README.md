# JSON-CDN-EDENV

CDN de videos de los paquetes SCORM de la **Escuela de Enfermería del Valle (EdenV)**, línea de la fábrica Griky
Genius. Mismo sistema que `griky-org-scorm-cdn` (scorm-forge, `SPEC_CDN_VIDEO_SCORM_PORTABLE.md`).

Los SCORM no traen los videos adentro: cada video es una **clave** y el paquete, al abrirse en el LMS, descarga
`mapeo_videos.json` desde GitHub Pages, busca su clave y arma `https://player.vimeo.com/video/<id>`. Si la clave
no está, el estudiante ve «Contenido en fase de post-producción. Disponible próximamente.».

**Registrar o cambiar un video = editar este JSON.** Los SCORM ya entregados no se vuelven a subir.

## URL (congelada — no cambiar)

```
https://julianjj5.github.io/JSON-CDN-EDENV/mapeo_videos.json
```

Requiere GitHub Pages activo en la rama `main`, carpeta raíz (Settings → Pages).

## Clave de cada video (contrato congelado)

```
clean("EdenV") _ clean(nombre del curso) _ clean("Modulo N") _ clean(título de la sección en el SCORM)
```

`clean()`: sin tildes, minúsculas, espacios → `_`, solo `[a-z0-9_]`, sin `_` repetidos ni en los extremos.
Ejemplo: `edenv_atencion_en_salud_a_victimas_de_violencia_sexual_modulo_1_video_de_complemento_teorico_1_de_2`.

Una vez entregado un SCORM, sus claves no se renombran nunca.

## Cómo se actualiza

No se edita a mano: lo genera el orquestador de EdenV desde `cursos/<curso>/vimeo.yaml`:

```bash
python personalizacion/multimedia/videos_cdn.py mapeo cursos/<curso> --out ../JSON-CDN-EDENV/mapeo_videos.json
```
