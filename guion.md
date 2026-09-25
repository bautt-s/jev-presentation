# Guion: Charla "Jev" · Equipo Dev Sheriff

> **Cómo usar este guion:** cada slide ya se sostiene solo (el público puede leerlo sin ti).
> Lo de abajo es lo que **tú sumas** hablando: contexto, énfasis, anécdotas y transiciones.
> No leas la pantalla en voz alta: amplíala.
>
> **Navegación:** `→ / espacio / Enter` avanza · `←` retrocede · **`F`** pantalla completa · **`R`** repite la animación del slide actual · clic o toque (derecha avanza, izquierda retrocede).
>
> **Ojo:** en los slides de casos (18 a 22) el primer `→` muestra la traducción. El slide 13 (Alucinaciones) tiene **2 revelaciones**: las dos primeras veces que presionas `→` aparecen el matiz y la conclusión; recién la tercera pasa al slide siguiente.
> **Duración estimada:** 15–20 min + preguntas. Los `⏱` son un ritmo sugerido.

---

## 01 · Portada: "Jev" ⏱ 0:30
**En pantalla:** título Jev + "el modelo que no escribe ni una palabra".

**Qué decir:**
- Arranca con el gancho: *"Esto salió hace unos días y me voló la cabeza. Es un modelo de IA que, a propósito, no escribe texto. Ni una palabra. Y cuando entiendan por qué, van a querer usarlo."*
- Pon la expectativa: *"En 15 minutos les cuento qué es, cómo funciona, cuánto cuesta, y, lo más importante, cuándo conviene usarlo en Sheriff y cuándo no."*

---

## 02 · El problema ⏱ 1:30
**En pantalla:** LLMs = lentos + alucinan; barras de latencia/costo/alucinación.

**Qué decir:**
- Aterriza el dolor con algo nuestro: *"Cuántas veces hemos querido solo clasificar algo, ¿este ticket es de billing o soporte?, ¿este documento es una factura?, y terminamos llamando a un LLM gigante, esperando segundos y pagando por un párrafo que después tenemos que parsear."*
- Frase clave: *"Para chatear son insuperables. Para **decidir**, son un cañón para matar una mosca."*
- Transición: *"De esa incomodidad exacta nace Jev."*

---

## 03 · Quién y por qué ⏱ 2:30
**En pantalla:** TypeSafe AI, Diogo Almeida (ex-OpenAI), timeline, $40M.

**Qué decir:**
- Da credibilidad: *"Esto no es un experimento de fin de semana. El CEO, Diogo Almeida, estuvo ~4 años en OpenAI trabajando en las tripas de InstructGPT, ChatGPT y GPT-4."*
- El insight fundacional: *"Su observación fue: la IA ya chatea mejor que un humano, pero la **automatización de verdad** sigue rota. Estuvieron ~2 años en stealth resolviendo eso."*
- Señala que hay respaldo fuerte ($40M seed, DCVC, ~$200M valuación) → *"el mercado se lo está tomando en serio."*

---

## 04 · Qué es ⏱ 4:00
**En pantalla:** LLM devuelve un string vs. Jev devuelve valor tipado + prob + confianza.

**Animación:** el texto del LLM se escribe palabra por palabra mientras los valores de Jev ya aparecieron. Deja que termine: el contraste lo explica solo.

**Qué decir:**
- Contrasta los dos "terminales" en vivo: *"Miren la diferencia. A la izquierda, el LLM te da una frase amable que igual tienes que interpretar. A la derecha, Jev te da la variable ya lista: equipo = billing, con 94% de probabilidad y 88% de confianza."*
- Idea ancla: *"Jev no produce algo para que **lo leas tú**; produce algo para que **lo consuma tu código**."*

---

## 05 · System 1 / System 2 (Kahneman) ⏱ 5:15
**En pantalla:** dos círculos, Jev en System 1.

