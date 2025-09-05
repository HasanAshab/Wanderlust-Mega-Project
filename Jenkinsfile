pipeline {
    agent any

    options {
        buildDiscarder(logRotator(numToKeepStr: '5', artifactNumToKeepStr: '5'))
        disableConcurrentBuilds()
        durabilityHint('PERFORMANCE_OPTIMIZED')
        preserveStashes(buildCount: 5)
    }
    triggers {
        githubPush()
    }
    stages {
        stage('Checkout') {
            steps {
                sh 'touch test.txt'
            }
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
