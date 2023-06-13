pipeline {
    agent any
    stages {
        stage('build file') {
            steps {
                checkout scm
                script {
                    withCredentials([usernamePassword(credentialsId: 'GitHub', usernameVariable: 'GitUser', passwordVariable: 'GITHUB_TOKEN')]) {
                        withEnv(["GITHUB_TOKEN=${env.GITHUB_TOKEN}"]) {
                            sh "git config --global --add safe.directory ${env.WORKSPACE}"
                            sh """
                            git branch -a
                            git checkout release
                            git branch --show-current
                            npm init --yes
                            npm install semantic-release @semantic-release/git
                            npx semantic-release
                            """
                        }
                    }
                }
            }
        }
    }
}
