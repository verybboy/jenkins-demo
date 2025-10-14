pipeline {
  agent any
  stages {
    stage('Saludo') {
      steps {
        echo '¡Hola desde un pipeline declarativo!'
      }
    }
    stage('Fecha') {
      steps {
        sh 'date'
      }
    }
  }
}