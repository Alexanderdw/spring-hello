def dockerhub_username = 'depauna'
def img_name = 'spring-hello'
def img_tag = 'latest'
def namespace = 'depauna'

pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        sh """
          docker build . -t ${dockerhub_username}/${img_name}:${img_tag}
        """
      }
    }
    stage('Push') {
      steps {
        withCredentials([[$class: 'UsernamePasswordMultiBinding', credentialsId: 'depauna', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD']]) {
          sh """
            docker login -u ${USERNAME} -p ${PASSWORD}
            docker push ${dockerhub_username}/${img_name}:${img_tag}
            docker logout
          """
        }
      }
    }
  }
}
