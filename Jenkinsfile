pipeline {
  agent any

  stages {
    stage('Build') {
      steps {
        sh 'docker build -t french-db -f Dockerfile .'
        sh 'docker tag french-db $DOCKER_FRENCH_DB_IMAGE'
      }
    }
    // stage('Test') {
    //   steps {
    //     sh 'docker run my-flask-app python -m pytest app/tests/'
    //   }
    // }
    stage('Deploy') {
      steps {
        withCredentials([usernamePassword(credentialsId: "${DOCKER_REGISTRY_CREDS}", passwordVariable: 'DOCKER_PASSWORD', usernameVariable: 'DOCKER_USERNAME')]) {
          sh "echo \$DOCKER_PASSWORD | docker login -u \$DOCKER_USERNAME --password-stdin docker.io"
          sh 'docker push $DOCKER_FRENCH_DB_IMAGE'
        }
      }
    }
  }
  post {
    always {
      sh 'docker logout'
    }
  }
}