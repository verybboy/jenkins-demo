# Jenkins Pipeline: Comprobación de APIs con curl

Este pipeline de Jenkins permite comprobar la disponibilidad y latencia de múltiples endpoints de API usando `curl`, de forma automatizada y parametrizable.

## Descripción General

El pipeline está definido en el archivo `Jenkinsfile` y realiza las siguientes acciones:

1. **Parámetros configurables:**
   - `ENDPOINTS_FILE`: Ruta al archivo con las URLs de las APIs (una por línea).
   - `TIMEOUT_SECONDS`: Tiempo máximo de espera para cada petición.
   - `LATENCY_FAIL_MS`: Umbral de latencia en milisegundos para considerar una API como fallida.
   - `EXPECTED_CODES`: Códigos HTTP válidos (separados por coma).
   - `HEADERS`: Cabeceras HTTP personalizadas (key=value por línea).

2. **Stages principales:**
   - **Checkout:** Descarga el código fuente del repositorio.
   - **Comprobar APIs con curl:**
     - Lee el archivo de endpoints y filtra URLs válidas.
     - Genera un archivo de cabeceras para `curl` si se especifican.
     - Para cada URL:
       - Realiza una petición HTTP (por defecto OPTIONS, configurable).
       - Verifica si el código de respuesta está entre los esperados.
       - Mide la latencia y la compara con el umbral definido.
       - Registra el resultado en un log.
     - Si alguna API falla por código inesperado o latencia alta, el pipeline termina con error.
     - Archiva los logs y archivos generados en la carpeta `artifacts`.

3. **Post Actions:**
   - Siempre archiva los artefactos generados.
   - Muestra mensajes de éxito o fallo según el resultado de las comprobaciones.

## Uso

1. Prepara un archivo de endpoints (por defecto `apis-control/api_endpoints.txt`) con una URL por línea.
2. (Opcional) Define cabeceras HTTP en el parámetro `HEADERS` si tus APIs requieren autenticación o configuración especial.
3. Configura un job de tipo "Pipeline" en Jenkins y apunta al archivo `Jenkinsfile`.
4. Ejecuta el pipeline y revisa los resultados en los artefactos generados.

## Requisitos

- Jenkins instalado y configurado.
- El agente debe tener acceso a `curl` y a los endpoints definidos.
- Acceso de red a las APIs que se van a comprobar.

## Notas

- El pipeline es flexible y permite ajustar parámetros para adaptarse a diferentes APIs y criterios de validación.
- Los resultados detallados se guardan en `artifacts/api_checks.log`.
- Si alguna API supera el umbral de latencia o responde con un código no esperado, el pipeline fallará y mostrará un mensaje de error.

---

**Autor:** verybboy
