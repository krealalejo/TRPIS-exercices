# 🧩 Enunciado del ejercicio — Diseño UML: Exportador de listas de dispositivos

## 📘 Contexto

Se requiere diseñar (y opcionalmente implementar y testear) una funcionalidad que permita **exportar una lista de dispositivos** a un formato de salida concreto (por ahora **JSON** o **CSV**).

El objetivo principal del ejercicio es **el diseño del sistema**, aplicando los principios de:

- **Alta cohesión**
- **Bajo acoplamiento**
- **Preferencia de composición sobre herencia**

## 🎯 Objetivo del ejercicio

- Diseñar, usando un diagramas de **clases** (UML), que permita exportar listas de dispositivos a diferentes formatos.
- Se debe plantear el diseño pensando en la mantenibilidad y evolución del software.
- (Opcional) Implementar el diseño y crear test unitarios automáticos usando la filosofía BDD y utilizando la notación **Gherkin**.

## 💾 Datos del dominio

Un **Device** tiene la siguiente estructura:

| Campo         | Tipo                  | Descripción                                                 |
| ------------- | --------------------- | ----------------------------------------------------------- |
| `id`          | `string`              | Identificador único del dispositivo                         |
| `name`        | `string`              | Nombre descriptivo del dispositivo                          |
| `mac`         | `Mac`                 | Dirección MAC en formato estándar (ej: `AA:BB:CC:DD:EE:FF`) |
| `geolocation` | `Location`            | Objeto con `lat` (float) y `lon` (float)                    |
| `telemetry`   | `List<TelemetryItem>` | Lista de pares `{ name: string, value: string }`            |

## Ubiquitous Language

| **Term**          | **Descripción**                                                                          |
| ----------------- | ---------------------------------------------------------------------------------------- |
| **Device**        | Entidad que representa un dispositivo con id, nombre, mac, geolocalización y telemetría. |
| **Location**      | Objeto que contiene `lat` y `lon`.                                                       |
| **TelemetryItem** | Conjunto de pares `name:value` asociados al dispositivo.                                 |
| **Formatter**     | Define el transformador a un formato.                                                    |

## 🧭 Punto de entrada

El programa recibirá **dos parámetros**:

1. **La lista de dispositivos**, un string con formato interno **JSON** (entrada).
2. **El formato de salida** deseado (`"json"` o `"csv"` por ahora).

> El sistema debe parsear la entrada, transformarla al formato de exportación y generar un único archivo de salida con el contenido correctamente formateado.

## ⚙️ Requisitos funcionales mínimos

1. Parsear la lista de dispositivos desde un archivo JSON.
2. Exportar la lista completa en uno de los siguientes formatos:
   - JSON
   - CSV
3. Gestionar errores de entrada con mensajes claros (JSON malformado, formato desconocido, etc.).

## 📄 Ejemplo de entrada y salida

### 🔹 Ejemplo JSON de entrada

```text
'[{"id":"d1","name":"Sensor puerta","mac":"AA:BB:CC:11:22:33","geolocation":{"lat":40.4168,"lon":-3.7038},"telemetry":[{"name":"temperatura","value":"22.5"},{"name":"bateria","value":"85%"}]},{"id":"d2","name":"Cámara 1","mac":"FF:EE:DD:44:55:66","geolocation":{"lat":41.3851,"lon":2.1734},"telemetry":[]}]'
```

### 🔹 Ejemplo JSON de salida

```json
[
  {
    "id": "d1",
    "name": "Sensor puerta",
    "mac": "AA:BB:CC:11:22:33",
    "geolocation": { "lat": 40.4168, "lon": -3.7038 },
    "telemetry": [
      { "name": "temperatura", "value": "22.5" },
      { "name": "bateria", "value": "85%" }
    ]
  },
  {
    "id": "d2",
    "name": "Cámara 1",
    "mac": "FF:EE:DD:44:55:66",
    "geolocation": { "lat": 41.3851, "lon": 2.1734 },
    "telemetry": []
  }
]
```

🔹 Ejemplo CSV de salida

```csv
id,name,mac,lat,lon,telemetry
d1,"Sensor puerta","AA:BB:CC:11:22:33",40.4168,-3.7038,"temperatura=22.5;bateria=85%"
d2,"Cámara 1","FF:EE:DD:44:55:66",41.3851,2.1734,""
```

## 📦 Entregables

- **Diagrama UML de clases**: mostrar las principales clases y sus relaciones (interfaces, dependencias, composición).
- **Justificación de diseño**: explicar cómo el diseño cumple los principios de alta cohesión, bajo acoplamiento y composición sobre herencia.

### 💡 Entregables opcionales (valor añadido)

- **Implementación funcional** del diseño en el lenguaje que prefieras.
- **Suite de tests BDD** con **Gherkin**.

\*\* Si entregas código: incluye instrucciones claras para ejecutar la exportación y correr los tests

## 🧠 Criterios de evaluación

| **Criterio**             | **Descripción**                                                             |
| ------------------------ | --------------------------------------------------------------------------- |
| **Corrección**           | Cumple los requisitos funcionales mínimos.                                  |
| **Calidad del diseño**   | Claridad en la responsabilidad de cada clase, modularidad y extensibilidad. |
| **Principios aplicados** | Cumplimiento de alta cohesión, bajo acoplamiento y composición.             |
| **Documentación**        | Diagramas y justificaciones claros y completos.                             |
| **Pruebas (opcional)**   | Casos relevantes cubiertos con BDD y escenarios bien definidos.             |

### Preguntas para aplicar al diseño

- ¿Cómo cambiaría el diseño si metemos nuevos formatos de salida?
- ¿Cómo cambiaría el diseño si tenemos otros tipos de datos a exportar además del dispositivo?
- ¿Cómo cambiaría el diseño si además de a archivo tuviésemos que exportarlo de otra forma (EJ: enviándolo a un servidor)?
- ¿Cómo cambiaría el diseño si tuviesemos otros formatos de entrada que no fuesen JSON?