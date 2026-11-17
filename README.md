
<div align="center">

<h1>ORANETA AI | LEGISLACIÓN FEDERAL MEXICANA</h1>

<h2>Inteligencia artificial aplicada a la consulta de legislación federal en México</h2>

<p><strong>Solución desarrollada por Oraneta AI para Inteligencia Jurídica.</strong></p>

<p>Consulta leyes, códigos, reglamentos y otros ordenamientos jurídicos federales mexicanos mediante inteligencia artificial y lenguaje natural, utilizando información procedente de fuentes oficiales.</p>

<img src="https://img.shields.io/badge/Inteligencia-Artificial-168BFF?style=for-the-badge" alt="Inteligencia Artificial">
<img src="https://img.shields.io/badge/LegalTech-643BFF?style=for-the-badge" alt="LegalTech">
<img src="https://img.shields.io/badge/Legislación-Federal-C329F4?style=for-the-badge" alt="Legislación Federal">

<br><br>

<a href="https://inteligenciajuridica.mx/legislacion-federal/">
<img src="https://img.shields.io/badge/PROBAR_APLICACIÓN_GRATIS-168BFF?style=for-the-badge" alt="Probar aplicación">
</a>

</div>

---

## Acerca del proyecto

**Oraneta AI | Legislación Federal Mexicana** es una solución tecnológica desarrollada por **Oraneta** para **Inteligencia Jurídica**, orientada a facilitar la investigación, localización y consulta de legislación federal mexicana.

La plataforma integra procesos de recopilación de documentos jurídicos oficiales, procesamiento documental, actualización de bases de datos, búsqueda semántica e inteligencia artificial generativa.

Su objetivo es transformar una colección de ordenamientos jurídicos en una base de conocimiento inteligente que permita realizar consultas mediante preguntas formuladas en español.

La aplicación está disponible gratuitamente en:

**https://inteligenciajuridica.mx/legislacion-federal/**

---

## El desafío

La investigación legislativa en México requiere consultar numerosos ordenamientos jurídicos, identificar disposiciones aplicables y revisar sus modificaciones.

Entre los principales desafíos se encuentran:

- Localizar leyes, códigos y reglamentos relevantes para una consulta.
- Identificar disposiciones sin conocer previamente el nombre exacto del ordenamiento.
- Consultar información distribuida entre múltiples documentos oficiales.
- Procesar documentos publicados en diferentes formatos.
- Incorporar nuevos documentos a una base de conocimiento.
- Relacionar disposiciones de distintos ordenamientos para responder preguntas complejas.
- Identificar fechas de publicación y última reforma cuando esta información está disponible.

---

## La solución

Oraneta desarrolló una arquitectura tecnológica que combina ingeniería de datos, automatización documental, bases de datos vectoriales e inteligencia artificial generativa.

### 1. Recopilación de legislación oficial

Un proceso desarrollado en Python consulta el repositorio del **Orden Jurídico Nacional (OJN)**.

El sistema permite:

- Identificar ordenamientos jurídicos disponibles.
- Recuperar información y metadatos de los documentos.
- Localizar las direcciones oficiales de descarga.
- Comparar los documentos encontrados con los registros existentes.
- Descargar documentos nuevos sin repetir archivos previamente incorporados.
- Generar un catálogo estructurado de documentos jurídicos.

La arquitectura de recopilación contempla ordenamientos federales, estatales y municipales, mientras que esta aplicación se especializa en la consulta de legislación federal.

### 2. Normalización y procesamiento documental

Los documentos descargados pasan por un proceso de preparación para facilitar su almacenamiento y consulta.

El sistema:

- Identifica documentos PDF y Microsoft Word.
- Convierte documentos Word a PDF mediante LibreOffice.
- Conserva los documentos originales.
- Extrae el contenido textual de los PDF.
- Organiza el contenido por número de página.
- Relaciona el texto con los metadatos del ordenamiento.
- Genera archivos estructurados para su incorporación a la base de datos.

El procesamiento incorpora mecanismos de seguimiento que permiten continuar operaciones interrumpidas sin repetir documentos completados.

### 3. Actualización de la base de conocimiento

Los registros procesados se incorporan a una base de datos PostgreSQL.

La solución utiliza procedimientos de actualización incremental para identificar información nueva y evitar duplicados.

Entre sus capacidades se encuentran:

- Identificación de registros mediante hashes.
- Detección de documentos previamente procesados.
- Incorporación de nuevos registros.
- Procesamiento por lotes.
- Reconexión ante interrupciones de base de datos.
- Conservación de información jurídica y metadatos.

La base de conocimiento utilizada por el asistente federal se encuentra organizada en la tabla `IJ_Federal`.

### 4. Indexación semántica

Los registros jurídicos se transforman en representaciones vectoriales mediante modelos de embeddings de OpenAI.

La información utilizada para la indexación incluye:

