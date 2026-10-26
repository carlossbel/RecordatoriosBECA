# RecordatoriosBECA

Lista de recordatorios minimalista en blanco, azul y rojo. Un solo archivo (`index.html`), sin dependencias de build.

## Stack

- HTML + CSS + JS vanilla
- Tipografías de Google Fonts (Fraunces + Geist)
- Persistencia en `localStorage` del navegador
- Sincronización automática entre pestañas del mismo navegador

## Correr local

Abre `index.html` directamente en el navegador, o sirve la carpeta:

```sh
python3 -m http.server 8080
# http://localhost:8080
```

## Desplegar

Como es un archivo único, cualquier hosting estático funciona:

- **GitHub Pages**: Settings → Pages → Deploy from branch → `main` / `/root`
- **Vercel**: `vercel --prod` desde la raíz
- **Netlify**: arrastrar la carpeta a app.netlify.com

## Nota sobre sincronización

En esta versión cada navegador tiene su propia lista (`localStorage`). Para compartir la lista entre dispositivos o personas hay que cambiar la capa de datos a un backend (Firebase, Supabase, etc.).
