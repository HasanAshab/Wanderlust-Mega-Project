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
            }
        }
        stage('Detect Changes') {
            steps {
                script {
                    // Get changed files vs previous commit
                    def changedFiles = sh(
                        script: "git diff --name-only HEAD~1 HEAD",
                        returnStdout: true
                    ).trim().split("\n")

                    echo "Changed files: ${changedFiles}"

                    // Set flags
                    env.BUILD_BACKEND = changedFiles.any { it.startsWith('backend/') }.toString()
                    env.BUILD_FRONTEND = changedFiles.any { it.startsWith('frontend/') }.toString()

                    echo "Build Backend? ${env.BUILD_BACKEND}"
                    echo "Build Frontend? ${env.BUILD_FRONTEND}"
                }
            }
        }
    }

    post {
        always {
            cleanWs()
        }
        success { echo '✅ Pipeline succeeded!' }
        failure { echo '❌ Pipeline failed!' }
    }
}
