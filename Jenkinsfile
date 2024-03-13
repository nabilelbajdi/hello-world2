pipeline {
    agent any
    tools {
        maven 'MAV'
        jdk 'JDK'
    }
    stages {
        stage('Setup') {
            steps {
                script {
                    def buildConfigurations = [
                        [repo: 'https://github.com/user/repo1.git', branch: 'branch1', name: 'repo1-branch1'],
                        [repo: 'https://github.com/user/repo2.git', branch: 'branch2', name: 'repo2-branch2']
                    ]

                    for (config in buildConfigurations) {
                        buildRepoBranch(config.repo, config.branch, config.name)
                    }
                }
            }
        }
    }
}

def buildRepoBranch(String repoUrl, String branch, String stageName) {
    stage("Building ${stageName}") {
        steps {
            checkout([$class: 'GitSCM', branches: [[name: branch]], userRemoteConfigs: [[url: repoUrl]]])
            sh 'mvn clean install'
        }
    }
}
