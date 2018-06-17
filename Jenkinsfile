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
		docker.withServer('tcp://production:2376', 'production'){
			sh 'docker --tlsverify run --add-host production:192.168.1.121 -d subhashe/sample-app'
		}
	}
}
