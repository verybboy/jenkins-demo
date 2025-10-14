# Jenkins Pipeline: Ping a CloudFront Endpoint

Este proyecto contiene un pipeline de Jenkins que realiza una verificación de conectividad a un endpoint de AWS CloudFront mediante el comando `ping`.

## Descripción del Pipeline

El pipeline está definido en el archivo `Jenkinsfile` y realiza las siguientes acciones:

1. **Agente**: Se ejecuta en cualquier agente disponible (`agent any`).
2. **Stage: Ping CloudFront**:
    - Ejecuta el comando `ping` 4 veces contra el dominio `d3bs0mnt2u0oni.cloudfront.net`.
    - Captura y muestra la salida completa del comando.
    - Busca la línea de resumen que indica la pérdida de paquetes.
    - Verifica que no haya pérdida de paquetes (`0% packet loss`). Si todos los paquetes se reciben correctamente, muestra un mensaje de éxito. Si hay pérdida, marca el pipeline como fallido.
3. **Post Actions**:
    - Si el pipeline finaliza correctamente, muestra un mensaje de éxito.
    - Si falla, muestra un mensaje indicando que se debe verificar la conectividad con CloudFront.

## Uso

1. Clona este repositorio en tu servidor Jenkins.
2. Configura un job de tipo "Pipeline" y apunta al archivo `Jenkinsfile`.
3. Ejecuta el pipeline para verificar la conectividad con el endpoint de CloudFront.

## Requisitos

- Jenkins instalado y configurado.
- El agente debe tener acceso al comando `ping`.
- Acceso de red al dominio de CloudFront especificado.

## Notas

- El pipeline está diseñado para detectar problemas de conectividad de red de forma rápida y automática.
- Si se detecta pérdida de paquetes, el pipeline fallará y mostrará un mensaje de error.

---

**Autor:** verybboy
