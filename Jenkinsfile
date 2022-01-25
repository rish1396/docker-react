
pipeline{

	agent any

	environment {
		DOCKERHUB_CREDENTIALS=credentials('df887365-48ed-4ac8-a0dd-49c993009388')
	}

	stages {

		stage('Build') {

			steps {
				sh 'docker build -t rishabh1396/test:latest .'
			}
		}

		stage('Login') {

			steps {
				sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
			}
		}

		stage('Push') {

			steps {
				sh 'docker push rishabh1396/test:latest'
			}
		}
	}

}
