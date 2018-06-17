node {
    def app
	stage('Build Docker Image') {
	    checkout scm
		app = docker.build('subhashe/sample-app:latest')
	}

    stage('Publish to Docker Hub'){
		docker.withRegistry("https://hub.docker.com/", "dockerhub")	{
		    app.push('latest')
			}
	}
    stage('Deploy to Production'){
		docker.withServer('tcp://production:2376', 'production'){
			sh 'docker run -d subhashe/sample-app'
		}
	}
}
