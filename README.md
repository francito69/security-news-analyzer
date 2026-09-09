# 🛡️ Security News Analyzer

**Security News Analyzer** es una aplicación desarrollada en Python que analiza artículos o noticias web a partir de una URL proporcionada. El proyecto fue diseñado como un laboratorio práctico para la gestión segura de dependencias y el análisis de la cadena de suministro de software (*Software Supply Chain*).

---

## 🎓 Contexto Académico

- **Curso:** SW707U Construcción de Software II (Herramientas y Tecnologías)  
- **Laboratorio:** Construcción segura de una aplicación Python con pip (Laboratorio 1)  
- **Docente:** ANIBAL JAVIER GUILLEN VASQUEZ  
- **Universidad:** Universidad Nacional de Ingeniería (UNI)
## 🚀 Características

* **Análisis Web:** Extrae el título, conteo de palabras, cantidad de caracteres y la fecha/hora exacta del análisis.
* **Gestión de Entorno:** Uso de entornos virtuales aislados (`.venv`).
* **Auditoría de Seguridad (SCA):** Integración con `pipdeptree` y `pip-audit` para la inspección de dependencias transitivas y detección de vulnerabilidades conocidas.

---

## 🛠️ Requisitos Previos

* Python 3.10+
* Git

---

## 🔧 Instalación y Configuración

1. **Clonar el repositorio:**
   ```bash
   git clone https://github.com/TU_USUARIO/security-news-analyzer.git
   cd security-news-analyzer
   ```

2. **Crear y activar el entorno virtual:**
   * **Linux / macOS:**
     ```bash
     python3 -m venv .venv
     source .venv/bin/activate
     ```
   * **Windows (CMD):**
     ```cmd
     python -m venv .venv
     .venv\Scripts\activate
     ```
   * **Windows (PowerShell):**
     ```powershell
     python -m venv .venv
     .\.venv\Scripts\activate
     ```

3. **Instalar dependencias:**
   ```bash
   pip install -r requirements.txt
   ```

---

## 💻 Uso de la Aplicación

Ejecuta el script principal en tu terminal:
```bash
python app.py
```
Ingresa cualquier URL válida (por ejemplo: `https://www.python.org/`) para obtener el reporte del análisis en pantalla.

---

## 🔒 Auditoría de Seguridad y Dependencias

Para inspeccionar el árbol de dependencias directas e indirectas instaladas en el entorno:
```bash
pipdeptree
```

Para realizar un escaneo completo de vulnerabilidades conocidas (*Software Composition Analysis - SCA*):
```bash
pip-audit
```

---

## 📁 Estructura del Proyecto

```text
security-news-analyzer/
├── .venv/                  # Entorno virtual aislado (Excluido en .gitignore)
├── app.py                  # Código fuente de la aplicación
├── requirements.txt        # Congelamiento de dependencias y versiones
├── README.md               # Documentación general del proyecto
├── .gitignore              # Archivos excluidos del repositorio (ej. .venv)
├── dependency-report.txt   # Reporte en texto plano de pip list y pipdeptree
└── security-report.md      # Informe técnico de auditoría y análisis de riesgos
```
