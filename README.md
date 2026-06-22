# Asistente Daruma — Guía de despliegue

Chat web interno que guía a los usuarios en los 6 módulos del sistema QMS Daruma.

## Cómo funciona (arquitectura segura)

```
[Usuario en navegador]  →  [index.html]  →  [/api/chat.js en el servidor]  →  [OpenAI API]
```

Tu API Key y todo el conocimiento de Daruma viven **en el servidor** (`api/chat.js`), nunca en el navegador del usuario. Esto significa:
- Nadie puede ver tu API Key abriendo el código de la página.
- Nadie puede copiar tu base de conocimiento de Daruma.

---

## Paso 1: Crea (o revoca y recrea) tu API Key de OpenAI

1. Entra a https://platform.openai.com/api-keys
2. Si ya compartiste una key antes, haz clic en **Revoke** para anularla.
3. Clic en **Create new secret key**, ponle un nombre (ej. "daruma") y cópiala. La verás solo una vez.
4. Guárdala en un lugar seguro temporalmente. **No la pegues en ningún chat ni archivo de código.**

---

## Paso 2: Sube el proyecto a GitHub

1. Crea una cuenta en https://github.com (si no tienes).
2. Crea un repositorio nuevo, privado, llamado `asistente-daruma`.
3. Sube esta carpeta completa (puedes arrastrar los archivos en la web de GitHub: botón "Add file" → "Upload files").

---

## Paso 3: Conecta con Vercel

1. Entra a https://vercel.com y regístrate con tu cuenta de GitHub.
2. Clic en **Add New → Project**.
3. Selecciona el repositorio `asistente-daruma` e importa.
4. **ANTES de hacer Deploy**, ve a la sección **Environment Variables** y agrega:
   - Name: `OPENAI_API_KEY`
   - Value: *(pega aquí tu API Key de OpenAI)*
5. Clic en **Deploy**. En ~1 minuto tendrás un link tipo `https://asistente-daruma.vercel.app`

---

## Paso 4: Comparte y prueba

- Comparte el link con 2-3 usuarios de prueba primero.
- Pídeles que pregunten cosas reales que les surgen al usar Daruma.
- Anota qué preguntas no respondió bien para mejorar el conocimiento después.

---

## Costos

- Vercel: gratis (plan Hobby) para este uso.
- OpenAI: pagas por consumo. El modelo usado es `gpt-4o-mini` (muy económico). Con 30-50 usuarios haciendo consultas ocasionales, el costo estimado es de **2 a 10 USD al mes**.
- Tienes los créditos gratuitos iniciales de OpenAI para empezar sin pagar nada.

---

## Cómo mejorar el conocimiento más adelante

Todo el conocimiento de Daruma está en la constante `CONOCIMIENTO_DARUMA` al inicio del archivo `api/chat.js`. Para agregar o corregir información:
1. Edita ese texto.
2. Sube el cambio a GitHub.
3. Vercel actualiza la página automáticamente.

---

## Seguridad: límites de este prototipo

- El acceso es por link. Cualquiera con el link puede entrar. Para una prueba interna está bien.
- Para producción con 30-50 personas, conviene agregar autenticación (login con correo corporativo). Eso es parte de la Fase 2.
- No pongas datos sensibles reales en el conocimiento; solo procesos genéricos.