**Qué decir:**
- Explica la metáfora si alguien no leyó a Kahneman: *"System 1 es cuando ves 2+2 y sabes que es 4 sin pensarlo. System 2 es cuando resuelves 17×24: te toma esfuerzo."*
- Remátalo: *"Los LLMs viven en el System 2: deliberan, razonan, gastan. Jev es puro System 1: el reflejo. Por eso es su categoría propia, 'System One Model'."*

---

## 06 · Cómo funciona (arquitectura) ⏱ 7:00
**En pantalla:** diagrama State + preguntas → Parallel Sampler → outputs tipados. Menciona RLCD.

**Qué decir:**
- Recorre el diagrama de izquierda a derecha: *"Le pasas un **state**, el contexto, y una lista de **preguntas tipadas**. Las resuelve todas de una y te devuelve valores listos."*
- Destaca RLCD sin tecnicismo: *"Y ojo con cómo lo entrenaron: no con feedback humano de '¿te gustó esta respuesta?', sino optimizando para que sus probabilidades sean **honestas**. Solo con datos sintéticos. Eso importa para el siguiente punto."*

---

## 07 · Autoregresivo vs paralelo ⏱ 8:15
**En pantalla:** cadena de tokens vs 3 barras en paralelo. 70–500 ms vs 3–329 s.

**Animación:** es una carrera. Jev termina casi al instante ("listo · 0.2 s") y el LLM sigue encendiendo tokens uno a uno. Si quieres repetirla mientras hablas, presiona `R`.

**Qué decir:**
- Explica el porqué de la velocidad: *"Un LLM escribe una palabra, se relee entero, escribe la siguiente… cientos de veces. Es intrínsecamente secuencial. Jev no genera texto, así que puede resolver todo en paralelo, de una pasada."*
- Aterriza el número: *"Estamos hablando de milisegundos vs. segundos. No es 'un poco más rápido'. Es otra categoría."*

---

## 08 · Las 3 primitivas ⏱ 10:00
**En pantalla:** Choice / Score / Noul con mini-gráficos.

**Qué decir:**
- Una frase por primitiva:
 - *"**Choice**: elige una opción de una lista. Clasificar, rutear."*
 - *"**Score**: puntúa en una escala. Severidad, calidad, riesgo."*
 - *"**Noul**: sí o no, pero te da la probabilidad. ¿Es phishing? 0.79."*
- El punto arquitectónico (clave para devs): *"Fíjense que la lógica de negocio queda en **nuestro** código, no enterrada en un prompt gigante. Es testeable, versionable, revisable en un PR."*

---

## 09 · Confianza calibrada / RLCD ⏱ 11:30
**En pantalla:** curva de calibración, Jev sobre la diagonal, LLM sobre-confiado.

**Qué decir:**
- Explica el gráfico: *"El eje X es la confianza que declara; el Y, cuánto acierta de verdad. Lo ideal es la diagonal: si dice 0.9, acierta 9 de 10."*
- El contraste: *"Los LLMs son fanfarrones: te dicen 0.95 y aciertan 0.7. Jev está pegado a la diagonal. Eso te deja **usar la confianza como umbral de decisión**: algo que con un LLM no puedes hacer con seguridad."*

---

## 10 · Jev vs LLM (tabla) ⏱ 12:30
**En pantalla:** tabla comparativa de 6 dimensiones.

**Qué decir:**
- No leas la tabla entera; señala 2–3 filas: *"Miren output, latencia y costo. Ahí está toda la historia."*
- Honestidad intelectual (suma credibilidad): *"Y fíjense en 'contexto': 64K tokens. Es un límite real. Esto **no** reemplaza a un LLM; juega en otra liga."*

---

## 11 · La brecha, a escala ⏱ 13:15
**En pantalla:** barra sliver (Jev) vs barra larga (LLM), 193.6× / 444.6×.

