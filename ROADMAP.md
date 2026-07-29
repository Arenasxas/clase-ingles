# Hoja de ruta — Mi Clase de Inglés

Seguimiento de mejoras. Basado en el análisis de las mejores apps (Duolingo, Babbel, Busuu, Memrise, ELSA, TalkPal/Speak).

## ✅ Hecho
- Test de nivel (A1–C1) + plan personalizado
- Clase con IA ("Miss Clara") + corrección ❌/✅
- Voz: hablar (micrófono) + escuchar (dictado)
- Repaso espaciado (SRS, tarjetas) — local, ilimitado
- Juegos: escuchar, completar, ordenar, traducir
- Racha, meta diaria, recordatorio
- Material propio + personalización de clase
- Guía de uso
- Medidor de uso diario de la API + manejo de límite
- Auto-detección del modelo de Gemini
- PWA instalable + deploy en GitHub Pages

## ✅ Hecho (nuevas)
- **P1 · Roleplays / escenarios** (café, médico, aeropuerto, teléfono, restaurante, compras, direcciones, presentarse) — la IA hace de personaje y corrige con TIP

- **P2 · Logros / insignias / XP** — 12 insignias, puntos, niveles, avisos (toast) al desbloquear
- **P3 · Camino de lecciones por nivel** — 10 lecciones por nivel (A1–C1), progreso, desbloqueo lineal, +20 XP por lección
- **P4 · Feedback de pronunciación** — repetir frase, marca palabras bien (verde) / a reforzar (rojo) + puntaje. Local, sin API
- **P5 · Historias / lecturas graduadas** — la IA crea un cuento corto a nivel, con audio, traducción y 2 preguntas de comprensión

## 🔨 En progreso
- (nada abierto — roadmap base completo)

## ✅ Hecho (extra)
- **🎧 Solo escuchar / audio-clases** — la IA arma una mini-clase hablada del tema, se reproduce manos libres con resaltado del texto (read-along), guarda apunte en español y suma vocabulario a las tarjetas

## ✅ Hecho (extra)
- **🩹 Repaso de errores frecuentes** — la profe marca cada error (ERROR: mal === bien === por qué), se guarda y ordena por frecuencia; modo "practicar mis errores"
- **🔎 Diccionario** — buscar palabra (inglés o español): traducción, significado, ejemplo, pronunciación y audio; guardar en tarjetas
- **Profe experto** — prompt reforzado: profesora nativa C2 con formación TEFL/CELTA, sin inventar

## ✅ Hecho (extra)
- **📞 Clase por llamada (voz en vivo)** — modo manos libres tipo llamada telefónica: escucha → IA → habla en bucle automático, con pantalla de llamada, subtítulos y botón colgar. Clase hablada natural. Usa Web Speech (gratis), no Gemini Live.

## ✅ Hecho (extra)
- **📷 Practicar con una foto** — saca/elige una foto (cartel, etiqueta, menú), Gemini (visión) lee el texto, traduce, explica y suma vocabulario a las tarjetas. Gratis (mismo modelo, sin costo extra).

## 🐛 Bugs encontrados y corregidos
- **Botones en fila apilados en vez de lado a lado** — faltaba la clase CSS `.row` (solo existía `.rowbtw`). Afectaba: Repaso/Juegos, Mis errores/Diccionario en el inicio, Sí/No del repaso, controles de audio-clase, reintentar en pronunciación. Corregido agregando `.row{display:flex;gap:10px}` + `.row>*{flex:1}`.
- **Avisos de logro (toast) superpuestos** — si se desbloqueaban 2+ insignias en el mismo momento (ej. primera clase + racha 7 días + 100 puntos a la vez), los carteles se dibujaban todos en el mismo lugar, ilegibles. Corregido con una cola: ahora se muestran de a uno.

## 🔍 Revisión integral realizada
- Las 16 pantallas abren sin error de consola, probadas juntas con un estado "rico" (todas las funciones con datos).
- Transiciones entre modos (clase ↔ situación ↔ lección ↔ llamada) no mezclan historiales ni dejan estado roto; cada entrada resetea el modo correctamente.
- Barra superior recupera el título correcto al volver de una situación/lección a la clase normal.
- Todas las clases CSS usadas en el código tienen su regla definida (chequeo automático, ninguna faltante tras el fix de `.row`).

## ✅ Hecho (extra)
- **Material curricular real para las 50 lecciones** (A1–C1) — cada lección ahora tiene: explicación gramatical concreta en español, vocabulario curado (5-6 términos con traducción), y el error típico de interferencia español→inglés a vigilar. Antes solo tenían título + 3 palabras sueltas y la IA improvisaba todo. Ahora la profe enseña desde material preparado, no inventa sobre la marcha.
- El generador de **audio-clases** también usa este material cuando el tema viene del camino (gramática + vocab + error se pasan al prompt).
- `lessonSystem()` reescrito para inyectar el material real (tema, gramática, vocabulario a incorporar, error a vigilar) en cada lección.

## ❌ Descartado
- **Migrar la llamada a Gemini Live API** — investigado (jul-2026): el audio en tiempo real NO tiene capa gratuita confiable, se cobra aparte del texto y hubo baja de modelos live (gemini-2.0-flash-live discontinuado 1-jun-2026). Rompe el requisito de "siempre gratis" de la app. Decisión del usuario: mantener el modo llamada actual (Web Speech, gratis) y no migrar. No reabrir salvo que el usuario pida explícitamente pagar por esto.

## 💡 Ideas futuras
- (ninguna pendiente por ahora)

## ⏳ Próximo (priorizado)

## Notas
- URL: https://arenasxas.github.io/clase-ingles/
- Todo local (localStorage), sin backend. IA: Gemini gratis.
