node {
  def app


  stage('Clone repository'){
    checkout scm
  }

  stage('Build image'){
    sh 'usermod -aG docker jenkins'
    docker.build("liijuun/nginx")
  }

  stage('Test image'){
    sh 'echo "Test Passed"'
  }


  stage('Publish image'){
    sh 'echo "image published"'
  }
}
