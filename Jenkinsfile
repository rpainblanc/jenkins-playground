// Check use-cases in this order: CHANGE_BRANCH then (BRANCH_NAME || GIT_BRANCH)
if (env.CHANGE_BRANCH && env.CHANGE_ID && env.CHANGE_TARGET) {
    // Jenkins build context: GitHub organization and a PR
    println("Working on branch '${env.CHANGE_BRANCH}', linked to GitHub PR '${env.CHANGE_ID}' which targets branch '${env.CHANGE_TARGET}'")
} else if (env.BRANCH_NAME || env.GIT_BRANCH) {
    // Jenkins build context: GitHub organization and not a PR (e.g. master / release branches)
    // OR
    // Jenkins build context: direct SCM configuration
    def branch_name = getBranchName()
    println("Working on branch '${branch_name}'")
} else {
    println("WARNING Could not determine Jenkins build context, no Sonar analysis would be executed")
}

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
                    if (env.CHANGE_BRANCH) {
                        println("Jenkins build context: GitHub organization and a PR")
                    } else if (env.BRANCH_NAME || env.GIT_BRANCH) {
                        println("Jenkins build context: GitHub organization and not a PR")
                        println("OR")
                        println("Jenkins build context: direct SCM configuration")
                    }
                    sh 'git reset --hard && git clean -xfdf'
                }
            }
        }
    }
}

// Return the name of the branch the job is running on. Depending on how the job is configured
// in Jenkins, this information come from the following environment variables:
//  - CHANGE_BRANCH: if the job is configured with GitHub organization and it's a PR
//  - BRANCH_NAME || GIT_BRANCH:
//    - if the job is configured with GitHub organization and it's a simple branch
//    - or if the branch is set in the SCM configuration of the job
def getBranchName() {
    // Check use-cases in this order: CHANGE_BRANCH then (BRANCH_NAME || GIT_BRANCH)
    String branchName = env.CHANGE_BRANCH
    if (branchName == null) {
        branchName = env.BRANCH_NAME
    }
    if (branchName == null) {
        branchName = env.GIT_BRANCH
    }

    return branchName.replaceAll(/^origin\//, '')
}

