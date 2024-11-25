
# Documentación - API de OpenAI para embeddings de Textos

## ¿Qué es un embedding de texto?
Son representaciones numéricas de cadenas de textos, como palabras, frases, documentos, etc. Las cuales
capturan la información semántica y contextual del texto. Los embedding convierten el texto a vectores
numéricos, los cuales pueden ser procesados por algoritmos de machine learning, determinando similitud 
entre diferentes fragmentos de texto.


## Descripción General

Lo que se busca con la utilización de esta API es, en detalle, extraer texto de archivos PDF en un directorio, generar embeddings a partir de ese texto y compararlos con una consulta (KEYWORDS) de texto para encontrar los documentos más relevantes. La similitud entre los embeddings generados a partir de los documentos y la consulta, son caluclados mediante la función coseno.

## API de OpenAI

### Endpoints Relevantes

En este proyecto, interactuamos con la API de OpenAI para obtener embeddings de texto. El **endpoint principal** que utilizamos es:

- **`POST /v1/embeddings`**: Este endpoint genera representaciones vectoriales (embeddings) de texto.

### Parámetros de la API

Cuando llamamos al endpoint `/v1/embeddings`, necesitamos proporcionar ciertos parámetros:

#### **Modelo (`model`)**

- **Tipo**: Cadena de texto
- **Valor esperado**: `"text-embedding-ada-002"` (Recomendado para generación de embeddings)
- **Descripción**: Este es el modelo preentrenado de OpenAI utilizado para generar los embeddings de texto. "text-embedding-ada-002" es adecuado para tareas de análisis semántico, comparación y búsqueda de similitudes.

#### **Entrada (`input`)**

- **Tipo**: Lista o cadena de texto
- **Descripción**: El texto o los textos que se van a convertir en embeddings. Puede ser un solo texto o una lista de textos. Cada texto se convierte en un vector numérico que representa su contenido semántico.
- **Ejemplo**: `"Agricultura sostenible y sus beneficios en el medio ambiente"`

### **Ejemplo de solicitud a la API**
  ```python
import openai

openai.api_key = "CLAVE_OPENAI"

response = openai.Embedding.create(
    model="text-embedding-ada-002",
    input="Agricultura sostenible y sus beneficios en el medio ambiente"
)

print(response['data'][0]['embedding'])

```
#### **Respuesta de la API**

Cuando la API recibe la solicitud, procesa el texto de entrada y devuelve una **respuesta** en forma de un vector numérico (embedding).
Esta respuetsa incluirá:
* Identificador único de la solicitud.
* Embedding generado en forma de arreglo.

El retorno será utilizado para:
* Realizar búsquedas semánticas y según un input o conjunto de keywords.

Ejemplo de la respuesta de la API:

```json
{
  "data": [
    {
      "embedding": [0.23, -0.13, 0.56, ..., 0.09],
      "index": 0
    }
  ]
}
```

### ¿Cómo lo utilizaremos en el contexto del proyecto?
La idea de utilizar esta API es la selección de las fuentes de información a considerar para la generación del boletín final.
El proceso mencionado se realizará de la siguiente manera:

* Administrador sube "tema" acotado a la web creada, por medio de una vista propia de admin.
* Este "tema" contiene keywords sobre de qué temas necesita que sean incluídos en el boletín final.
* La API toma este input y realiza el "filtrado" de las distintas fuentes de información disponibles, seleccionando las más relevantes.
* Finalmente obtenemos una arreglo con los indices de los boletines que fueron seleccionados.
* El output de la API servirá, posteriormente, como input para la herramienta de IA que hará la generación de los boletines finales.


