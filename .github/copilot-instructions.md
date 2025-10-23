## Instrucciones rápidas para agentes de código (proyecto SaludDigitalB_E1)

Propósito: ayudar a un agente IA a ser productivo inmediatamente en este repositorio Python/Notebooks orientado a generación y procesamiento de datos de pacientes.

- Raíz y entorno
  - Proyecto en: raíz del workspace. Entorno Python activo recomendado: `myenv` (ruta: `myenv/Scripts/python.exe`).
  - Notebooks principales están en `scripts/` (ej: `3_Generar_Data_Turismo.ipynb`, `4_Proceso_ETL.ipynb`, `5_Loading_MongoDB.ipynb`).

- Flujo de trabajo principal
  1. Los notebooks generan y limpian datos en `data/` y `database/` (ej: `data/pacientes.csv` y `database/pacientes_clean.csv`).
  2. ETL y carga a Mongo se hacen desde los notebooks `4_Proceso_ETL.ipynb` y `5_Loading_MongoDB.ipynb`.
  3. Reportes están en `reports/` y se generan desde `6_Reportes.ipynb`.

- Cómo ejecutar localmente (detectable y reproducible)
  - Activar el virtualenv (PowerShell):
    - `.\myenv\Scripts\Activate.ps1` (o usar la UI de VS Code para seleccionar el intérprete `myenv`).
  - Ejecutar un notebook desde VS Code o ejecutar fragmentos de Python con el intérprete del workspace.
  - Ejemplo concreto: la celda de `scripts/3_Generar_Data_Turismo.ipynb` crea `data/pacientes.csv`. Ejecutar esa celda o correr un script que importe pathlib/csv como en el notebook.

- Convenciones del repo y patrones frecuentes
  - Uso intensivo de Jupyter Notebooks para procesos: cada paso del pipeline (generación, limpieza, carga, reportes) está separado en un notebook. Cambios persistentes a la lógica deben extraerse a scripts Python si se requiere integración continua.
  - Rutas relativas: los notebooks usan rutas relativas desde la raíz del proyecto (p. ej. `Path('data')`).
  - Formato CSV: columnas estándar: `Paciente_ID, Nombre, Apellido, Edad, Sexo, Diagnostico, Distrito, Fecha_Ingreso` (ver `3_Generar_Data_Turismo.ipynb`).

- Dependencias y ejecución reproducible
  - No hay `requirements.txt` visible; confiar en el `myenv` provisto. Antes de ejecutar notebooks en otro entorno, instalar paquetes típicos: `pandas`, `pymongo` (si se usa Mongo), `matplotlib`/`seaborn` para reportes.

- Integraciones y puntos de atención
  - MongoDB: hay un notebook llamado `5_Loading_MongoDB.ipynb` — buscar allí cadenas de conexión y uso de `pymongo.MongoClient`. No modifiques credenciales si aparecen; en su lugar, usar variables de entorno.
  - Jenkins/CI: la carpeta `ci/` contiene imágenes de jobs; no hay pipeline declarativo en el repo. Tenga cuidado al asumir pasos de CI.

- Ejemplos útiles para ediciones automáticas
  - Si el agente automatiza generación de datos, reproduzca el patrón de `scripts/3_Generar_Data_Turismo.ipynb`: crear `data/`, escribir CSV con `csv.writer` y usar `Path` para construir rutas.
  - Para integrar validaciones, añadir una pequeña función utilitaria (p. ej. `scripts/utils/io.py`) y referenciarla desde notebooks.

- Errores comunes detectados en notebooks
  - Celdas con comillas o comas mal escapadas al copiar/pegar; validar con un lint de Python o ejecutar la celda (sintaxis en el repo está bien para `3_Generar_Data_Turismo.ipynb`).
  - Ausencia de `requirements.txt`; documentar dependencias cuando añadas nuevos paquetes.

- Qué NO cambiar automáticamente
  - No subir credenciales ni cadenas de conexión en texto plano. Preferir variables de entorno o archivos `.env` excluidos por git.

Si algo de esto está incompleto o quieres que agregue ejemplos concretos (scripts, requirements, o un pequeño utilitario), indícame qué prefieres y lo agrego.
