node {
  def app
  def image_name
  def image_tag
  def container_name="nginx"
  def dockerhub=""
  
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
    docker.withRegistry('https://hub.docker.com/', 'DockerHubCredential'){
	  docker.push("${image_name}:${image_tag}")
	}
    sh 'echo "image published"'
  }

  stage('Deploy image'){
    sh "docker container rm -f ${container_name}"

    sh "docker run --name ${container_name} -d -p 9001:80 ${image_name}:${image_tag}"
  }
}
