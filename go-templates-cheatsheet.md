# ⚙️ Go-Template para Chart Templates en Helm ⚙️

Los Go Templates son el corazón de la personalización y dinamismo en los Charts de Helm. Permiten generar manifiestos de Kubernetes de forma flexible, adaptándolos a diferentes entornos y configuraciones sin necesidad de duplicar código.

---

## 🌟 ¿Por qué usar Go Templates en Helm?

* **Reutilización Avanzada:** Un mismo chart puede desplegarse en múltiples entornos (desarrollo, staging, producción) simplemente cambiando los valores de configuración.
* **Configuración Dinámica:** Genera manifiestos que se adaptan basados en lógica condicional, bucles y variables.
* **Evita la Duplicación (DRY - Don't Repeat Yourself):** Define fragmentos comunes una vez y reutilízalos en diferentes partes de tus plantillas.
* **Manejo de Complejidad:** Facilita la gestión de configuraciones complejas de aplicaciones Kubernetes.

---

## 🧱 Conceptos Fundamentales

Helm procesa los archivos de plantilla (generalmente ubicados en el directorio `templates/`) y los combina con los valores que proporcionas (a través de archivos `values.yaml`, la línea de comandos con `--set`, o archivos de valores específicos). El resultado es un conjunto de manifiestos YAML listos para ser aplicados a tu clúster de Kubernetes.

La sintaxis de las plantillas de Go se basa en el uso de `{{ }}` para delimitar las acciones de la plantilla.

---

## 🎯 Operaciones Básicas y Sintaxis

### 1. Acceder a Valores (`{{ .Values.tuValor }}`)

El objeto más comúnmente utilizado es `.Values`. Contiene todos los valores definidos en tu archivo `values.yaml` y los pasados por línea de comando.

**Ejemplo:**

Si tu `values.yaml` contiene:

```yaml
replicaCount: 3
image:
  repository: myapp
  tag: latest