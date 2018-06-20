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
        stage('Gatling Test') {
            steps {
				withEnv(["BASE_URL=http://localhost:8080"]) {
					def gatling = new com.timw.Gatling(this)
					gatling.execute()
				}
            }
        }
    }
}


