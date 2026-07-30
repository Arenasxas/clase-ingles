# Hoja de ruta — Mi Clase de Inglés

Seguimiento de mejoras. Basado en el análisis de las mejores apps (Duolingo, Babbel, Busuu, Memrise, ELSA, TalkPal/Speak).

## 🧠 Tutor adaptativo (en curso) — plan completo en `C:\Users\nicoi\.claude\plans\me-gustar-a-que-la-hazy-moth.md`

Objetivo: dejar de ser "una app más" y modelar de verdad al alumno (qué necesita, qué domina, cómo se siente al hablar) para decidir cada día qué conviene practicar. Basado en evidencia real (no "estilos de aprendizaje" VAK — desacreditado por meta-análisis 2024; sí needs analysis, práctica espaciada g≈0.80, corrective feedback d≈0.64).

- **Fase 0 — Andamiaje** ✅: backup automático de localStorage, `deepDefaults()` genérico, poda de cuota, `escapeHtml()` en todo el HTML dinámico, fixes (`--good`→`--ok` en pronunciación, `seenGuide` ahora se lee, bug de tipeo).
- **Fase 1 — Contexto real en las 11 llamadas a IA** ✅: `buildLearnerContext(scope)` con presupuesto de tokens por tipo (full/task/drill/lookup) + `aiCall()`. Antes 8 de 11 funciones (roleplay, llamada, juegos, audio-clases, historias, diccionario, foto) no recibían nada del perfil del usuario — ahora todas lo reciben, cada una con el nivel de detalle que le corresponde. Verificado con `?debug=1`: todos los scopes dentro de presupuesto (full 370/900, task 113/400, drill 55/250, lookup 39/150 en la prueba).
- **Fase 2 — Motor de dominio (BKT local, sin gastar IA)** ✅: catálogo de 24 puntos gramaticales (KC), modelo bayesiano simple (Bayesian Knowledge Tracing: prior 0.25, guess 0.25, slip 0.10, learn 0.15) que mide dominio real a partir de 10 puntos de instrumentación (test de nivel, errores detectados por la profe, lecciones completadas, juegos, pronunciación, repaso, diccionario, foto). Decae hacia el prior si no se practica en 30 días. Clasificador local por regex (`guessKC`, 22 reglas) que detecta a qué error típico corresponde cada corrección de la profe, sin gastar IA. Repaso espaciado con intervalos IGUALES (Kim & Webb 2022: mejor retención a largo plazo que expansivo) y agrupado por tema (Brunmair & Richter 2019: intercalar vocabulario lo perjudica, g=-0.39). Vista "🧠 Cómo te veo" con barras de destreza + temas a reforzar. Verificado con matemática exacta: 5 aciertos cruza a 99.5%, 3 errores baja a 17.3%, 30 días sin practicar decae de 90% a 48.9%.
- **Fase 3 — Onboarding needs-analysis**: reemplaza el test de estilos por preguntas que sí predicen mejor aprendizaje (qué necesita hacer con el inglés, tiempo real disponible, ansiedad al hablar) + preferencia de formato (solo como desempate, nunca filtra contenido) + diagnóstico adaptativo + prescripción explicada.
- **Fase 4 — Recomendador en el inicio**: "hoy te conviene esto porque…" en vez de menú fijo.
- **Fase 5 — Coach con IA**: 1 llamada por sesión (no por turno) que ajusta la prescripción, con patch validado campo por campo (nunca puede tocar el dominio medido).
- **Fase 6 — Contenido real**: recomendación de series/música/videos de un catálogo curado a mano por nivel + intereses (no inventado por la IA).
- **Fuera de alcance ahora**: Supabase (investigado, documentado en el plan) y multi-usuario — decisión del dueño: "solo mi nonna por ahora", sin proxy de API.

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

## 🧠 Proyecto grande: tutor adaptativo por alumno

