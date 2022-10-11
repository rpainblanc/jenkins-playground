def branch_name

pipeline {
    agent {
        label 'built-in'
    }
    options {
        timestamps()
    }
    parameters {
        string(defaultValue: 'main',
                description: 'The Git branch name to build (or the commit hash)',
                name: 'branch')
    }
    stages {
        stage('init') {
            steps {
                script {
                    sh 'printenv | sort'
                    sh 'git reset --hard && git clean -xfdf'

                    // Remove non-printable characters from provided parameters (when people get the value from texts with formatting enrichment)
                    branch_name = params.branch.replaceAll(/[^\w-.\/]/, '')
                }
            }
        }
    }
}
