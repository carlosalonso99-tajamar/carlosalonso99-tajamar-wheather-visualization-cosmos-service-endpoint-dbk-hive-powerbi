# Arquitectura de Integración: Azure Cosmos DB, Databricks y Power BI

Este documento describe la arquitectura de integración entre Azure Cosmos DB, Azure Databricks y Power BI. La implementación se realiza utilizando servicios en Azure para capturar, procesar y visualizar datos de forma eficiente y segura.

## Descripción General de la Arquitectura

La arquitectura consiste en la integración de los siguientes componentes principales:

- **Azure Cosmos DB**: Base de datos NoSQL utilizada para almacenar datos de origen, que en este caso son datos meteorológicos obtenidos a través de la API de OpenWeather.
- **Azure Databricks**: Plataforma de procesamiento de datos que utiliza Apache Spark para realizar transformaciones y procesamiento en los datos almacenados en Cosmos DB.
- **Power BI**: Herramienta de visualización de datos que permite generar informes y dashboards interactivos con los datos procesados en Databricks.
- **Virtual Network (VNet)**: Proporciona una red segura y aislada para los servicios de Azure, asegurando la comunicación privada entre Cosmos DB y Databricks.
- **Service Endpoint**: Conexión directa y segura entre la red virtual y Azure Cosmos DB, eliminando la necesidad de exponer datos a través de Internet.

## Componentes de la Arquitectura

### 1. Azure Cosmos DB (API para MongoDB)
Azure Cosmos DB actúa como la base de datos principal para almacenar datos meteorológicos capturados por un script de Python. Utilizamos la API de MongoDB para facilitar la integración con Azure Databricks.

- **Tipo de Implementación**: Serverless.
- **Propósito**: Almacenar datos de manera escalable y con baja latencia.

### 2. Azure Databricks
Azure Databricks se encarga del procesamiento de datos utilizando Apache Spark. Los datos almacenados en Cosmos DB son transformados y procesados para su posterior visualización.

- **Configuración del Clúster**: Se configura un clúster de nodo único (Single Node) para realizar operaciones locales.
- **Conectores**: Se instala el conector oficial de Spark para MongoDB, permitiendo que Spark lea y escriba datos en Cosmos DB.
- **Metastore de Hive**: Los datos procesados se almacenan en un metastore de Hive, lo cual facilita la consulta desde Power BI.

### 3. Power BI
Power BI se utiliza para la visualización de los datos procesados. Los datos almacenados en el metastore de Hive están disponibles para ser consultados y visualizados mediante dashboards interactivos.

- **Integración con Databricks**: Utiliza **Partner Connect** para conectarse directamente con Azure Databricks y acceder a los datos procesados.

### 4. Virtual Network (VNet)
La VNet proporciona un entorno seguro y aislado para los recursos de Azure. Los recursos, como Azure Databricks y Cosmos DB, se comunican dentro de esta red, garantizando la privacidad del tráfico de datos.

### 5. Service Endpoint
Un Service Endpoint se utiliza para conectar la VNet con Azure Cosmos DB. Esto permite una conexión segura y directa, eliminando la necesidad de una IP pública para el acceso a Cosmos DB.

## Flujo de Datos en la Arquitectura
1. **Captura de Datos**: Un script de Python obtiene datos meteorológicos de la API de OpenWeather y los almacena en Azure Cosmos DB.
2. **Procesamiento de Datos**: Azure Databricks recupera los datos desde Cosmos DB, los procesa y los transforma utilizando Apache Spark.
3. **Almacenamiento de Datos Procesados**: Los datos transformados se registran en el Hive Metastore, lo cual permite su acceso mediante SQL.
4. **Visualización**: Power BI se conecta a Azure Databricks a través de Partner Connect, accede a los datos procesados y genera informes interactivos.

## Ventajas de la Arquitectura
- **Escalabilidad**: Cosmos DB y Databricks permiten manejar grandes volúmenes de datos de forma eficiente y escalable.
- **Seguridad**: La VNet y el Service Endpoint aseguran que la comunicación entre servicios se mantenga privada y segura.
- **Facilidad de Visualización**: Power BI proporciona una forma rápida y eficaz de analizar y presentar los datos transformados.

## Configuración del Clúster en Azure Databricks
En las **Advanced Options** del clúster en Databricks, se configuraron las siguientes opciones para permitir la conexión con Cosmos DB. Por favor, rellena las variables con la información correspondiente:

```plaintext
spark.master              local[*, 4]
spark.databricks.cluster.profile  singleNode
spark.mongodb.output.uri  <output_uri>  # Rellena con la URI de salida para Cosmos DB
spark.mongodb.input.uri   <input_uri>   # Rellena con la URI de entrada para Cosmos DB
pruebadbkcosmosdb?ssl=true&replicaSet=globaldb&retrywrites=false&maxIdleTimeMS=120000&appName=@cosmosaccountcarlos@
```

Estas configuraciones permiten a Spark interactuar directamente con la base de datos Cosmos DB, facilitando la ingesta y transformación de datos.

## Consideraciones Finales
- Asegúrate de tener las credenciales correctas y permisos adecuados configurados en Cosmos DB para evitar problemas de conexión.
- Utiliza **Partner Connect** para simplificar la integración con Power BI y evitar configuraciones manuales adicionales.
- Una vez finalizada la utilización, elimina los recursos para evitar cargos innecesarios en Azure.

Para cualquier duda o consulta adicional, no dudes en contactarme.
