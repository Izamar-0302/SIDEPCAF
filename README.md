# 🌿 AgroDetect

**Sistema Inteligente para la Detección de Enfermedades y Plagas Foliares en el Cultivo de Café**

> Un anteproyecto de Inteligencia Artificial aplicado a la caficultura de Comayagua, Honduras.

[![Estado](https://img.shields.io/badge/estado-en%20desarrollo-yellow)]()
[![Licencia](https://img.shields.io/badge/licencia-MIT-blue)]()
[![Python](https://img.shields.io/badge/Python-3.10%2B-blue)]()
[![Streamlit](https://img.shields.io/badge/UI-Streamlit-FF4B4B)]()

---

## 📖 Índice

- [Descripción del proyecto](#-descripción-del-proyecto)
- [Problema que resuelve](#-problema-que-resuelve)
- [Objetivos](#-objetivos)
- [Enfermedades y plagas detectadas](#-enfermedades-y-plagas-detectadas)
- [Arquitectura de la solución](#-arquitectura-de-la-solución)
- [Tecnologías utilizadas](#-tecnologías-utilizadas)
- [Datasets utilizados](#-datasets-utilizados)
- [Instalación](#-instalación)
- [Uso](#-uso)
- [Estructura del repositorio](#-estructura-del-repositorio)
- [Cronograma](#-cronograma)
- [Beneficiarios](#-beneficiarios)
- [Mantenimiento y mejoras futuras](#-mantenimiento-y-mejoras-futuras)
- [Equipo](#-equipo)
- [Licencia](#-licencia)
- [Referencias](#-referencias)

---

## 🌱 Descripción del proyecto

El café es uno de los pilares de la economía hondureña, generando ingresos directos e indirectos para cientos de miles de familias. Sin embargo, la caficultura enfrenta amenazas recurrentes como la **roya del café** (*Hemileia vastatrix*), la **cercospora**, la **phoma**, y plagas como la **araña roja** y el **minador de la hoja**, que reducen el rendimiento y la calidad del grano.

**AgroDetect** es un sistema basado en **visión artificial** y **aprendizaje profundo** que, a partir de una fotografía tomada con un teléfono móvil, clasifica el estado de salud de una hoja de café y sugiere la enfermedad o plaga presente, funcionando como una primera línea de apoyo al diagnóstico agronómico para productores con acceso limitado a asistencia técnica especializada.

## 🎯 Problema que resuelve

En la actualidad, el diagnóstico de enfermedades foliares depende casi exclusivamente de la inspección visual del productor o de un técnico agrónomo, un método lento, subjetivo y poco accesible en fincas pequeñas, medianas o de difícil acceso geográfico —una realidad común en la región de Comayagua, Honduras.

**AgroDetect** busca reducir esa brecha ofreciendo un diagnóstico **rápido, objetivo y accesible desde un smartphone**.

## 🎯 Objetivos

**Objetivo general:** desarrollar un sistema de IA para la detección y clasificación de enfermedades y plagas foliares del café, como herramienta de apoyo al diagnóstico fitosanitario de productores de Comayagua, Honduras.

**Objetivos específicos:**

- Recopilar y curar un dataset de imágenes de hojas de café sanas y afectadas.
- Entrenar un modelo de clasificación basado en CNN mediante *transfer learning*.
- Evaluar el modelo con métricas estándar (exactitud, precisión, sensibilidad, F1-score).
- Desarrollar una interfaz web accesible para subir/capturar fotos y recibir diagnóstico.
- Integrar un módulo de recomendaciones agronómicas basado en un LLM.
- Desplegar la solución en una plataforma en la nube gratuita.
- Definir una estrategia de mantenimiento y mejora continua.

## 🍃 Enfermedades y plagas detectadas

| Clase | Tipo | Alcance |
|---|---|---|
| Roya (*Hemileia vastatrix*) | Enfermedad | Clasificación de la enfermedad |
| Cercospora | Enfermedad | Presencia/ausencia en la hoja |
| Phoma | Enfermedad | Presencia/ausencia en la hoja |
| Araña roja (*red spider mite*) | Plaga | Presencia/ausencia en la hoja |
| Minador de la hoja (*leaf miner*) | Plaga | Presencia/ausencia en la hoja |

*(+ clase adicional: hoja sana)*

## 🏗️ Arquitectura de la solución

```
📷 Foto de la hoja
      │
      ▼
🧠 Modelo CNN (Transfer Learning)
   MobileNetV2 / ResNet50 / EfficientNet
      │
      ▼
🔎 Clasificación (sana / roya / cercospora / phoma / araña roja / minador)
      │
      ▼
💬 API de Groq (LLM) ──► Recomendaciones agronómicas
      │
      ▼
🖥️ Interfaz Streamlit ──► Resultado + recomendación al productor
```

Todo el flujo corre en un **único servicio de Streamlit**: la app entrena/carga el modelo de visión, clasifica la imagen, y llama directamente a la **API de Groq** con una API key (gestionada como *secret*) para generar las recomendaciones de manejo agronómico — sin necesidad de un backend independiente.

## 🛠️ Tecnologías utilizadas

| Categoría | Herramienta / Tecnología |
|---|---|
| Lenguaje de programación | Python |
| Frameworks de Deep Learning | TensorFlow / Keras (alternativa: PyTorch) |
| Procesamiento de imágenes | OpenCV, Pillow |
| Entrenamiento y experimentación | Google Colab (GPU gratuita) |
| Etiquetado y gestión de datasets | Roboflow |
| Interfaz de usuario | Streamlit |
| Recomendaciones mediante LLM | API de Groq (API key) |
| Control de versiones | Git y GitHub |
| Documentación y análisis | Jupyter Notebook, pandas, matplotlib |

## 📊 Datasets utilizados

El proyecto trabaja exclusivamente con imágenes de repositorios públicos ya etiquetados:

- **RoCoLe** — A Robusta Coffee Leaf Images Dataset ([Mendeley Data](https://data.mendeley.com/datasets/c5yvn32dzg/2) / [Kaggle](https://www.kaggle.com/datasets/nirmalsankalana/rocole-a-robusta-coffee-leaf-images-dataset))
- **CLR-Dataset** ([GitHub](https://github.com/dvelaren/clr-dataset))
- **Coffee Leaf Disease** y variantes ([Roboflow Universe](https://universe.roboflow.com/dame-23kub/coffee-leaf-disease-kc1ca))
- **Ethiopian Coffee Leaf Disease** ([Kaggle](https://www.kaggle.com/datasets/biniyamyoseph/ethiopian-coffee-leaf-disease))
- **JMuBEN Coffee Dataset** ([Kaggle](https://www.kaggle.com/datasets/noamaanabdulazeem/jmuben-coffee-dataset))
- **Red Spider Mite** y **ROCC** ([Roboflow Universe](https://universe.roboflow.com/lance-eugene/red-spider-mite))

> La lista completa de repositorios y referencias bibliográficas está disponible en el [anteproyecto](./docs/anteproyecto.pdf).

## ⚙️ Instalación

```bash
# Clonar el repositorio
git clone https://github.com/<tu-usuario>/agrodetect.git
cd agrodetect

# Crear entorno virtual
python -m venv venv
source venv/bin/activate      # En Windows: venv\Scripts\activate

# Instalar dependencias
pip install -r requirements.txt
```

Configura tu API key de Groq como variable de entorno o en `.streamlit/secrets.toml`:

```toml
# .streamlit/secrets.toml
GROQ_API_KEY = "tu_api_key_aqui"
```

## ▶️ Uso

```bash
streamlit run app.py
```

1. Sube o captura una fotografía de una hoja de café.
2. El modelo de visión clasifica la imagen (sana, enfermedad o plaga).
3. La app consulta la API de Groq y muestra recomendaciones de manejo agronómico.
4. Consulta el resultado y, de ser necesario, contacta a un técnico del IHCAFE.

## 📁 Estructura del repositorio

```
agrodetect/
├── app.py                  # Aplicación principal de Streamlit
├── model/                  # Modelo entrenado y scripts de entrenamiento
├── notebooks/              # Notebooks de exploración y entrenamiento (Colab/Jupyter)
├── data/                   # Scripts de descarga/organización de datasets
├── docs/                   # Anteproyecto y documentación
├── requirements.txt
└── README.md
```

## 🗓️ Cronograma

Proyecto desarrollado en un plazo de **dos semanas** (14–27 de julio de 2026):

| Semana | Fechas | Actividades |
|---|---|---|
| 1 | 14 jul | Planificación y asignación de tareas |
| 1 | 15–16 jul | Recolección de datasets |
| 1 | 17–18 jul | Preprocesamiento y *data augmentation* |
| 1 | 19–20 jul | Entrenamiento inicial del modelo CNN |
| 2 | 21–22 jul | Evaluación y ajuste de hiperparámetros |
| 2 | 23 jul | Integración del módulo de recomendaciones (Groq) |
| 2 | 24 jul | Desarrollo de la interfaz Streamlit |
| 2 | 25 jul | Despliegue en Streamlit Community Cloud |
| 2 | 26–27 jul | Ajustes finales y documentación |

## 👥 Beneficiarios

- Pequeños y medianos productores de café de Comayagua.
- Técnicos agrónomos y extensionistas del IHCAFE.
- Cooperativas y asociaciones de caficultores.
- Estudiantes y docentes de carreras agronómicas.

## 🔧 Mantenimiento y mejoras futuras

- Reentrenamiento periódico del modelo con nuevas imágenes.
- Versionado de modelos entrenados.
- Actualización del *prompt* del módulo de recomendaciones.
- Futuras mejoras: incorporación de la broca del café, app móvil offline, mapa de incidencia por zona geográfica.

## 👨‍💻 Equipo

Proyecto desarrollado para la asignatura de **Inteligencia Artificial**, UNAH — Campus Comayagua (UNAH-CURC).

- Jeimy Jazmín Palma Santos — 20221900269
- Ángeles Izamar Euceda Herrera — 20221930061
- Kilver Said Nolasco Parada — 20221930129

**Docente:** Asalia Alejandra Zavala

## 📄 Licencia

Este proyecto se distribuye bajo la licencia MIT. Ver [LICENSE](./LICENSE) para más detalles.

## 📚 Referencias

Las referencias completas de los datasets utilizados están disponibles en la sección de **Referencias bibliográficas** del [anteproyecto](./docs/anteproyecto.pdf).

---

<p align="center">Hecho con ☕ y 🧠 en Comayagua, Honduras</p>
