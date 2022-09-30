pipeline {
    agent any
    environment {
        // Override "author display name" with "author" do not have accented characters
        // Quick fix for https://app.shortcut.com/dataiku/story/98467/integration-tests-prs-k3d-tests-fail-if-environment-variable-contains-accented-characters
        CHANGE_AUTHOR_DISPLAY_NAME = env.CHANGE_AUTHOR
    }
    stages {
        stage('init') {
            steps {
                script {
                    sh 'git reset --hard && git clean -xfdf'
                    sh 'printenv | sort | tee printenv.log'
                    archiveArtifacts artifacts: '*.log', allowEmptyArchive: true
                }
            }
        }
    }
}
