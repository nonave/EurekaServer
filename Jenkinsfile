pipeline {
  agent any
  stages {
    stage('Build') {
      agent any
      steps {
        echo 'Build......'
        sh 'mvn clean -DskipTests=true'
        sh 'mvn install -DskipTests=true'
      }
    }

    stage('Test') {
      agent any
      environment {
        registry = 'davidperez01/EurekaServer'
        registryCredential = 'dockerhub'
      }
      steps {
        echo 'Test'
        sh 'mvn test'
      }
    }

    stage('Docker Build') {
      steps {
        git(url: 'https://github.com/davidperezmillan/EurekaServer.git', branch: 'main')
        echo 'Docker build images'
        sh 'docker image build -t nonave/eureka .'
      }
    }

    stage('Docker Register') {
      steps {
        echo 'Register Docker'
      }
    }

  }
}