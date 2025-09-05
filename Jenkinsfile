pipeline {
    agent any

    options {
        buildDiscarder(logRotator(numToKeepStr: '10', artifactNumToKeepStr: '5'))
        disableConcurrentBuilds()
        durabilityHint('PERFORMANCE_OPTIMIZED')
        preserveStashes(buildCount: 5)
        // skipDefaultCheckout()
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

    post {
        success { echo '✅ Pipeline succeeded!' }
        failure { echo '❌ Pipeline failed!' }
        // always { 
        //     cleanWs()
        // }
    }
}
