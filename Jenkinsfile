// Pipeline declarativo
pipeline {
    // Ejecutar el pipeline desde un agente concreto
  agent {
    node {
      label 'principal'
    }
  }
  options {
    //Ficheros de log
    buildDiscarder logRotator(
      daysToKeepStr: '15',
      numToKeepStr: '10'
    )
  }
  
    // Definicion de fases 
    stages {
        stage('Cleanup Worksapce') {
            steps {
               cleanWs()
              echo 'Eliminado Workspace para Job';
            }
        }
        
        stage('Code Checkout') {           
            steps {
              checkout(
                $class: 'GitSCM',
                branches: [[name: '*/main']],
                userRemoteConfigs: [[url: 'https://github.com/spring-projects/spring-petclinic.git']]
              )
            }
        }
        stage('Unit Testing') {
          when {
            branch 'testing'
          }
            steps {
              echo 'Running Unit Tests';
            }
        }
        stage('Code Analysis') {
            steps {
              echo 'Running code Analysis';
            }
        }
        stage('Build Deploy Code') {
          when {
            branch 'developer'
          }
            steps {
              echo 'Build Arifact';
              echo 'Deploying Code';
            }
        }
    }
}
