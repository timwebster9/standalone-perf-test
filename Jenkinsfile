import com.timw.Gatling

node('mac') {
	stage('Cleanup') {
		deleteDir()
	}
	stage('Checkout') {
		checkout scm
	}
	stage('Gatling Test') {
		withEnv(["BASE_URL=http://localhost:8080"]) {
			def gatling = new Gatling(this)
			gatling.execute()
		}
	}
	stage('Publish Reports') {

		// you only need to customise this Map
		def params = [environment: 'dev',
		              product: 'some-webapp',
		              component: 'backend']

		// Publish to Azure Blob Storage
		azureBlobUpload('container-key', Gatling.GATLING_REPORTS_DIR, "performance/${params.product}-${params.component}/${params.environment}")

		// Publish to Azure CosmosDB
	    def reportsPath = "${WORKSPACE}/" + Gatling.GATLING_REPORTS_PATH
	    publishToCosmosDb(this, params, Gatling.COSMOSDB_COLLECTION, reportsPath, '**/*.json')
	}
}


