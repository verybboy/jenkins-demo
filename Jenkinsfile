pipeline {
    agent any

    stages {
        stage('Ping CloudFront') {
            steps {
                script {
                    // Ejecutar ping 4 veces y capturar la salida
                    def output = sh(script: 'ping -c 4 d3bs0mnt2u0oni.cloudfront.net', returnStdout: true).trim()
                    echo output

                    // Buscar la línea de resumen (ejemplo: "4 packets transmitted, 4 received, 0% packet loss")
                    def summaryLine = output.readLines().find { it.contains("packet loss") }
                    echo "Resumen: ${summaryLine}"

                    // Comprobar que todos los paquetes se recibieron
                    if (summaryLine && summaryLine.contains("0% packet loss")) {
                        echo "✅ Ping exitoso: todos los paquetes recibidos."
                    } else {
                        error("❌ Ping fallido: pérdida de paquetes detectada.")
                    }
                }
            }
        }
    }

    post {
        success {
            echo "Pipeline completado correctamente."
        }
        failure {
            echo "Pipeline falló: verifica la conectividad con CloudFront."
        }
    }
}
