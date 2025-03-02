pipeline {
  agent any

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
            withCredentials([usernamePassword(credentialsId: 'docker-hub', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
				sh 'echo "$DOCKER_PASS" | docker login -u "$DOCKER_USER" --password-stdin'
			}
            sh 'docker build -t dhwanii08/whong4_hw2_swe_645_survey:$BUILD_NUMBER .'
        }
      }
    }
    
    stage('Push to Docker Hub') {
      steps {
        script {
            sh 'docker push dhwanii08/whong4_hw2_swe_645_survey:$BUILD_NUMBER'
          }
        }
      }
    
    stage('Deploy to Rancher') {
      steps {
        script {
          sh 'kubectl set image deployment/swe-645-assign2-survey-form container-0=dhwanii08/whong4_hw2_swe_645_survey:$BUILD_NUMBER'
        }
      }
    }
  }
}