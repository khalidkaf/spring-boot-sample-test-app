pipeline {
  agent any
  stages {
    stage('build') {
      steps {
        echo 'debut de l\'etape build'
        bat 'mvnw -DskipTests clean install'
        echo 'fin de build'
      }
    }

    stage('test') {
      parallel {
        stage('test intégration') {
          steps {
            echo 'debut test integration'
            bat 'mvnw -Dtest=com.exemple.testingweb.integration.** test'
            echo 'fin test integration'
          }
        }

        stage('test fonctionnel') {
          steps {
            echo 'debut test fonctionnel'
            bat 'mvnw -Dtest=com.exemple.testingweb.functional.** test'
            echo 'fin test fonctionnel'
          }
        }

        stage('smoke test') {
          steps {
            echo 'debut smoke test'
            bat 'mvnw -Dtest=com.exemple.testingweb.smoke.** test'
            echo 'fin smoke test'
          }
        }

      }
    }

    stage('deploy') {
      steps {
        echo 'stage deploy'
      }
    }

  }
  tools {
    maven 'maven 3.9'
    jdk 'java 11'
  }
}