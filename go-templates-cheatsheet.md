Cheatsheet Básico de Go Template: Control de Flujo
Este cheatsheet te ayudará a entender las estructuras más comunes que ves en los templates de Go (a menudo usados en herramientas como Helm para Kubernetes). Piensa en esto como la lógica que le dice a tu plantilla qué mostrar y cuándo.

Conceptos Básicos
{{ ... }}: Estas son las delimitaciones que indican que lo que está dentro es código de template de Go y no texto plano. Es como el "portal" a la magia de la plantilla.
. (El punto): Representa el contexto actual. Si estás en el nivel superior, es el objeto principal. Si estás dentro de un range o with, representa el elemento actual que estás procesando. Es como tu ubicación actual en un mapa.
.Values: En Helm, .Values es un objeto especial que contiene todas las variables de configuración que le pasas a tu chart. Imagina que es una caja con todos los interruptores y configuraciones para tu aplicación.
.Values.miVariable: Accede a una variable específica llamada miVariable dentro del objeto .Values.
Control de Flujo: if (Condicionales)
El if te permite ejecutar un bloque de código solo si una condición es verdadera.

Go

{{- if .Values.secret.enabled }}
    # Si .Values.secret.enabled es 'true', este bloque se mostrará.
    # Por ejemplo, puedes incluir configuraciones de secretos aquí.
    apiVersion: v1
    kind: Secret
    metadata:
      name: my-app-secret
    data:
      api_key: {{ .Values.secret.apiKey | b64enc }}
{{- end }}
{{- y -}}: Estos guiones (-) al principio o al final de las delimitaciones eliminan los espacios en blanco adyacentes (saltos de línea o espacios). Esto es útil para que tu YAML o configuración generada quede limpia sin líneas vacías inesperadas.
Control de Flujo: range (Bucles/Iteraciones)
El range te permite iterar sobre listas o mapas, ejecutando un bloque de código por cada elemento.

Go

{{- range .Values.myList }}
    # Este bloque se ejecutará una vez por cada elemento en .Values.myList
    # Dentro de este bloque, el punto '.' representa el elemento actual.
    - name: {{ .name }}
      value: {{ .value }}
{{- end }}
Ejemplo con range para crear múltiples objetos:

Si tienes una lista de servicios en tus .Values y quieres crear un servicio de Kubernetes para cada uno:

values.yaml (parte del archivo de valores)

YAML

myServices:
  - name: frontend-service
    port: 80
  - name: backend-service
    port: 8080
template.yaml (parte de tu plantilla)

Go

{{- range .Values.myServices }}
---
apiVersion: v1
kind: Service
metadata:
  name: {{ .name }}
spec:
  selector:
    app: my-app
  ports:
    - protocol: TCP
      port: {{ .port }}
      targetPort: {{ .port }}
{{- end }}
En este ejemplo:

{{- range .Values.myServices }}: Le dice a la plantilla que recorra cada elemento dentro de la lista myServices.
Dentro del range, . (el punto) se refiere al elemento actual de la lista. Así, .name accedería al nombre del servicio actual (por ejemplo, frontend-service) y .port a su puerto (por ejemplo, 80).
¡Espero que este cheatsheet te sea muy útil! ¿Hay alguna otra parte de los templates de Go que te gustaría que te explique?