# Mi Clase de Inglés 👵🇬🇧

App web simple para que mi nonna aprenda inglés con una profe de IA (Gemini). Una sola página, sin servidor, gratis.

## Qué hace
- **Test de nivel** al inicio → detecta A1–C1 (marco CEFR).
- **Plan personalizado** según nivel y objetivo.
- **Clase con "Miss Clara"**: chat con IA que enseña de a poco, corrige con ❌/✅, dicta en voz alta y propone ejercicios.
- **Hablar en inglés** con el micrófono (reconocimiento de voz del navegador) → la profe corrige la pronunciación/gramática.
- **Apuntes automáticos**: lo importante que enseña la profe queda guardado.
- Todo se guarda en el **celular** (localStorage). No hay backend ni base de datos.

## Requisitos
- **Chrome en Android** (el reconocimiento de voz anda perfecto ahí).
- Una **clave gratis de Gemini**: https://aistudio.google.com/apikey
  - Se pega **una sola vez** dentro de la app y queda guardada en el dispositivo. No va en el código.

## Cómo publicarla gratis

### Opción A — GitHub Pages (URL permanente)
1. Crear cuenta en github.com (gratis).
2. Crear un repositorio público, ej: `clase-ingles`.
3. Subir `index.html` (y este README).
4. Settings → Pages → Source: `main` / `/root` → Save.
5. En ~1 min queda en `https://TU-USUARIO.github.io/clase-ingles/`.

### Opción B — Netlify Drop (más rápido, sin comandos)
1. Entrar a https://app.netlify.com/drop
2. Arrastrar la carpeta `Nona` completa.
3. Da una URL al instante. (Crear cuenta gratis para que no expire.)

Después: abrir la URL en el celular de la nonna, pegar la clave de Gemini una vez, y listo.

## Costo
- Gemini tiene capa gratuita amplia; para uso de una persona no se paga.
- GitHub Pages / Netlify: gratis.
