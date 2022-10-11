def branch_name
def build_kit

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
        booleanParam(name: 'buildKit', defaultValue: true, description: 'If enabled, a kit will be built')
    }
    stages {
        stage('init') {
            steps {
                script {
                    sh 'printenv | sort'
                    sh 'git reset --hard && git clean -xfdf'
                    sh 'ls -al'

                    // Remove non-printable characters from provided parameters (when people get the value from texts with formatting enrichment)
                    branch_name = params.branch.replaceAll(/[^\w-.\/]/, '')
                    build_kit = params.buildKit
                }
            }
        }
        stage('Build kits') {
            when {
                beforeAgent true
                expression {
                    build_kit
                }
            }
            agent {
                docker {
                    image "${DKU_DOCKER_JENKINS_BUILDER_IMAGE}"
                    label 'dku21-low'
                }
            }
            steps {
                script {
                    sh 'printenv | sort'
                    sh 'git reset --hard && git clean -xfdf'
                    sh 'ls -al'
                }
            }
        }
    }
}
