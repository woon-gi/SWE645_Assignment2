pipeline {
  agent any
  environment {
	DOCKERHUB_PASSWORD = credentials('Hubdoc645')
  }

  stages {
    stage('Checkout GitHub Repository') {
      steps {
        checkout scm
      }
    }
    
    stage('Build Docker Image') {
      steps {
        script {
            sh 'rm -rf *.war'
            sh 'jar -cvf SWE645_Assignment2.war -C src/ .'
            sh 'echo $BUILD_NUMBER'
            sh 'sudo docker login -u dhwanii08 -p ${DOCKERHUB_PASSWORD}'
            sh 'sudo docker build -t dhwanii08/whong4_hw2_swe_645_survey:$BUILD_NUMBER .'
        }
      }
    }
    
    stage('Push to Docker Hub') {
      steps {
        script {
            sh 'sudo docker push dhwanii08/whong4_hw2_swe_645_survey:$BUILD_NUMBER'
          }
        }
      }
    
    stage('Deploy to Rancher') {
      steps {
        script {
          sh 'kubectl set image deployment/swe645deployment container-0=dhwanii08/whong4_hw2_swe_645_survey:$BUILD_NUMBER'
        }
      }
    }
  }
}