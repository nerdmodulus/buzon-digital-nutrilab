[Uploading README.md…]()
# buzon-digital-nutrilab# NutriLab · Buzón "Resuelve tu duda"

Formulario estático para GitHub Pages + backend en Google Apps Script que avisa por correo al equipo docente.

```
index.html        el formulario (esto va a GitHub)
assets/           los dos logos
Codigo.gs         el backend (esto va a Apps Script, NO a GitHub)
```

## 1. Publicar el backend (5 minutos)

1. Entra a [script.google.com](https://script.google.com) con la cuenta que enviará los correos y crea un proyecto nuevo.
2. Borra lo que trae y pega el contenido de `Codigo.gs`.
3. Ejecuta la función **`prueba`** una vez. Google te pedirá autorización: acepta. Te debería llegar un correo de ejemplo a las cuatro casillas.
4. **Implementar → Nueva implementación → Aplicación web**, con:
   - Ejecutar como: **Yo**
   - Quién tiene acceso: **Cualquier usuario**
5. Copia la URL que termina en `/exec`.

## 2. Conectar el formulario

En `index.html`, línea del principio del `<script>`:

```js
const ENDPOINT = "PEGA_AQUI_LA_URL_DEL_APPS_SCRIPT";
```

Reemplaza el texto por tu URL `/exec`.

## 3. Subir a GitHub Pages

Sube `index.html` y la carpeta `assets/` al repositorio, y activa Pages en
**Settings → Pages → Branch: main / root**. En un par de minutos queda en
`https://<usuario>.github.io/<repo>/`.

> `Codigo.gs` no necesita estar en el repositorio. Si lo subes, no pasa nada:
> no contiene claves, solo los correos del equipo.

## Cómo llegan los correos

| El estudiante elige | Asunto | Qué ve el equipo |
|---|---|---|
| Para todo el curso | 💬 Duda para el curso · NutriLab | Banda amarilla, aviso de que es anónima y que se responde en el taller |
| Solo para mí | 🔒 Duda personal · responder a *correo* | Banda roja con el correo destacado; al apretar **Responder** en Gmail la respuesta va directa al estudiante |

## Ajustes que quizás quieras hacer

- **Cambiar destinatarios:** la lista `ADMINS` al inicio de `Codigo.gs`.
- **Dejar registro:** crea una hoja de cálculo, copia su ID desde la URL y pégalo en `SHEET_ID`. Sirve como evidencia para el informe VCM. Las dudas anónimas se guardan sin correo.
- **Límite de Gmail:** 100 correos al día en cuenta personal, 1.500 en cuenta institucional. De sobra para el taller.
- **Volver a implementar:** cada vez que edites `Codigo.gs` hay que hacer *Implementar → Gestionar implementaciones → editar → Versión: nueva*. Si no, sigue corriendo la versión antigua.

## Dos decisiones de diseño

**El anónimo es anónimo de verdad.** Cuando el estudiante elige "para todo el curso", el formulario no envía correo ni ningún identificador, y el backend no registra IP. Vale la pena decírselo en voz alta en la sesión: es lo que hace que se atrevan a preguntar.

**El formulario avisa que no hay diagnósticos.** Abajo del botón hay una nota que deriva a un adulto de confianza o a la dupla psicosocial. Es el mismo criterio del protocolo de moderación que el curso va a redactar en la sesión 8, y conviene que ya esté puesto antes de que llegue la primera consulta delicada.
