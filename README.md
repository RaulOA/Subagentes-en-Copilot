# Subagentes en Copilot

## 📖 Qué es
Un conjunto de instrucciones para configurar a GitHub Copilot como **agente orquestador**, delegando todas las tareas de lectura y edición de código en subagentes especializados. El objetivo es optimizar el uso de la ventana de contexto, mejorar la trazabilidad y separar responsabilidades.

---

## 🎯 Para qué sirve
- Controlar el flujo de trabajo en proyectos grandes.
- Evitar saturación de la ventana de contexto.
- Generar documentación previa a la implementación.
- Mejorar la auditabilidad y trazabilidad de cambios.
- Separar claramente investigación, especificación e implementación.

---

## ⚙️ Cómo utilizarlo
1. Crear o editar el archivo `copilot-instructions.md` en el repositorio.
2. Copiar las instrucciones de subagentes dentro de ese archivo.
3. Configurar Copilot para que lea las instrucciones desde `copilot-instructions.md`.
4. Seguir el flujo obligatorio:
   - **Subagente #1 (Investigación)**: analiza archivos y crea especificación en `docs/SubAgent_docs/`.
   - **Orquestador**: recibe resultados y pasa la ruta del archivo.
   - **Subagente #2 (Implementación)**: aplica cambios según la especificación.
5. Usar siempre el subagente por defecto, sin `agentName`.
6. Al invocar `runSubagent`, incluir siempre:
   - `description`: resumen de 3-5 palabras.
   - `prompt`: instrucciones detalladas.

---

## 📑 Plantillas de prompts

### Investigación

```
Research [tema]. Analiza los archivos relevantes en el código.
Crea un documento de especificación en: docs/SubAgent_docs/[NOMBRE].md
Devuelve: resumen de hallazgos y la ruta del archivo.
```

### Implementación

```
Lee la especificación en: docs/SubAgent_docs/[NOMBRE].md
Implementa según la especificación.
Devuelve: resumen de cambios realizados.
```

---

## ✅ Casos de uso óptimos
- **Proyectos grandes y complejos**: repositorios con múltiples módulos y dependencias.
- **Entornos auditables**: documentación generada facilita revisiones y auditorías.
- **Trabajo en equipo**: separación clara de roles y tareas.
- **Refactorización y migraciones**: análisis previo reduce riesgos.
- **Educación y formación**: fomenta buenas prácticas al obligar a documentar antes de implementar.

---

## ⚠️ Contraindicaciones
- **Proyectos pequeños o simples**: añade fricción innecesaria.
- **Sobrecarga documental**: proliferación de archivos en `docs/SubAgent_docs/`.
- **Pérdida de contexto**: riesgo de omitir detalles críticos al resumir entre agentes.
- **Complejidad operativa**: flujo más lento, requiere disciplina.
- **Errores de orquestación**: posibilidad de bucles infinitos o prompts mal definidos.
- **Dependencia de versiones**: mejor soporte en VS Code Insiders; puede no ser estable en todas las configuraciones.

---

## 📊 Balance
- **Muy recomendable** en proyectos grandes, con necesidad de trazabilidad y documentación.
- **Menos recomendable** en proyectos pequeños, prototipos rápidos o tareas urgentes donde la velocidad prima sobre la auditabilidad.
```
