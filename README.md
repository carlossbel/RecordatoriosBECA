# RecordatoriosBECA

Lista de recordatorios compartida en tiempo real entre tú y tu novio. Diseño minimalista en blanco con acentos azul y rojo, con corazones.

## Stack

- HTML + CSS + JS vanilla (sin build, un solo archivo)
- Tipografías de Google Fonts (Fraunces + Geist)
- **Firebase Firestore** para persistencia y sync en vivo
- **Firebase Auth anónima** para asegurar el acceso

## Setup en Firebase Console

Antes de que funcione, hay que habilitar dos cosas en la consola del proyecto `recordatoriosbelcas`:

### 1. Activar inicio de sesión anónimo

**Authentication → Sign-in method → Anonymous → Activar → Guardar**

### 2. Crear la base Firestore y poner las reglas

**Firestore Database → Crear base de datos → Modo producción → Región `nam5` (o la más cercana a México)**

Luego en **Firestore Database → Rules**, pega esto y publica:

```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /reminders/{reminderId} {
      allow read, write: if request.auth != null;
    }
  }
}
```

Esto permite que cualquiera que use la página (y que haya pasado el sign-in anónimo) pueda leer y escribir los recordatorios. Suficiente para una lista entre dos personas.

## Correr local

```sh
python3 -m http.server 8080
# http://localhost:8080
```

También funciona abriendo el `index.html` directo en el navegador (`file://`).

## Desplegar

Es un archivo estático único:

- **GitHub Pages**: Settings → Pages → Source: Deploy from branch → `main` / `(root)`
- **Vercel**: importa el repo desde el dashboard, auto-deploy
- **Netlify**: arrastra la carpeta a app.netlify.com

**Importante**: en Firebase Console → Authentication → Settings → Authorized domains, agrega los dominios donde lo despliegues (`carlossbel.github.io`, `recordatoriosbeca.vercel.app`, etc.) para que la auth funcione.

## Estructura de datos

Collection `reminders`, un doc por recordatorio:

```json
{
  "text": "comprar algo",
  "createdAt": 1730000000000,
  "completed": false,
  "completedAt": null,
  "createdBy": "<uid anónimo>"
}
```
