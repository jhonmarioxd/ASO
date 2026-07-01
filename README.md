# Portal Renacer — Sitio estático (sin login)

Este sitio muestra automáticamente los PDFs que pongas en la carpeta `pdfs/`,
usando el archivo `documentos.json` como índice. No necesita servidor,
base de datos ni inicio de sesión.

## Estructura de carpetas

```
/
├── index.html
├── documentos.json
└── pdfs/
    ├── acta-04-2026.pdf
    ├── acta-05-2026.pdf
    └── ...
```

## Cómo agregar un documento nuevo

1. Copia el archivo PDF dentro de la carpeta `pdfs/`.
   - Usa un nombre de archivo sin espacios ni tildes, por ejemplo:
     `acta-05-2026.pdf`
2. Abre `documentos.json` y agrega un nuevo bloque al inicio del arreglo,
   con una coma separando los bloques:

```json
{
  "id": "acta-05-2026",
  "title": "Acta No 05 - Reunión Ordinaria de Junio",
  "desc": "Resumen de los acuerdos tomados en la reunión ordinaria del mes.",
  "date": "15 Jul 2026",
  "file": "acta-05-2026.pdf"
}
```

   - `id`: identificador único (no repetir entre documentos). Se usa para
     guardar los comentarios de ese documento.
   - `title` / `desc` / `date`: lo que se muestra en la tarjeta.
   - `file`: el nombre exacto del archivo dentro de `pdfs/`.

3. Guarda el archivo y publica los cambios (commit + push si usas GitHub
   Pages, o simplemente sube los archivos si usas otro hosting estático).
   El documento aparecerá automáticamente en la lista, sin tocar el código.

## Comentarios

Los comentarios que la gente escribe se guardan únicamente en el
navegador de cada persona (localStorage). No se comparten entre
visitantes ni se suben a ningún servidor. Si más adelante quieres que
los comentarios sean compartidos por todos (visibles para cualquiera),
se necesitaría una base de datos en la nube (por ejemplo Firebase), lo
cual es un cambio distinto a este modo simple sin login.

## Probar el sitio en tu computador

Los navegadores bloquean por seguridad la carga de `documentos.json`
cuando abres `index.html` directamente con doble clic (protocolo
`file://`). Para probarlo localmente, levanta un servidor simple desde
esta carpeta:

```bash
python3 -m http.server 8000
```

y abre `http://localhost:8000` en el navegador.

Esto **no** afecta a GitHub Pages ni a otros hostings, donde el sitio
funciona normalmente porque sirve los archivos por `http(s)://`.

## Publicar en GitHub Pages

1. Sube esta carpeta completa (incluyendo `pdfs/` y `documentos.json`)
   a tu repositorio de GitHub.
2. En la configuración del repositorio, activa GitHub Pages apuntando
   a la rama y carpeta donde están estos archivos.
3. Cada vez que agregues un PDF nuevo siguiendo los pasos de arriba,
   solo tienes que volver a subir (commit + push) los cambios.