Pivote mayor (jul-2026): la app deja de tratar a todos igual y pasa a modelar a su alumno (qué necesita, qué domina, cómo se siente al hablar) para decidir cada día qué conviene practicar. Plan completo en `me-gustar-a-que-la-hazy-moth.md` (plan mode). Basado en evidencia científica real, no en "estilos de aprendizaje" (VAK) — ver decisión abajo.

**Decisión importante — test de estilos de aprendizaje DESCARTADO como filtro de contenido**: el usuario pidió un test de estilos visual/auditivo/kinestésico. Investigación (jul-2026): meta-análisis Clinton-Lisell & Litzinger 2024 (Frontiers in Psychology, 21 estudios, N=1712) encontró la interacción cruzada que la "meshing hypothesis" exige en solo 26% de las medidas; los autores concluyen que los beneficios son "too small and too infrequent to warrant widespread adoption" y piden "extreme caution", recomendando **instrucción multimodal para todos** en su lugar (g=0,28–0,70). Decisión (aprobada por el usuario): el test inicial pasa a ser **needs analysis** (qué tareas reales necesita hacer con el inglés — esto sí tiene respaldo sólido, revisión de 149 estudios ESP) + una pregunta de formato preferido que se usa **solo como desempate** del recomendador, nunca para quitar actividades. **No reabrir el test VAK como filtro de contenido** salvo pedido explícito nuevo del usuario con nueva evidencia en contra.

Otras restricciones de evidencia que rigen el diseño: práctica espaciada g≈0,80 (Kim & Webb 2022) → intervalos iguales por defecto; corrective feedback explícito d≈0,64, prompts>recasts (Li 2010; Lyster & Saito); interleaving daña vocabulario g=−0,39 (Brunmair & Richter 2019) → nunca intercalar palabras, solo gramática y con dominio medio; ansiedad al hablar r≈−0,36 → puntajes ocultables y reintentos libres.

**Alcance actual**: solo la nonna (sin multi-usuario ni proxy de API — cada quien pega su propia clave gratis). Supabase queda documentado para una fase posterior, no se implementa todavía.

### Fases
- ✅ **Fase 0 — Andamiaje y fixes**: backup de localStorage antes de migrar + botón "Restaurar copia anterior" en Ajustes; `deepDefaults()` recursivo reemplaza el merge a mano (preserva correctamente diccionarios dinámicos como badges/goalsDone/lessonsDone, verificado); poda de `history` a 40 turnos + manejo de `QuotaExceededError` con poda progresiva; `escapeHtml()` aplicado a ~14 sitios que inyectan texto de IA/usuario por `innerHTML` (verificado con payloads XSS reales: quedan como texto, no se ejecutan); fix de `scoreLevel()` para que use el campo `lvl` de las preguntas (antes se ignoraba — ahora acertar una pregunta difícil pesa aunque falles varias fáciles); fix de `seenGuide` (se escribía y nunca se leía). Todo verificado: migración probada con un estado viejo completo (nada se perdió), inyección HTML maliciosa neutralizada, 14 pantallas sin errores de consola.
- ⏳ **Fase 1** — Personalización real en las 11 llamadas a IA (`buildLearnerContext`, hoy 8 de 11 no reciben nada del perfil)
- ⏳ **Fase 2** — Motor de dominio: catálogo de knowledge components + BKT local (determinista, sin gastar IA)
- ⏳ **Fase 3** — Onboarding nuevo: needs analysis + diagnóstico adaptativo + prescripción de método explicada
- ⏳ **Fase 4** — Recomendador en el home ("hoy te conviene esto porque…")
- ⏳ **Fase 5** — Coach con IA (1 llamada por sesión) que ajusta la prescripción, con patch validado
- ⏳ **Fase 6** — Recomendaciones de contenido real (series/música) desde catálogo curado
- 🔜 Supabase (fuera de alcance por ahora, investigado: free tier 500MB/50k MAU, RLS + anon auth, se pausa a los 7 días de inactividad)

## ⏳ Próximo (priorizado)
- Fase 1 del tutor adaptativo (ver arriba)

## Notas
- URL: https://arenasxas.github.io/clase-ingles/
- Todo local (localStorage), sin backend. IA: Gemini gratis.
