pipeline {
  agent any

  triggers {
    // Dispara con el webhook de GitHub
    githubPush()
  }

  options {
    skipDefaultCheckout(false) // deja que Jenkins haga el checkout automático
  }

  stages {
    stage('Limpiar Workspace') {
      steps {
        cleanWs()
      }
    }

    stage('Checkout del repo') {
      steps {
        // Jenkins hará checkout del repo configurado en el job
        checkout scm
        sh 'ls -la'
      }
    }

    stage('Ejecutar Comando Simple') {
      steps {
        sh 'echo "¡El pipeline se ejecutó exitosamente!"'
      }
    }
  }

  post {
    always { echo 'Pipeline completado' }
    success { echo 'El pipeline fue exitoso' }
    failure { echo 'El pipeline falló' }
  }
}
