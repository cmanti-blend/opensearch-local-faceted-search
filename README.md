OpenSearch local + Faceted Search (Docker Compose)
Objetivo

Levantar un entorno local de OpenSearch utilizando Docker Compose, cargar un dataset de ejemplo y construir un dashboard interactivo con búsqueda facetada (Faceted Search).

1️⃣ Instalación y ejecución
Levantar el entorno
docker compose up -d
docker ps


Se levantan:

2 nodos de OpenSearch

1 instancia de OpenSearch Dashboards

Verificación del motor (API REST)
curl -k -u 'admin:Str0ng!Passw0rd_2026' https://localhost:9200


Esto valida que el cluster esté activo y respondiendo correctamente.

2️⃣ Dataset cargado

Se utilizó el dataset oficial de OpenSearch:

opensearch_dashboards_sample_data_logs

Este dataset contiene logs simulados de tráfico web.

3️⃣ Visualizaciones creadas

Se construyeron las siguientes visualizaciones:

1. Logs por país

Tipo: Vertical Bar Chart

Campo: geo.src

Agregación: Terms

Métrica: Count

Propósito: Mostrar el conteo de logs agrupados por país de origen.

2. Logs en el tiempo

Tipo: Line Chart

Campo: timestamp

Agregación: Date Histogram

Métrica: Count

Propósito: Visualizar la evolución de los logs en el tiempo.

3. Total de logs

Tipo: Metric

Agregación: Count

Propósito: Mostrar el total de documentos del índice seleccionado.

4️⃣ Dashboard

Se creó un dashboard integrando las tres visualizaciones:

Logs por país

Logs en el tiempo

Total de logs

El dashboard permite analizar los datos de forma consolidada e interactiva.

5️⃣ Faceted Search

Se implementaron filtros dinámicos utilizando el campo:

geo.src

Ejemplo de filtro aplicado:

geo.src = CN


Al aplicar el filtro:

La métrica total cambia automáticamente

La gráfica por país se actualiza

La gráfica temporal se ajusta al subconjunto filtrado

Esto demuestra el funcionamiento de búsqueda facetada, donde múltiples visualizaciones reaccionan al mismo filtro dinámico.

6️⃣ Validación vía API REST

Se realizaron consultas directamente contra OpenSearch:

Conteo de documentos
curl -k -u 'admin:Str0ng!Passw0rd_2026' https://localhost:9200/opensearch_dashboards_sample_data_logs/_count

Obtener un documento
curl -k -u 'admin:Str0ng!Passw0rd_2026' https://localhost:9200/opensearch_dashboards_sample_data_logs/_search?size=1


Estas consultas permiten validar el motor sin depender de la interfaz gráfica.

📸 Evidencias (Screenshots)

Las capturas se encuentran en la carpeta:

screenshots/

01_docker_compose_running_containers.png

Contenedores ejecutándose correctamente.

02_opensearch_api_cluster_validation.png

Validación del cluster vía API REST.

03_opensearch_index_document_count.png

Conteo total de documentos del índice.

04_opensearch_single_document_search.png

Retorno de un documento en formato JSON.

05_dashboard_overview.png

Dashboard general con las tres visualizaciones.

06_dashboard_faceted_filter_CN.png

Dashboard con filtro aplicado (Faceted Search).
