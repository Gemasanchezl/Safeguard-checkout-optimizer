# 🎼 Arquitectura del Proyecto: La Orquesta Filarmónica de IA

> **Analogía central:** Este proyecto no funciona como un único prompt gigante.
> Funciona como una **orquesta**: cada pieza tiene un rol preciso, y el resultado
> es armonioso porque cada músico sabe exactamente qué tiene que tocar y cuándo.

---

## 🗺️ Mapa General de la Arquitectura

```
Usuario / Alumno
      │
      ▼
┌─────────────────────┐
│   🎩 AGENTS.md      │  ← El Director de Orquesta
│   (Orquestador)     │
└────────┬────────────┘
         │ lee y convoca
    ┌────┴──────────────────────────┐
    │                               │
    ▼                               ▼
┌──────────────┐          ┌─────────────────────────┐
│ 📜 SKILL.md  │          │  🎻 rules/*.mdc          │
│ (Partitura)  │          │  (Los Músicos)           │
└──────────────┘          └─────────────────────────┘
         │                               │
         └──────────────┬────────────────┘
                        │ aplica mejoras sobre
                        ▼
              ┌──────────────────────┐
              │  🏛️ Insights.mdc     │
              │  (Acústica del Teatro)│
              └──────────────────────┘
                        │
                        ▼
              ┌──────────────────────┐
              │  ✅ index-v2.html    │
              │  (La Sinfonía Final) │
              └──────────────────────┘
```

---

## 🎭 Los 4 Roles de la Orquesta

### 🎩 1. El Director de Orquesta — `AGENTS.md`

> *"Él no toca ningún instrumento. Escucha, interpreta y decide."*

El agente orquestador es el cerebro del sistema. Su función **no** es escribir código
directamente — es leer el contexto, entender el problema y decidir qué recursos
convocar en cada momento.

| Propiedad | Detalle |
| :--- | :--- |
| **Archivo** | `AGENTS.md` |
| **Rol** | Toma de decisiones estratégicas |
| **Lo que hace** | Lee los Insights, carga la Skill y valida contra las Rules |
| **Lo que NO hace** | Improvisar. Nunca inventa soluciones sin consultar el protocolo |
| **Lógica clave** | Elige entre **Plan A** (UX ideal) y **Plan B** (contingencia técnica) según el contexto |

**Fragmento de su lógica de orquestación:**
```
PLAN A (Default): Se ejecuta siempre que no haya restricción técnica.
PLAN B (Contingencia): Solo se activa si el usuario menciona "bloqueo de backend".
```

---

### 📜 2. La Partitura — `skills/optimizar_checkout.mdc`

> *"La partitura no improvisa. Es el algoritmo humano que le damos a la IA
> para que siga un método probado."*

La Skill es el protocolo paso a paso. Define **cómo** resolver el problema,
no qué herramientas usar. Es la diferencia entre un orquestador que actúa con
criterio y uno que improvisa.

| Propiedad | Detalle |
| :--- | :--- |
| **Archivo** | `skills/optimizar_checkout.mdc` |
| **Rol** | Protocolo de ejecución |
| **Lo que contiene** | Fases de análisis, árbol de decisión (Plan A/B) e implementaciones obligatorias |
| **Por qué es clave** | Sin partitura, el Director podría "improvisar" soluciones inconsistentes |

**Las 4 fases de la Skill:**

```
Fase 1 → Análisis: Detectar los errores de UX en el HTML
Fase 2 → Decisión: ¿Plan A o Plan B?
Fase 3 → Implementación: Validación inline, microcopy, CTA descriptivo
Fase 4 → Documentación: Registrar cada mejora vinculada a un Insight
```

---

### 🎻 3. Los Músicos — `rules/*.mdc`

> *"Conocen su técnica a la perfección. Garantizan que la 'música' siempre
> respete la marca, sin importar qué partitura esté sonando."*

Las Rules son las restricciones y estándares que se aplican de forma **automática**
en cada fichero del proyecto. Son el Design System vivo.

