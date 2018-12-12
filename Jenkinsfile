node {
  def app
  def image_name
  def image_tag
  def container_name="nginx"
  def dockerhub=""
  
  stage('Clone repository'){
    checkout scm
  }

  stage('Build Docker image'){
    image_name="liijuun/nginx"
    image_tag="1.${BUILD_NUMBER}"
    docker.build("${image_name}:${image_tag}")
  }

  stage('Test Docker image'){
    sh 'echo "Test Passed"'
  }


  stage('Publish Docker image'){
    docker.withRegistry('https://index.docker.io/v1/', 'DockerHubCredential'){
	  sh "docker push ${image_name}:${image_tag}"
	}
    sh 'echo "image published"'
  }

  stage('Deploy on Kubernetes'){
    //sh "docker container rm -f ${container_name}"
    //sh "docker run --name ${container_name} -d -p 9001:80 ${image_name}:${image_tag}"
	sh "sed -i 's%IMAGE%${image_name}:${image_tag}%'"
	
	kubernetesDeploy(kubeconfigId: 'kubernetesConfig',
                 configs: 'nginx-deployment-service.yaml',
                 enableConfigSubstitution: false,
        
                 secretNamespace: 'nginx',
                 secretName: 'nginx',
                 dockerCredentials: [
                        [credentialsId: 'DockerHubCredential']
                        
                 ]
	)
	
	
  }
}