**Qué decir:**
- Da el "para qué": *"¿Por qué me importa 100 ms? Porque a esa velocidad puedes meter IA **dentro de un loop en tiempo real**: un feed, una UI, mientras el usuario tipea, sin que note la espera. Eso antes no era posible con IA."*
- Aviso de rigor: *"Los benchmarks son de ellos, corridos en sus condiciones. Tómenlos como orden de magnitud, no como evangelio."*

---

## 12 · Costos ⏱ 14:00
**En pantalla:** $0.042/MTok, output gratis, ejemplo $4.20, demo 390×.

**Animación:** el número grande baja desde $10 (el techo de un LLM frontier) hasta $0.042. Buen momento para quedarse callado un segundo.

**Qué decir:**
- Haz el cálculo tangible: *"Cien mil clasificaciones por cuatro dólares con veinte. Piénsenlo para un job batch nuestro."*
- La demo del builder ancla la comparación directa con un LLM top: *"384 titulares por 19 centavos, ~390× más barato que Opus haciendo lo mismo."*

---

## 13 · Alucinaciones ⏱ 15:30 **(momento fuerte)**
**En pantalla:** "matemáticamente imposible" + el matiz type-safe ≠ correcto.

**Ritmo:** al entrar solo se ve el claim. Primer `→`: aparece el asterisco y el panel del matiz. Segundo `→`: la conclusión sobre la confianza calibrada. Usa esas pausas para construir el remate.

**Qué decir:**
- Presenta el claim y luego el bisturí: *"Dicen que alucinar es matemáticamente imposible. Y a nivel de **formato** es verdad: no puede devolver algo fuera de tu schema."*
- El matiz que te hace ver crítico (no fan): *"PERO, y esto es lo que quiero que se lleven, type-safe garantiza que la respuesta tenga **forma válida**, no que sea **correcta**. Un 'billing' equivocado de tu lista permitida sigue siendo un error. Solo que ahora es un error bien tipado."*
- Cierra con la salida práctica: *"Por eso la confianza calibrada es la red: pones un umbral y lo que caiga por debajo lo escalas a un humano o a un LLM."*

---

## 14 · Dónde destaca ✓ ⏱ 16:30
**En pantalla:** clasificar/rutear, batch, tiempo real, guardrails, scoring.

**Qué decir:**
- Enmarca el patrón común: *"Todos estos casos comparten una cosa: son **reglas de decisión difusas**, donde escribir if/else a mano sería frágil, pero no necesitas que la IA te explique nada."*
- Menciona el uso de **guardrail** como el más subestimado: *"Este me parece el más interesante para nosotros: usar Jev de portero barato para filtrar o verificar lo que produce un LLM."*

---

## 15 · Dónde NO ✕ ⏱ 17:15
**En pantalla:** escribir, razonar, contexto largo, conversar, bajo volumen, security.

**Qué decir:**
- Sé tajante (esto genera confianza): *"Igual de importante es saber cuándo NO. Si necesitas que escriba, razone, compare fechas o mantenga una conversación: Jev no es la herramienta. Punto."*
- La anécdota del bot de trading: *"Alguien lo puso a operar cripto y no rindió. Moraleja: **rápido no es lo mismo que acertado**. Jev decide veloz, pero la calidad de la decisión depende del problema."*

---

## 16 · La regla mental ⏱ 18:00
**En pantalla:** árbol "¿quién consume la salida?" → humano=LLM / software=Jev.

**Qué decir:**
- Regálales el criterio para llevarse: *"Si se llevan una sola cosa, que sea esta pregunta: **¿la salida la lee un humano, o la consume otro pedazo de software?** Humano → LLM. Software → Jev."*
- Desactiva el falso dilema: *"No es Jev **vs** LLM. Es Jev **y** LLM. Jev es el nervio reflejo; el LLM, la corteza que delibera. Se complementan."*

---

## 17 · Casos reales (apertura) ⏱ 19:00
**En pantalla:** 5 tarjetas con los casos, cada una con su número clave.

**Qué decir:**
- *"Todo lo que les conté es teoría. Esto es lo que la gente construyó con Jev en su primera semana de vida."*
- No expliques cada tarjeta aquí: es el mapa. Di que vas a pasar por los cinco.

