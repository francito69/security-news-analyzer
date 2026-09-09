# Informe de Análisis de Seguridad y Dependencias
**Proyecto:** Security News Analyzer  
**Fecha:** 8 de Septiembre de 2026  
**Entorno:** Python 3.12.6 / pip 26.2.1

---

## 1. Dependencias Directas
Las dependencias directas son aquellas librerías requeridas e instaladas explícitamente para el funcionamiento del código principal de la aplicación (`app.py`):

* **`requests`**: Utilizada para realizar solicitudes HTTP/HTTPS a la URL ingresada por el usuario.
* **`beautifulsoup4`**: Utilizada para realizar el procesamiento (*parsing*) del HTML y extraer el título y texto de la página.

---

## 2. Dependencias Transitivas
Las dependencias transitivas son librerías requeridas indirectamente por las dependencias directas para poder ejecutar sus funciones internas. La estructura jerárquica obtenida mediante `pipdeptree` es la siguiente:

```text
beautifulsoup4==4.15.0
  ├── soupsieve [required: >=1.6.1, installed: 2.9.2]
  └── typing_extensions [required: >=4.0.0, installed: 4.16.0]

requests==2.34.2
  ├── certifi [required: >=2017.4.17, installed: 2026.7.22]
  ├── charset-normalizer [required: >=2,<4, installed: 3.5.1]
  ├── idna [required: >=2.5,<4, installed: 3.19]
  └── urllib3 [required: >=1.21.1,<3, installed: 2.7.0]
```
Análisis: Aunque el proyecto declara solo 2 librerías directas, el entorno ejecuta un total de 8 paquetes en segundo plano.

## 3. Vulnerabilidades Detectadas (SCA)

Se realizó un escaneo de **Software Composition Analysis (SCA)** utilizando la herramienta `pip-audit`.

* **Comando ejecutado:** `pip-audit`
* **Resultado del análisis:**

| Paquete | Versión Instalada | ID Vulnerabilidad | Versión Corregida | Estado |
| :--- | :--- | :--- | :--- | :--- |
| Sin hallazgos | N/A | N/A | N/A | *No known vulnerabilities found* |

**Conclusión del escaneo:** En la revisión actual, ninguna de las dependencias directas ni transitivas presenta vulnerabilidades conocidas registradas en las bases de datos de seguridad.

---

## 4. Plan de Remediación y Gestión de Riesgos

### A. Evaluación del Riesgo en la Cadena de Suministro (*Software Supply Chain*)

* **Superficie de Ataque:** Aunque el código fuente desarrollado solo utiliza sentencias `import` para `requests` y `beautifulsoup4`, la aplicación ejecuta código de componentes de terceros pertenecientes a todas las dependencias transitivas (por ejemplo: `urllib3`, `certifi`).
* **Responsabilidad de Seguridad:** Cualquier vulnerabilidad detectada en una dependencia transitiva afecta la seguridad general de la aplicación. El equipo de desarrollo es responsable de auditar, identificar y remediar fallas en toda la cadena de dependencias.

### B. Protocolo de Remediación ante Alertas Futuras

Si un escaneo futuro con `pip-audit` detecta un fallo de seguridad (ej. un CVE en `urllib3`), se aplicará estrictamente el siguiente procedimiento desde la consola:

1. **Identificación:** Determinar qué versión parcheada corrige el fallo según el reporte generado por `pip-audit`.
2. **Actualización Controlada:** Ejecutar la actualización en el entorno virtual de la librería correspondiente:
   ```bash
   pip install --upgrade <nombre_paquete>
   ```
3. **Pruebas de Regresión:** Validar que la actualización no introduzca *breaking changes*, cambios de comportamiento inesperados en la API o incompatibilidades entre librerías.
4. **Fijación de Versiones:** Regenerar el archivo de congelación de dependencias para asegurar la trazabilidad del código:
   ```bash
   pip freeze > requirements.txt
   ```
5. **Re-auditoría:** Confirmar la eliminación definitiva del riesgo ejecutando nuevamente la herramienta de análisis:
   ```bash
   pip-audit
   ```

