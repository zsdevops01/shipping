pipeline {
  agent {
    label 'NODEJS'
  }

  stages {

    stage('Compile Code') {
      steps {
        sh '''
          mvn compile
        '''
      }
    }

    stage('Make Package') {
      steps {
        sh '''
          mvn package
        '''
      }
    }

    stage('Prepare Artifacts') {
      steps {
        sh '''
          cp target/*.jar shipping.jar 
          zip -r shipping.zip shipping.jar
        '''
      }
    }

    stage('Upload Artifacts') {
      steps {
        sh '''
          curl -f -v -u admin:admin123 --upload-file shipping.zip http://172.31.14.124:8081/repository/shipping/shipping.zip
        '''
      }
    }

  }

}