---

## 18 · Caso 1/5 · @nedwize, clasificador tributario ⏱ 19:45
**En pantalla:** tweet original + video. **Primer `→`**: el interruptor pasa de *en* a *es* y aparece la traducción.

**Qué decir:**
- Este es el que más nos toca: **clasificar documentos tributarios**, justo el tipo de trabajo que hacemos con la Carpeta Tributaria.
- El dato: 100% del corpus clasificado a $0.001 por página, 34 veces más barato y 6 veces más rápido que su pipeline con LLM. Y es open source: se puede probar.

---

## 19 · Caso 2/5 · @johnyeo_, router para agentes ⏱ 20:30
**Qué decir:**
- El patrón más reutilizable: **Jev delante de un agente como router**. Antes de que el agente lento piense, Jev elige skill, herramienta y parámetros.
- Resultado: agente 2 veces más rápido. Jev no reemplaza al LLM, le ahorra la parte de decidir (vuelve a la regla del slide 16).

---

## 20 · Caso 3/5 · @steventey, detección de abuso ⏱ 21:15
**Qué decir:**
- Dub (acortador de links) le pasó a Jev más de 10K dominios maliciosos conocidos y lo puso a marcar URLs sospechosas.
- Frase clave del tweet: *"algo con lo que peleábamos desde el primer día, lo resolvimos en 2 horas"*. Clasificación binaria clásica: un **Noul**.
- Ojo con el matiz del slide "Cuándo no": para seguridad, Jev es una **primera señal**, no la decisión final.

---

## 21 · Caso 4/5 · @TheMattBerman, focus group sintético ⏱ 22:00
**Qué decir:**
- Lo más creativo: Jev "mira" 723 anuncios como si fuera 30 tipos de comprador distintos y decide si parar o seguir scrolleando.
- 21.690 decisiones por 22 centavos. Muestra la escala: juicios masivos en paralelo que con un LLM serían carísimos.

---

## 22 · Caso 5/5 · @fazlerocks, ad blocker en vivo ⏱ 22:45
**Qué decir:**
- Tiempo real en el navegador: mira cada elemento de la página y decide "anuncio o no", sin listas de filtros.
- 16 anuncios fuera de un artículo por $0.0008, y queda en caché. Es el ejemplo perfecto de los 100 ms: IA dentro de la UI sin que se note.
- Cierre de la sección: *"Clasificar, rutear, detectar, simular, filtrar. Cinco verbos, un mismo modelo."*

> **Tip videos:** arrancan solos y en silencio al entrar al slide. Clic sobre el video lo pausa o reanuda. **`M`** activa o quita el audio.

---

## 23 · Resumen (TL;DR) ⏱ 20:00
**En pantalla:** la frase resumen + chips.

**Qué decir:**
- Repite la tesis una vez más, lento: *"Jev cambia conversación por decisión: tipada, calibrada, cien veces más rápida y barata. Brillante para clasificar y rutear; inútil para escribir. Es un modelo **nuevo**, no un LLM mejor."*

---

## 24 · Gracias ⏱
**Qué decir:**
- *"Gracias. Abro preguntas, y si quieren pasamos a ver los casos de Sheriff en detalle."*

---

### Notas de rigor (por si preguntan)
- **Fuentes:** TypeSafe AI (blog oficial), Wikipedia "Jev (AI model)", Requesty, MindStudio, LangChain, Towards Data Science. Consultadas 24·09·2026.
- **Sesgo de benchmarks:** los números de velocidad/costo son de TypeSafe, corridos en sus condiciones (laptops en la costa oeste, comparando contra competidores). Preséntalos como órdenes de magnitud.
- **Dato honesto a mano:** 64K de contexto y la distinción "type-safe ≠ correcto" son los dos límites que te blindan de sonar como vendedor.
- **Si preguntan por disponibilidad:** early access limitado desde el 15·09·2026.
