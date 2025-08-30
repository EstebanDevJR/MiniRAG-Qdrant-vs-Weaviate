# Mini-RAG: Comparación Qdrant vs Weaviate

Este notebook implementa y compara dos sistemas Mini-RAG (Retrieval-Augmented Generation) utilizando diferentes bases de datos vectoriales para evaluar su rendimiento, latencia y facilidad de uso.

## 📋 Descripción

El proyecto construye sistemas RAG completos que combinan:
- **Bases de datos vectoriales**: Qdrant y Weaviate
- **Modelo de embeddings**: `sentence-transformers/all-MiniLM-L6-v2`
- **Modelo de generación**: `google/flan-t5-small`
- **Corpus de datos**: 30 documentos con metadatos completos
- **Métricas de evaluación**: Precision@k, Recall@k y nDCG@k

## 🎯 Objetivos

1. **Construir Mini-RAG** con ambas bases vectoriales
2. **Evaluar rendimiento** usando métricas estándar de recuperación de información
3. **Comparar latencia** y tiempos de respuesta
4. **Implementar filtrado** por metadatos y consultas híbridas
5. **Analizar facilidad de uso** de cada sistema

## 🛠️ Tecnologías Utilizadas

### Dependencias Principales
```python
qdrant-client          # Cliente para Qdrant
weaviate-client        # Cliente para Weaviate  
sentence-transformers  # Modelos de embeddings
transformers          # Modelos de generación
pandas               # Manipulación de datos
numpy                # Operaciones numéricas
scikit-learn         # Métricas de evaluación
tqdm                 # Barras de progreso
rich                 # Visualización mejorada
```

## 📊 Corpus de Datos

El notebook utiliza un corpus de **30 documentos** cuidadosamente seleccionados que cubren múltiples categorías:

- **Medicina**: IA en medicina, células madre, neuroplasticidad
- **Tecnología**: Blockchain, VPN, machine learning, Python vs JavaScript
- **Ciencia**: Atmósfera, fotosíntesis, estrellas fugaces
- **Física**: Relatividad, Big Bang, arcoíris
- **Historia**: Imprenta, Renacimiento, Marie Curie
- **Salud**: Té verde, ejercicio, fibra alimentaria
- **Ambiente**: Cambio climático, CO₂, economía circular
- **Y más categorías...**

Cada documento incluye metadatos completos:
```python
{
    "id": 1,
    "title": "Título del documento",
    "text": "Contenido completo...",
    "source": "Fuente de información",
    "date": "2024-06-12",
    "category": "medicina"
}
```

## 🔍 Funcionalidades Implementadas

### 1. **Sistemas RAG Completos**
- Indexación automática de documentos
- Búsqueda semántica por similitud
- Generación de respuestas contextualmente relevantes
- Manejo de metadatos y filtros

### 2. **Métricas de Evaluación**
- **Precision@k**: Proporción de documentos relevantes en los k primeros resultados
- **Recall@k**: Proporción de documentos relevantes recuperados
- **nDCG@k**: Normalized Discounted Cumulative Gain (considera orden de relevancia)

### 3. **Filtrado Avanzado**
- Filtros por categoría
- Filtros por rango de fechas
- Consultas híbridas (texto + metadatos)

### 4. **Análisis de Rendimiento**
- Medición de latencia de búsqueda
- Tiempo total de procesamiento
- Comparación estadística detallada

## 🚀 Cómo Ejecutar

### 1. **Instalación de Dependencias**
```bash
pip install qdrant-client weaviate-client sentence-transformers transformers accelerate pandas numpy scikit-learn tqdm rich
```

### 2. **Ejecución del Notebook**
1. Abrir `MiniRAG_Qdrant_vs_Weaviate.ipynb` en Jupyter/Colab
2. Ejecutar todas las celdas secuencialmente
3. El notebook se encarga de:
   - Descargar y configurar los modelos
   - Crear las bases de datos vectoriales
   - Indexar los documentos
   - Ejecutar las evaluaciones
   - Mostrar los resultados comparativos

### 3. **Estructura de Ejecución**
```
1. Configuración de modelos (FLAN-T5 + MiniLM)
2. Creación del corpus de 30 documentos
3. Implementación de métricas de evaluación
4. Configuración e indexación en Qdrant
5. Configuración e indexación en Weaviate (simulado)
6. Implementación de clases RAG
7. Evaluación completa con 10 preguntas de prueba
8. Análisis comparativo y visualización
9. Ejemplos de filtrado por metadatos
```