| Archivo | Instrumento | Función |
| :--- | :--- | :--- |
| `design-system.mdc` | 🎻 Primer Violín | Tokens de color, sombras, radios, tipografías |
| `REGLAS_UX.mdc` | 🎺 Viento Metal | Principios de usabilidad y accesibilidad |
| `proyecto.mdc` | 🥁 Percusión | Contexto del proyecto y restricciones globales |
| `flujo-checkout.mdc` | 🎹 Piano | Reglas específicas del flujo de compra |

**Ejemplo de token del Design System en acción:**

```css
/* ❌ Sin reglas: el músico improvisa */
border: 2px solid red;

/* ✅ Con reglas: el músico toca su parte */
border: 2px solid var(--status-error); /* = #FF3B30 */
```

---

### 🏛️ 4. La Acústica del Teatro — `Insights.mdc`

> *"La acústica nos dice dónde rebota mal el sonido. Sin ella, el Director
> ajustaría la ejecución a ciegas."*

Los Insights son los **datos reales de usuarios**. No son opiniones del equipo —
son evidencias de comportamiento que el Director usa para justificar cada decisión.

| Propiedad | Detalle |
| :--- | :--- |
| **Archivo** | `Insights.mdc` |
| **Rol** | Fuente de verdad sobre la fricción de usuario |
| **Lo que contiene** | Métricas de negocio (40% drop-off) + hallazgos cualitativos |
| **Por qué es clave** | Convierte una opinión en una decisión fundamentada |

**Los 3 problemas que detectó la "acústica":**

| # | Insight | Causa Raíz | Solución en la Skill |
| :-- | :--- | :--- | :--- |
| 1 | 🧱 **El Muro del Teléfono** | El sistema pide `+34` sin indicarlo | Plan A: campo de 9 dígitos sin prefijo |
| 2 | 🔒 **Ansiedad por Privacidad** | No se explica para qué se usa el dato | Microcopy de confianza |
| 3 | 💀 **Validación Post-Mortem** | Los errores aparecen al final, no en tiempo real | Validación `onBlur` inline |

---

## 🔄 El Flujo Completo: De la Partitura a la Sinfonía

```
1. 📥 INPUT
   Usuario escribe: "@Agent optimiza el @index.html usando @Insights.mdc"
          │
          ▼
2. 🎩 DIRECTOR lee el contexto
   → Carga Insights.mdc  →  Detecta: 40% drop-off, 3 fricciones críticas
   → Decide: "Aplicaré el PLAN A"
          │
          ▼
3. 📜 DIRECTOR consulta la PARTITURA
   → Carga skills/optimizar_checkout.mdc
   → Sigue las 4 fases del protocolo
          │
          ▼
4. 🎻 LOS MÚSICOS entran en escena
   → Aplican tokens de design-system.mdc en cada cambio de CSS
   → Validan accesibilidad según REGLAS_UX.mdc
          │
          ▼
5. 🏛️ La ACÚSTICA valida el resultado
   → ¿Se resolvió el Muro del Teléfono? ✅
   → ¿Se añadió microcopy de confianza? ✅
   → ¿Validación inline activa? ✅
          │
          ▼
6. 🎼 OUTPUT: index-v2.html
   + Documento de "Mejoras Implementadas"
```

---

## 💡 La Lección de Arquitectura

> La diferencia entre un **prompt** y un **sistema de IA orquestado** es
> exactamente la misma que entre un músico tocando de oído y una orquesta
> siguiendo una partitura.

| | Prompt Simple | Sistema Orquestado |
| :--- | :--- | :--- |
| **Consistencia** | Varía en cada ejecución | Reproducible siempre |
| **Escalabilidad** | No escala | Se añaden nuevas Rules/Skills sin tocar el Agente |
| **Trazabilidad** | No sabes por qué tomó esa decisión | Cada acción se documenta |
| **Mantenimiento** | Hay que reescribir el prompt | Se actualiza solo la pieza que cambia |

---

*Documento creado para el curso de Orquestación de IA · Safeguard Digital Demo*
