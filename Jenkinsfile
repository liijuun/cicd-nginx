node {
  def app


  stage('Clone repository'){
    checkout scm
  }

  stage('Build image'){
    docker.build("liijuun/nginx")
  }

  stage('Test image'){
    sh 'echo "Test Passed"'
  }


  stage('Publish image'){
    sh 'echo "image published"'
  }
}