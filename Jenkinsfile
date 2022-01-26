
pipeline{

	agent any

	environment {
		DOCKERHUB_CREDENTIALS = credentials('df887365-48ed-4ac8-a0dd-49c993009388')
		AWS_ACCESS_KEY_ID     = credentials('jenkins-aws-access-key-id')
    AWS_SECRET_ACCESS_KEY = credentials('jenkins-aws-access-key')

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

		//stage('Push') {
			//steps {
				//sh 'docker push rishabh1396/test:latest'
		//	}
	//	}

		stage('Production') {
		  steps {
		    withAWS(region:'ap-south-1',credentials:'jenkins-aws-cred') {
		    s3Delete(bucket: 'elasticbeanstalk-ap-south-1-116002743124', path:'**/*')
		    s3Upload(bucket: 'elasticbeanstalk-ap-south-1-116002743124', includePathPattern:'**/*');
		  	}
		  }
    }

	}
}
