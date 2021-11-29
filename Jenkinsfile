pipeline{

	agent any

	environment {
		DOCKERHUB_CREDENTIALS=credentials('docker_connect')

	}

	stages {

		stage('Build') {

			steps {
				sh 'docker build -t kontetsu/frontend:v02 .'
			}
		}

		stage('Login') {

			steps {
				sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u suadakoci --password-976b831c-7951-4289-88e3-fae395de019e'
			}
		}

		stage('Push') {

			steps {
				sh 'docker push kontetsu/frontend:v02'
			}
		}

		stage ('Kubernetis deploy'){
			steps {
					sh ("/usr/local/bin/kubectl -n testenv apply -f frontend.yaml")
				
			}
		}
	}

	post {
		always {
			sh 'docker logout'
		}
	}

}

