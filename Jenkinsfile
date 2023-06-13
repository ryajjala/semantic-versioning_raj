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
                            echo "https://${GitUser}:${GITHUB_TOKEN}@github.com"
                            git remote set-url origin "https://${GitUser}:${GITHUB_TOKEN}@github.com"
                            git config --global --add user.email "rajasekhar19489@mgmail.com"
                            git config --global --add user.name "Rajasekhar Yajjala"
                            git config --get remote.origin.url
                            npm init --yes
                            npm install semantic-release @semantic-release/git @semantic-release/changelog @semantic-release/npm conventional-changelog-conventionalcommits
                            npx semantic-release
                            """
                        }
                    }
                }
            }
        }
    }
}