- Ámbito jurídico.
- Título del ordenamiento.
- Tipo de ordenamiento.
- Fecha de publicación.
- Fecha de última reforma.
- Número de página.
- Contenido del documento.

Las representaciones vectoriales se almacenan en PostgreSQL utilizando **pgvector**.

La arquitectura incorpora índices HNSW para facilitar la recuperación de información mediante similitud semántica.

Esto permite identificar disposiciones relacionadas con una pregunta incluso cuando el usuario utiliza palabras diferentes a las presentes en el documento original.

### 5. Motor inteligente de consultas

La aplicación utiliza una arquitectura de inteligencia artificial de dos etapas.

**Planificación de búsqueda**

Un primer modelo de OpenAI interpreta la pregunta del usuario y el contexto de la conversación.

Este modelo determina:

- La consulta semántica que debe ejecutarse.
- Los filtros estructurados que pueden complementar la búsqueda.
- Los campos relevantes para localizar documentos.
- Los criterios de ordenamiento de resultados.

**Recuperación de información**

El sistema consulta PostgreSQL combinando búsqueda semántica y filtros estructurados.

La recuperación permite identificar registros relacionados con la pregunta y seleccionar información relevante para generar la respuesta.

**Generación de respuestas**

Un segundo modelo de OpenAI analiza exclusivamente los registros jurídicos recuperados.

El asistente está diseñado para:

- Responder utilizando información de la base de conocimiento.
- Identificar los ordenamientos que sustentan sus respuestas.
- Referenciar documentos y páginas cuando están disponibles.
- Distinguir disposiciones provenientes de diferentes ordenamientos.
- Considerar fechas de publicación y reforma cuando resulten relevantes.
- Reconocer cuando la información recuperada es insuficiente.
- Evitar incorporar disposiciones jurídicas no sustentadas por las fuentes consultadas.

### 6. Consulta conversacional

La aplicación expone un servicio backend desarrollado con Flask.

El usuario puede formular preguntas en lenguaje natural y realizar consultas de seguimiento.

La solución utiliza Redis para conservar temporalmente el historial conversacional, facilitando la continuidad de las consultas.

---

## Funcionalidades principales

### Búsqueda semántica

Permite localizar disposiciones jurídicas relacionadas con una pregunta, aunque no se utilicen exactamente las palabras contenidas en la legislación.

### Búsqueda estructurada

Permite complementar las consultas mediante campos disponibles en los registros, como:

- Título del ordenamiento.
- Tipo de ordenamiento.
- Ámbito jurídico.
- Fecha de publicación.
- Fecha de última reforma.
- Número de página.

### Búsqueda híbrida

Combina recuperación semántica con filtros estructurados para identificar registros jurídicos relevantes.

### Respuestas fundamentadas

El asistente está diseñado para generar respuestas basadas en documentos recuperados de la base de conocimiento.

Cuando la información está disponible, identifica el ordenamiento y las referencias documentales utilizadas.

### Actualización incremental

Los procesos de recopilación e incorporación identifican documentos nuevos y utilizan mecanismos para evitar registros duplicados.

### Historial conversacional

Permite realizar preguntas de seguimiento utilizando temporalmente el contexto de consultas anteriores.

### Procesamiento automatizado

La solución integra procesos de descarga, conversión, extracción de texto, generación de embeddings y almacenamiento estructurado.

---

## Arquitectura tecnológica

El funcionamiento general de la solución puede representarse mediante el siguiente flujo:

**Orden Jurídico Nacional**

↓

**Recopilación automatizada con Python**

↓

**Conversión y procesamiento de documentos PDF**

↓

**Extracción de contenido y metadatos**

↓

**PostgreSQL + pgvector + OpenAI Embeddings**

↓

**Motor de recuperación híbrida**

↓

**Modelos de inteligencia artificial generativa**

↓

**Asistente conversacional de Legislación Federal**

La arquitectura separa los procesos de recopilación y actualización documental del servicio que atiende las consultas de los usuarios.

---

## Tecnologías utilizadas

| Tecnología | Aplicación |
|---|---|
| Python | Automatización, procesamiento documental y servicios backend |
| Requests | Consulta y descarga de documentos oficiales |
| Beautiful Soup | Extracción de información de páginas HTML |
| LibreOffice | Conversión de documentos Word a PDF |
| pypdf | Extracción de texto de documentos PDF |
| PostgreSQL | Almacenamiento estructurado de información jurídica |
| pgvector | Indexación y búsqueda vectorial |
| HNSW | Optimización de búsquedas por similitud |
| OpenAI API | Embeddings, planificación de búsquedas y generación de respuestas |
| Flask | Servicio backend de consultas |
| Redis | Gestión temporal del historial conversacional |
| Orden Jurídico Nacional | Fuente oficial de documentos jurídicos |

---

## Prueba la aplicación

