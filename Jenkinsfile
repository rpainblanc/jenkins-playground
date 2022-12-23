pipeline {
    agent {
        label 'built-in'
    }
    options {
        timestamps()
    }
    stages {
        stage('init') {
            steps {
                script {
                    sh 'printenv | sort'
                }
            }
        }
    }
}
