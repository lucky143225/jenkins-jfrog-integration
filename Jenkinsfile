pipeline {
    agent any

    tools {
        maven "mvn"
    }

    stages {
        stage('Git Pull') {
            steps {
                git credentialsId: 'github', url: 'git@github.com:lucky143225/jenkins-jfrog-integration.git'
            }
        }

        stage('Build') {
            steps {
                sh "mvn clean install"
            }
        }

        stage('JFrog Upload') {
            steps {
                script {
                    def server = Artifactory.server 'jfrog'
                    def uploadSpec = '''{
                        "files": [
                            {
                                "pattern": "target/*.jar",
                                "target": "demo-maven-project"
                            }
                        ]
                    }'''
                    server.upload(uploadSpec)
                }
            }
        }
    }
}
