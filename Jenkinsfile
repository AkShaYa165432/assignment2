node {
    def app

    stage('Clone Repository') {
      

        checkout scm
    }

  stage('Build Image') {
       app = docker.build("akshaya23/assignment2")
    }

  stage('Push Image') {
        
        docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
            app.push("${env.BUILD_NUMBER}")
        }
  }

	stage('Deploy')	{
		
			def dockerImage = docker.image('akshaya23/assignment2:'+"${env.BUILD_NUMBER}")
			sh 'docker rm -f app'
			dockerImage.run('-d -p 8081:8080 --name app')	

		}

	}
