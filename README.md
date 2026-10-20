# 🩺 Clinical RAG Agent (HealthTech AI)

Asistente inteligente de apoyo a la decisión clínica con **cero tolerancia a alucinaciones** y **trazabilidad bibliográfica estricta**, desarrollado para procesar Guías de Práctica Clínica (GPC).

---

## 🚀 Descripción del Proyecto

La Inteligencia Artificial en el sector salud se enfrenta a un desafío crítico: las **alucinaciones** de los modelos de lenguaje y la falta de trazabilidad bibliográfica. Este proyecto resuelve dicho problema implementando una arquitectura **RAG (Retrieval-Augmented Generation)** estricta, diseñada para que un LLM responda consultas clínicas **únicamente** utilizando fragmentos verificados de guías oficiales en PDF (como las GPC del Ministerio de Salud o directrices internacionales), indicando la fuente y el número de página exacto.

---

## 🛠️ Arquitectura y Stack Tecnológico

```
[ Guías Médicas PDF ] 
         │
         ▼
[ Ingesta & Chunking (RecursiveCharacterTextSplitter) ]
         │
         ▼
[ Embeddings Vectoriales (HuggingFace: all-MiniLM-L6-v2) ] ──► [ Almacenamiento en Memoria (InMemoryVectorStore) ]
                                                                        │
[ Consulta Médica del Usuario ] ────────────────────────────────────────┤
                                                                        ▼
                                                        [ Recuperación Semántica (Top-k Chunks) ]
                                                                        │
                                                                        ▼
[ Respuesta Estructurada y Trazable ] ◄──────────────── [ LLM con Prompt Clínico Estricto (Google Gemini) ]

```

* **Frontend & Interfaz:** `Streamlit` (Desplegado interactivamente en la nube).
* **Orquestador RAG:** `LangChain` & `LangChain Community`.
* **Procesamiento de Documentos:** `PyPDF` & `RecursiveCharacterTextSplitter` (Segmentación por fragmentos de 1000 tokens con *overlap*).
* **Embeddings:** `Sentence-Transformers` (`all-MiniLM-L6-v2`).
* **Motor de Razonamiento (LLM):** Google Gemini (`gemini-3.8-flash`) con temperatura `0.0` para máxima determinabilidad.

---

## 🛡️ Características Principales

1. **Cero Alucinaciones (*Strict Grounding*):** El *System Prompt* restringe al modelo de forma absoluta. Si la respuesta no está contenida en el documento cargado, el agente responde de manera controlada: *"No dispongo de suficiente evidencia documentada..."*.
2. **Trazabilidad de Fuentes:** Cada respuesta incluye un panel desplegable con los fragmentos textuales originales y el **número de página exacto** de la guía consultada.
3. **Privacidad y Procesamiento Eficiente:** Diseñado con un pipeline modular compatible con modelos *Open Source* y APIs seguras, idóneo para entornos de salud regulados.

---

## 💻 Instalación y Uso Local

1. Clona el repositorio:
```bash
git clone https://github.com/JuanVelasco4574/clinical-rag-agent.git
cd clinical-rag-agent

```


2. Instala las dependencias:
```bash
pip install streamlit pypdf langchain langchain-community langchain-google-genai sentence-transformers

```


3. Ejecuta la aplicación:
```bash
streamlit run app.py

```



---

## 🎯 Impacto y Casos de Uso

* **Apoyo a la Práctica Médica:** Consulta rápida y validada de normativas y pautas de tratamiento en segundos.
* **Educación Médica:** Verificación ágil de criterios diagnósticos en estudiantes y profesionales de la salud.
* **Eficiencia Administrativa:** Automatización del análisis de documentación clínica de alta densidad.
