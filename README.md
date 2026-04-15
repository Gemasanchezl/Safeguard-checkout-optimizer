# 🛡️ Checkout Optimizer: Safeguard Digital

Ejercicio didáctico que demuestra la orquestación avanzada entre **Agents**, **Skills** y **Design Systems** dentro de Cursor para optimizar la conversión (CRO) en una aseguradora.

## 🚀 ¿Qué hace este proyecto?

Este Agente analiza un formulario de checkout con problemas críticos de usabilidad (basado en datos reales de usuario) y lo transforma automáticamente en un flujo de alta conversión siguiendo un protocolo de diseño estricto.

### Output del Agente:
- **Prototipo evolucionado:** Generación de `index-v2.html` con mejoras de UX aplicadas.
- **Validación Semántica:** Implementación de tokens de diseño (colores, radios, sombras) automáticos.
- **Documentación de Decisiones:** Un registro detallado de por qué se eligió el **Plan A** o el **Plan B** según el contexto técnico.

---

## 🛠️ Estructura del "Cerebro"

El proyecto se divide en capas de responsabilidad para demostrar una arquitectura de IA escalable:

| Capa | Archivo | Descripción |
| :--- | :--- | :--- |
| **Agent** | `AGENTS.md` | El orquestador que analiza los datos y toma decisiones estratégicas. |
| **Rules** | `rules/*.mdc` | Las "leyes" del proyecto: Design System, contexto de marca y flujos de trabajo. |
| **Skill** | `skills/optimizar_checkout.mdc` | El protocolo paso a paso con la lógica de negocio (Plan A/B). |
| **Insights** | `INSIGHTS_USER_TEST.mdc` | La fuente de verdad sobre los problemas que detectaron los usuarios reales. |

---

## 📖 Cómo usar en la Demo

1. **Escenario Base:** Abre el `index.html` original (el formulario que falla).
2. **El Problema:** Muestra el archivo `INSIGHTS_USER_TEST.mdc` para explicar por qué perdemos clientes.
3. **La Ejecución:** En el chat de Cursor, llama al agente:
   > `@Agent optimiza el @index.html usando los @INSIGHTS_USER_TEST.mdc`
4. **El Resultado:** Observa cómo el Agente consulta la **Skill**, aplica el **Design System** y genera la nueva versión documentada.

---

## 🎓 Notas para alumnos

Este proyecto pasó de ser un "prompter" a ser un **Orquestador de IA**:
- No le decimos a la IA *qué* escribir.
- Le damos las **reglas**, el **contexto** y las **skills** para que ella decida la mejor solución.
