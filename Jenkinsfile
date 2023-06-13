pipeline {
    agent {
        label 'ceeams-agent'
    }
    stages {
        stage('build file') {
            steps {
                container('node') {
                    checkout scm
                    script {
                        withCredentials([usernamePassword(credentialsId: 'GitHub', usernameVariable: 'GitUser', passwordVariable: 'GITHUB_TOKEN')]) {
                            withEnv(["GITHUB_TOKEN=${env.GITHUB_TOKEN}"]) {
                                sh 'git config --global --add safe.directory /home/jenkins/agent/workspace/versioning_test'
                                sh """
                                echo "https://${CMS_GH_UN}:${GITHUB_TOKEN}@github.cms.gov"
                                #git config --global --add safe.directory /home/jenkins/agent/workspace/versioning_test
                                git remote set-url origin "https://${CMS_GH_UN}:${GITHUB_TOKEN}@github.cms.gov"
                                git config --global --add user.email "vignesh@alcortechsolutions.com"
                                git config --global --add user.name "Vignesh Gowni"
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
}
