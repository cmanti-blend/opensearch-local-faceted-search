# OpenSearch local + faceted search (Docker Compose)

## Objetivo
Levantar OpenSearch en local con Docker Compose, cargar el dataset de ejemplo y crear un dashboard con filtros (faceted search).

## Instalación y ejecución

### Levantar el entorno
docker compose up -d
docker ps

### Verificación del motor (API REST)
curl -k -u 'admin:Str0ng!Passw0rd_2026' https://localhost:9200

## Dataset cargado
Se utilizó el dataset oficial:
opensearch_dashboards_sample_data_logs (Sample web logs)

## Visualizaciones creadas

1. Logs por país
   - Tipo: Bar chart
   - Campo: geo.src
   - Agregación: Terms

2. Logs en el tiempo
   - Tipo: Line chart
   - Campo: @timestamp
   - Agregación: Date histogram

3. Total de logs
   - Tipo: Metric
   - Agregación: Count

## Dashboard

Se creó un dashboard integrando las tres visualizaciones:
- Logs por país
- Logs en el tiempo
- Total de logs

## Faceted Search

Se implementaron filtros dinámicos utilizando:
- Campo: geo.src
- Ejemplo: geo.src = US

Al aplicar el filtro, todas las visualizaciones se actualizan dinámicamente.

## Evidencias

Las capturas de pantalla se encuentran en la carpeta:

screenshots/
