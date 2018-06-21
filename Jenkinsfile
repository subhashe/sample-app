node {
    def app
	stage('Build Docker Image') {
	    checkout scm
		app = docker.build('subhashe/sample-app:latest')
	}

    stage('Publish to Docker Hub'){
		docker.withRegistry("", "dockerhub")	{
		    app.push('latest')
			}
	}
    stage('Deploy to Production'){
	     sh '/bin/bash && export DOCKER_HOME=tcp://production:2376 && docker --tlsverify run  -d subhashe/sample-app'
             }
	}
}