La plataforma se encuentra disponible públicamente y puede utilizarse gratuitamente sin acceder al código fuente ni instalar dependencias.

<div align="center">

<a href="https://inteligenciajuridica.mx/legislacion-federal/">
<img src="https://img.shields.io/badge/ABRIR_DEMOSTRACIÓN_GRATUITA-168BFF?style=for-the-badge" alt="Abrir demostración gratuita">
</a>

</div>

### Ejemplos de consultas

**Consulta laboral**

> ¿Qué establece la Ley Federal del Trabajo sobre las vacaciones de los trabajadores?

**Consulta mercantil**

> ¿Cuáles son los requisitos legales para constituir una sociedad anónima en México?

**Consulta de protección de datos**

> ¿Qué obligaciones establece la legislación federal sobre el tratamiento de datos personales?

**Consulta fiscal**

> ¿Qué disposiciones del Código Fiscal de la Federación regulan las facultades de comprobación de las autoridades fiscales?

**Consulta de seguimiento**

> ¿Qué artículos de las leyes mencionadas sustentan tu respuesta anterior?

Las respuestas dependen de los documentos incorporados a la base de conocimiento y de la información recuperada en cada consulta.

La disponibilidad de documentos oficiales no garantiza por sí misma que todas las disposiciones estén actualizadas a su última reforma.

---

## Aplicación desarrollada por Oraneta para Inteligencia Jurídica

**Inteligencia Jurídica** es una plataforma mexicana especializada en información y conocimiento legal.

**Oraneta** desarrolló e implementó esta solución de inteligencia artificial para ampliar las capacidades de consulta jurídica de Inteligencia Jurídica.

El proyecto permite ofrecer a los usuarios una experiencia de investigación legislativa mediante lenguaje natural, utilizando una base de conocimiento construida a partir de documentos procedentes de fuentes oficiales.

Esta implementación representa un caso de aplicación real de inteligencia artificial generativa, automatización de procesos e ingeniería de datos en el sector LegalTech.

**Desarrollador:** [Oraneta](https://oraneta.com)

**Plataforma:** [Inteligencia Jurídica](https://inteligenciajuridica.mx)

**Aplicación:** [Consulta de Legislación Federal](https://inteligenciajuridica.mx/legislacion-federal/)

---

## Sobre Oraneta

**Oraneta** desarrolla soluciones empresariales de inteligencia artificial, automatización de procesos y asistentes digitales especializados.

Sus soluciones combinan modelos de inteligencia artificial, integración de sistemas y conocimiento especializado para automatizar operaciones, facilitar el acceso a información y mejorar la interacción entre organizaciones y usuarios.

**Oraneta AI | Legislación Federal Mexicana** demuestra la aplicación práctica de:

- Inteligencia artificial generativa.
- Arquitecturas de recuperación aumentada de información (RAG).
- Ingeniería y automatización de datos.
- Procesamiento de documentos.
- Bases de datos vectoriales.
- Búsqueda semántica e híbrida.
- Integración de modelos de lenguaje.
- Desarrollo de asistentes conversacionales especializados.

El proyecto fue desarrollado por Oraneta para Inteligencia Jurídica como una solución tecnológica aplicada a necesidades reales de consulta legislativa.

---

## Documentación y propiedad intelectual

Este repositorio tiene fines exclusivamente informativos, demostrativos y de portafolio profesional.

**El código fuente de la aplicación no se distribuye públicamente.**

Los componentes internos, las credenciales, las configuraciones de infraestructura, los procesos operativos y las implementaciones propietarias permanecen bajo control de sus respectivos titulares.

La documentación presenta las funcionalidades, tecnologías y arquitectura general de una solución desarrollada por Oraneta para Inteligencia Jurídica.

Los documentos jurídicos utilizados por la plataforma proceden de fuentes oficiales.

**Oraneta e Inteligencia Jurídica son entidades independientes y no representan ni forman parte del Orden Jurídico Nacional ni de las autoridades gubernamentales responsables de la publicación de la legislación mexicana.**

---

<div align="center">

<h2>Conoce Oraneta e Inteligencia Jurídica</h2>

<a href="https://oraneta.com">
<img src="https://img.shields.io/badge/Oraneta-168BFF?style=for-the-badge" alt="Oraneta">
</a>

<a href="https://inteligenciajuridica.mx">
<img src="https://img.shields.io/badge/Inteligencia_Jurídica-643BFF?style=for-the-badge" alt="Inteligencia Jurídica">
</a>

<a href="https://www.linkedin.com/company/oraneta/">
<img src="https://img.shields.io/badge/LinkedIn-C329F4?style=for-the-badge" alt="LinkedIn">
</a>

<br><br>

<p><strong>Oraneta AI — Inteligencia artificial aplicada a soluciones reales.</strong></p>

<p>Proyecto desarrollado por Oraneta para Inteligencia Jurídica.</p>

</div>
