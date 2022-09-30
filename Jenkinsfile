pipeline {
    agent any
    stages {
        stage('init') {
            steps {
                script {
                    sh 'git reset --hard && git clean -xfdf'
                    sh 'printenv | sort | tee printenv.txt'
                    archiveArtifacts artifacts: '*.txt', allowEmptyArchive: true
                }
            }
        }
    }
}
