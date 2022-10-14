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
                    sh 'git reset --hard && git clean -xfdf'
                    sh 'ls -al'
                    println("feature branch")
                }
            }
        }
    }
}
