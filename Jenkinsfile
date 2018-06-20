node('mac') {
	stage('Cleanup') {
		deleteDir()
	}
	stage('Checkout') {
		checkout scm
	}
	stage('Gatling Test') {
		withEnv(["BASE_URL=http://localhost:8080"]) {
			def gatling = new com.timw.Gatling(this)
			gatling.execute()
		}
	}
}


