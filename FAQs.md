# Preguntas Frecuentes

### 1. ¿Por qué Hive?
Hive es una herramienta clave en esta arquitectura, y estas son algunas razones para elegirla:

- **Metastore centralizado**:
  - Hive Metastore actúa como un catálogo central donde se almacena la información de las tablas (esquemas, ubicaciones de datos, particiones, etc.).
  - Esto permite que varias herramientas (como Databricks y Power BI) puedan acceder a los datos sin preocuparse por las complejidades del almacenamiento.

- **Interoperabilidad con otras herramientas**:
  - Hive es compatible con sistemas distribuidos como Spark (Databricks) y herramientas de visualización como Power BI.
  - Permite que las consultas SQL estándar funcionen sobre grandes volúmenes de datos distribuidos.

- **Escalabilidad y manejo de grandes volúmenes**:
  - Diseñado para manejar datos a gran escala en entornos distribuidos.
  - Hive permite estructurar datos no estructurados o semi-estructurados, convirtiéndolos en tablas accesibles.

- **Facilidad de uso para consultas SQL**:
  - Hive hace que los datos almacenados en formatos como Parquet, ORC o Avro sean consultables mediante SQL, lo cual reduce la curva de aprendizaje para analistas y científicos de datos.

**Respuesta sugerida**: "Hive se utiliza como metastore para proporcionar un catálogo centralizado y estructurado de los datos, facilitando la interoperabilidad entre herramientas como Databricks y Power BI, además de permitir consultas SQL sobre grandes volúmenes de datos de manera escalable."

### 2. ¿Qué es el Service Endpoint?
Un Service Endpoint es una funcionalidad en Azure que conecta recursos dentro de una red virtual con servicios de Azure sin necesidad de exponerlos a Internet. Aquí están los puntos clave:

- **Conexión directa y segura**:
  - Permite a los recursos en la red virtual acceder a servicios de Azure (como Azure Cosmos DB en este caso) directamente, sin necesidad de direcciones IP públicas ni tráfico en Internet.
  - Mejora la seguridad al restringir el acceso únicamente a la VNet.

- **Control de acceso granular**:
  - Puedes configurar políticas en la red virtual para permitir o denegar acceso a servicios específicos.
  - Esto asegura que solo los recursos dentro de la red virtual puedan interactuar con el servicio.

- **Mejor rendimiento**:
  - Al utilizar Service Endpoints, el tráfico entre la red virtual y el servicio de Azure fluye dentro de la red backbone de Azure, reduciendo latencias.

**Respuesta sugerida**: "El Service Endpoint asegura una conexión directa, segura y de alto rendimiento entre la red virtual y Azure Cosmos DB, eliminando la necesidad de exponer datos a través de Internet y mejorando el control de acceso."

### 3. ¿Por qué Virtual Network?
La Virtual Network (VNet) es una pieza fundamental de la arquitectura para la conectividad y seguridad. Sus principales razones de uso son:

- **Aislamiento y seguridad**:
  - La VNet crea un entorno aislado donde los recursos de Azure pueden comunicarse de manera privada.
  - Esto evita la exposición de los datos a Internet y asegura que el tráfico entre los servicios sea interno y protegido.

- **Control de acceso**:
  - Puedes establecer reglas de firewall, subredes y configuraciones específicas para permitir solo el tráfico necesario entre los recursos.

- **Integración de servicios**:
  - La VNet permite que servicios como Databricks, Hive Metastore y Cosmos DB interactúen de forma directa y privada.
  - Además, facilita la integración con herramientas externas como Power BI mediante subredes públicas.

- **Escalabilidad**:
  - Proporciona una base escalable para añadir más servicios o recursos en el futuro sin comprometer la seguridad.

**Respuesta sugerida**: "La Virtual Network asegura que los recursos de la arquitectura estén aislados y puedan comunicarse de manera privada. Proporciona control de acceso granular, aumenta la seguridad de los datos y facilita la integración de servicios dentro de un entorno escalable."

