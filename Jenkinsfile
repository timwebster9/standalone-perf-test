pipeline {
    agent {
        node {
            label 'mac'
        }
    }
    stages {
        stage('Cleanup') {
            steps {
                deleteDir()
            }
        }
		stage('Checkout') {
			steps {
				checkout scm
			}
		}
        stage('Gatling Test') {
            steps {
				withEnv(["BASE_URL=http://localhost:8080"]) {
					script {
						def gatling = new com.timw.Gatling(this)
						gatling.execute()
					}
				}
            }
        }
    }
}


