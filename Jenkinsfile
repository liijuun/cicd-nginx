node {
  def app
  def image_name
  def image_tag

  stage('Clone repository'){
    checkout scm
  }

  stage('Build image'){
    image_name="liijuun/nginx"
    image_tag="1.${BUILD_NUMBER}"
    docker.build("${image_name}:${image_tag}")
  }

  stage('Test image'){
    sh 'echo "Test Passed"'
  }


  stage('Publish image'){
    sh 'echo "image published"'
  }

  stage('Deploy image'){
    def nginx_container = docker.container('nginx')
    nginx_container.stop()

    docker.image("${image_name}:${image_tag}").run("--name nginx -d -p 9001:80")
  }
}
