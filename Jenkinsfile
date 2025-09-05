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
                echo "Commit SHA: ${env.GIT_COMMIT}"
                echo "Branch: ${env.GIT_BRANCH}"
                sh 'mkdir bar'
            }
        }
    }

    post {
        always {
            cleanWs(cleanWhenNotBuilt: false,
                    deleteDirs: true,
                    disableDeferredWipeout: true,
                    notFailBuild: false, //todo
                    patterns: [[pattern: '.gitignore', type: 'INCLUDE'],
                               [pattern: '.propsfile', type: 'EXCLUDE']])
        }
        success { echo '✅ Pipeline succeeded!' }
        failure { echo '❌ Pipeline failed!' }
    }
}
