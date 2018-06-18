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
			sh 'docker --tlsverify run --dns 192.168.1.120 --dns-search sunnybank.containeryard.com. -d subhashe/sample-app'
		}
	}
}
