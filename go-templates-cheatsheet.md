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

### Acceder a Valores (`{{ .Values.tuValor }}`)

El objeto más comúnmente utilizado es `.Values`. Contiene todos los valores definidos en tu archivo `values.yaml` y los pasados por línea de comando.

**Ejemplo:**

Si tu `values.yaml` contiene:

```yaml
replicaCount: 3
image:
  repository: myapp
  tag: latest
```

### **Operador If/Else**

```yaml
{{ if PIPELINE }}
  # Do something
{{ else if OTHER PIPELINE }}
  # Do something else
{{ else }}
  # Default case
{{ end }}
```

### **Modifying scope using with**
```yaml
  {{- with .Values.favorite }}
  drink: {{ .drink | default "tea" | quote }}
  food: {{ .food | upper | quote }}
  release: {{ $.Release.Name }}  #$ is mapped to the root scope
  {{- end }}
```

### **Looping with the range action**

```yaml
favorite:
  drink: coffee
  food: pizza
pizzaToppings:
  - mushrooms
  - cheese
  - peppers
  - onions
  - pineapple
```
Utilizando: 
```yaml
  toppings: |-
    {{- range .Values.pizzaToppings }}
    - {{ . | title | quote }}
    {{- end }}
```

Finalmente:
```yaml
  toppings: |-
    - "Mushrooms"
    - "Cheese"
    - "Peppers"
    - "Onions"
    - "Pineapple"
```

The ``|-`` marker in YAML takes a multi-line string. This can be a useful technique for embedding big blocks of data inside of your manifests, as exemplified here.

### **Variables**

``{{- $relname := .Release.Name -}}``

```yaml
 toppings: |-
    {{- range $index, $topping := .Values.pizzaToppings }}
      {{ $index }}: {{ $topping }}
    {{- end }} 
```
Finalmente:
```yaml
  toppings: |-
      0: mushrooms
      1: cheese
      2: peppers
      3: onions  
```

### **Define y template**

[doc](https://helm.sh/docs/chart_template_guide/named_templates/)
Para reutilizar bloques de codigo

```yaml
{{- define "mychart.labels" }}
  labels:
    generator: helm
    date: {{ now | htmlDate }}
{{- end }} 
```
Se utiliza llamando con
```yaml
{{- template "mychart.labels" }}
```

### **The include function**

Se considera preferible utilizar la opción de incluir en lugar de plantilla en las plantillas de Helm simplemente para que el formato de salida se pueda manejar mejor para los documentos YAML.

Permite manejas las indentaciones.
```yaml
{{ include "mychart.app" . | indent 4 }}
```

### Notas
``{{-`` indica que los espacios en blanco deben consumirse a la izquierda.
``-}}`` significa que los espacios en blanco a la derecha deben consumirse.

ejemplo de mal uso:

```yaml
  food: {{ .Values.favorite.food | upper | quote }}
  {{- if eq .Values.favorite.drink "coffee" -}}
  mug: "true"
  {{- end -}}
```
resultado: ``food: "PIZZA"mug: "true"``