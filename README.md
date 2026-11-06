# Guía de Ejecución: Evaluación Parcial N°1 - Solución RAG (Aseguradora del Pacífico)
**Asignatura:** ISY0101 - Ingeniería de Soluciones con IA | **Duoc UC**  
**Estudiantes:** Luciano Fernando & Ivan Santander

Este documento detalla el paso a paso para configurar el entorno de ejecución, gestionar las credenciales de forma segura y ejecutar con éxito el pipeline RAG y el marco de evaluación de métricas.

---

## Requisitos Previos
1. Una cuenta de Google para acceder a **Google Colab**.
2. Una cuenta gratuita en **Groq Cloud** para obtener una API Key (la cual permite inferencia rápida y gratuita con modelos abiertos).

---

## Paso 1: Configurar la API Key de forma segura en Google Colab Secrets
Para evitar exponer credenciales en el código fuente, utilizaremos el gestor de secretos nativo de Google Colab:

1. Abre tu archivo Jupyter Notebook en Google Colab (`EP1_ISY0101_Aseguradora_Pacifico.ipynb`).
2. Dirígete al panel izquierdo de Google Colab y haz clic en el ícono de la **llave inglesa / 🔑 (Secrets)**.
3. Haz clic en el botón **+ Add new secret**.
4. Completa los campos exactamente con los siguientes valores:
   - **Name:** `GROQ_API_KEY`
   - **Value:** `gsk_TU_API_KEY_DE_GROQ_AQUI` (pega tu clave real obtenida en Groq).
5. Asegúrate de activar el interruptor **Notebook access** para permitir que el script lea el secreto.

---

## Paso 2: Ejecución del Notebook en Orden Secuencial

Una vez configurado el secreto, ejecuta las celdas del notebook de arriba hacia abajo:

### 1. Celda de Dependencias e Inicialización:
* **Qué hace:** Instala las librerías necesarias (`langchain-text-splitters`, `langchain-huggingface`, `openai`, `scikit-learn`, etc.), carga el modelo de embeddings localmente (`all-MiniLM-L6-v2`) y extrae de forma segura la `GROQ_API_KEY` desde los Secrets de Colab para inicializar el cliente de Groq.
* **Resultado esperado:** Mensaje `✅ Conectado de forma segura usando Google Colab Secrets.`

### 2. Celda del Pipeline RAG y Corpus Documental:
* **Qué hace:** Carga el corpus documental base de la Aseguradora del Pacífico, aplica la fragmentación con `RecursiveCharacterTextSplitter` (`chunk_size=350`), y define las funciones de recuperación semántica por similitud de coseno y de generación con el LLM.

### 3. Celda de Ejecución del Dataset de Evaluación y Métricas:
* **Qué hace:** Ejecuta las consultas de prueba, mide el tiempo de respuesta, calcula la precisión del contexto y evalúa la **Fidelidad** de las respuestas mediante el marco automatizado.
* **Resultado esperado:** Se genera una tabla consolidada en formato `DataFrame` de Pandas mostrando la pregunta, la respuesta generada, la fidelidad (escala 1-10), la precisión del contexto y el tiempo total de procesamiento.

---

## Estructura del Repositorio de Entrega
* `EP1_ISY0101_Aseguradora_Pacifico.ipynb`: Notebook principal con todo el código ejecutable y las reflexiones obligatorias.
* `Informe_EP1_RAG_Aseguradora.html` / PDF: Informe técnico estructurado de acuerdo con los requerimientos de la rúbrica de Duoc UC.
* `README_EP1.md`: Este instructivo técnico.
