# 🤖 Automatización del proceso de validación y seguimiento de CUFES

> **Trabajo de Grado — Práctica Profesional**  
> Jorge Luis Reina Quiroga  
> Facultad de Economía, Empresa y Desarrollo Sostenible — FEEDS  
> Universidad De La Salle · 2025  
> Empresa: **Intertek Colombia S.A.**

---

## 📋 Descripción del proyecto

Este proyecto automatiza el proceso de validación y seguimiento de los **Comprobantes Únicos de Facturación Electrónica (CUFE)** en la plataforma de la **DIAN (Dirección de Impuestos y Aduanas Nacionales de Colombia)**.

Antes de esta solución, el área de Facturación de Intertek Colombia realizaba la verificación de manera manual, lo que implicaba:

- ⏱️ **2 minutos por CUFE** consultado manualmente
- 📋 **~300 facturas mensuales** a verificar
- ⏳ **~8 horas mensuales** dedicadas solo a verificaciones
- ⚠️ Alto riesgo de **errores humanos** y duplicación de datos

Con la automatización:

- ✅ **23-25 segundos por CUFE**
- ✅ **~2 horas mensuales** en total
- ✅ Reducción del **80% en tiempo de verificación**
- ✅ Errores humanos prácticamente **nulos**

---

## ⚙️ ¿Cómo funciona?

El modelo opera bajo un flujo secuencial de 4 etapas:

```
📂 Carga Excel con CUFES
        ↓
🌐 Apertura automática del navegador (Selenium)
        ↓
🔐 Resolución automática del CAPTCHA (Capsolver API)
        ↓
🔍 Consulta individual del CUFE en la DIAN
        ↓
📊 Exportación de resultados a Excel consolidado
```

### Estados que identifica (eventos DIAN)

| Código | Estado |
|--------|--------|
| `030` | Acuse de recibo de la factura electrónica de venta |
| `031` | Reclamo de la factura electrónica de venta |
| `032` | Recibo del bien o prestación del servicio |
| `033` | Aceptación expresa de la factura electrónica de venta |
| `034` | Aceptación tácita de la factura electrónica de venta |
| `Sin eventos` | No tiene eventos asociados |

---

## 🗂️ Estructura del proyecto

```
automatizacion-cufes-intertek/
│
├── main.py                          # Script principal
├── .env.example                     # Plantilla de variables de entorno
├── requirements.txt                 # Librerías necesarias
├── README.md                        # Este archivo
│
├── data/
│   └── REVISION_CUFES_2025_134_1.xlsx     # Archivo de entrada (ejemplo)
│
└── output/
    └── REVISION_CUFES_2025_134_1_con_Estado.xlsx  # Resultado generado
```

---

## 🛠️ Instalación y uso

### 1. Requisitos previos

Asegúrate de tener instalado en tu computador:

- [Python 3.8+](https://www.python.org/downloads/)
- [Google Chrome](https://www.google.com/chrome/) (versión actualizada)
- [ChromeDriver](https://chromedriver.chromium.org/) compatible con tu versión de Chrome
- Una cuenta y clave API en [Capsolver](https://capsolver.com/)

### 2. Clonar el repositorio

```bash
git clone https://github.com/TuUsuario/automatizacion-cufes-intertek.git
cd automatizacion-cufes-intertek
```

### 3. Instalar las librerías

```bash
pip install -r requirements.txt
```

### 4. Configurar las variables de entorno

Crea un archivo `.env` en la raíz del proyecto basándote en `.env.example`:

```bash
cp .env.example .env
```

Edita el archivo `.env` y agrega tu clave de Capsolver:

```env
CAPSOLVER_API_KEY=tu_clave_aqui
```

### 5. Preparar el archivo de entrada

Coloca tu archivo Excel en la raíz del proyecto. Debe tener una columna llamada **`CUFE/CUDE`** con los códigos a verificar.

El archivo debe llamarse:
```
REVISION_CUFES_2025_134_1.xlsx
```

### 6. Ejecutar el script

```bash
python main.py
```

El resultado se guardará automáticamente como:
```
REVISION_CUFES_2025_134_1_con_Estado.xlsx
```

---

## 📦 Librerías utilizadas

| Librería | Versión | Propósito |
|----------|---------|-----------|
| `pandas` | ≥1.5.0 | Lectura y escritura de archivos Excel |
| `selenium` | ≥4.0.0 | Automatización del navegador web |
| `capsolver` | ≥0.0.7 | Resolución automática del CAPTCHA |
| `python-dotenv` | ≥0.21.0 | Manejo seguro de credenciales |
| `openpyxl` | ≥3.0.0 | Soporte para archivos .xlsx |

Instálalas todas con:

```bash
pip install pandas selenium capsolver python-dotenv openpyxl
```

---

## 🔐 Seguridad

- La clave API de Capsolver se almacena en un archivo `.env` que **nunca se sube a GitHub**
- El archivo `.gitignore` excluye automáticamente `.env` y los archivos Excel con datos reales
- Los archivos de entrada y salida con datos de facturas reales **no se incluyen** en el repositorio

---

## ⚠️ Consideraciones importantes

> **Este script NO es ejecutable en línea** (GitHub, Google Colab, etc.)  
> Requiere ejecutarse **localmente** porque:
> - Utiliza **Google Chrome** instalado en el equipo
> - Automatiza la navegación con **Selenium WebDriver**
> - Accede directamente a la plataforma web de la **DIAN**
> - La clave API de **Capsolver** debe estar configurada en `.env`

---

## 🏢 Contexto empresarial

**Intertek Colombia S.A.** (NIT 800.069.554-8) es una empresa especializada en aseguramiento de calidad, certificación y evaluación técnica. Este proyecto fue desarrollado en el área de **Facturación** como parte de la modalidad de Práctica Profesional.

**Normativa aplicada:**
- Resolución DIAN 000042 de 2020 — Facturación electrónica en Colombia
- Decreto 2242 de 2015 — Condiciones de expedición e interoperabilidad

---

## 👨‍💻 Autor

**Jorge Luis Reina Quiroga**  
Estudiante de pregrado — Facultad de Economía, Empresa y Desarrollo Sostenible  
Universidad De La Salle — Bogotá, Colombia  
Práctica Profesional en Intertek Colombia S.A. · 2025

---

## 📄 Licencia

Este proyecto fue desarrollado con fines académicos como parte del trabajo de grado de la Universidad De La Salle. Su uso está restringido al contexto educativo e investigativo.

---

*"La automatización no es solo un cambio técnico, sino también cultural y estratégico."*  
— Davenport (1998)
