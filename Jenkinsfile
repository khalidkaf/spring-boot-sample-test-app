pipeline {
  agent any
  stages {
    stage('build') {
      steps {
        echo 'debut de l\'etape build'
        bat 'mvnw -DskipTests clean install'
        echo 'fin de build'
        archiveArtifacts '**/target/*.jar'
      }
    }

    stage('test') {
      parallel {
        stage('test intégration') {
          steps {
            echo 'debut test integration'
            bat 'mvnw -Dtest=com.example.testingweb.integration.** test'
            echo 'fin test integration'
          }
        }

        stage('test fonctionnel') {
          steps {
            echo 'debut test fonctionnel'
            bat 'mvnw -Dtest=com.example.testingweb.functional.** test'
            echo 'fin test fonctionnel'
          }
        }

        stage('smoke test') {
          steps {
            echo 'debut smoke test'
            bat 'mvnw -Dtest=com.example.testingweb.smoke.** test'
            echo 'fin smoke test'
          }
        }

      }
    }

    stage('deploy') {
      steps {
        echo 'stage deploy'
        bat 'java -jar ./target/testing-web-complete.jar'
      }
    }

  }
  tools {
    maven 'maven 3.9'
    jdk 'java 11'
  }
}