## 📈 Resultados y Métricas

El notebook genera una tabla comparativa completa:

| Sistema | P@5 | R@5 | nDCG@5 | Latencia Búsqueda (ms) | Tiempo Total (ms) |
|---------|-----|-----|--------|----------------------|-------------------|
| Qdrant  | X.XXX | X.XXX | X.XXX | XX.X | XXX.X |
| Weaviate| X.XXX | X.XXX | X.XXX | XX.X | XXX.X |

### Preguntas de Evaluación
El sistema evalúa 10 preguntas cuidadosamente diseñadas:
1. "¿En qué áreas de la medicina se usa la inteligencia artificial?"
2. "¿Cuál es la función principal de la fotosíntesis?"
3. "¿Qué propone la teoría del Big Bang sobre el origen del universo?"
4. "¿Cuáles son las capas de la atmósfera terrestre?"
5. Y más...

## 🔧 Características Técnicas

### Qdrant
- **Ventajas**: API simple, configuración directa, índices HNSW optimizados
- **Ideal para**: Aplicaciones que priorizan velocidad y simplicidad
- **Configuración**: Base de datos embebida local

### Weaviate
- **Ventajas**: Esquemas ricos, manejo complejo de metadatos, GraphQL integrado
- **Ideal para**: Aplicaciones con esquemas complejos y consultas avanzadas
- **Implementación**: Simulada para comparación justa

### Modelos Utilizados
- **Embeddings**: `all-MiniLM-L6-v2` (384 dimensiones)
- **Generación**: `flan-t5-small` (77M parámetros)
- **Similitud**: Coseno normalizado

## 📝 Ejemplos de Uso

### Búsqueda Básica
```python
# Pregunta simple
response = qdrant_rag.query("¿Qué es la fotosíntesis?", k=3)
print(response["answer"])
```

### Filtrado por Categoría
```python
# Solo documentos de medicina
filters = {"category": "medicina"}
response = qdrant_rag.query("¿Qué aplicaciones tiene la IA?", k=3, filters=filters)
```

### Filtrado por Fecha
```python
# Solo documentos de 2025
filters = {"date": ("2025-01-01", "2025-12-31")}
response = weaviate_rag.query("¿Cuáles son las tendencias recientes?", k=5, filters=filters)
```

## 📊 Análisis y Conclusiones

El notebook proporciona un análisis detallado que incluye:

### Calidad de Resultados
- Comparación de métricas P@k, R@k y nDCG@k
- Análisis de relevancia de documentos recuperados
- Evaluación de calidad de respuestas generadas

### Rendimiento
- Latencia de búsqueda vectorial
- Tiempo total de procesamiento RAG
- Escalabilidad y eficiencia

### Facilidad de Uso
- Complejidad de configuración
- Flexibilidad de consultas
- Manejo de metadatos

## 🎯 Casos de Uso Recomendados

### Usar Qdrant cuando:
- Se prioriza la velocidad de respuesta
- La configuración debe ser simple
- Los esquemas de datos son relativamente simples
- Se necesita una solución ligera y eficiente

### Usar Weaviate cuando:
- Se requieren esquemas complejos de metadatos
- Se necesitan consultas GraphQL avanzadas
- La flexibilidad en tipos de datos es importante
- Se planea integrar con ecosistemas más amplios

## 📚 Referencias y Recursos

- [Documentación Qdrant](https://qdrant.tech/documentation/)
- [Documentación Weaviate](https://weaviate.io/developers/weaviate)
- [Sentence Transformers](https://www.sbert.net/)
- [FLAN-T5 Paper](https://arxiv.org/abs/2210.11416)
- [Métricas de Evaluación IR](https://en.wikipedia.org/wiki/Evaluation_measures_(information_retrieval))

## 🤝 Contribuciones

Este notebook es una implementación educativa y de investigación. Las mejoras sugeridas incluyen:
- Implementación real de Weaviate (no simulada)
- Más modelos de embeddings para comparar
- Corpus más grande y diverso
- Métricas adicionales de evaluación
- Interfaz web interactiva

## 📄 Licencia

Este proyecto es de código abierto y está disponible bajo la licencia MIT.

---

*Desarrollado para comparar y evaluar sistemas RAG usando diferentes bases de datos vectoriales.*
