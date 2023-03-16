pipeline {
    agent none
    
    tools { go 'go 1.19' }
    
    stages {
        stage('Build') {
            agent {
                label {
                    label 'nodeworker'
                    customWorkspace '/home/nodeworker/go-webapp-sample'
                }
            }
            steps {
                sh 'go version'
                sh 'git pull origin master'
            }
        }
        
        stage('Test') {
            agent {
                label {
                    label 'nodeworker'
                    customWorkspace '/home/nodeworker/go-webapp-sample'
                }
            }
            steps {
                sh 'go test ./...'
            }
        }
        
        stage('Deploy') {
            agent {
                label {
                    label 'nodeworker'
                    customWorkspace '/home/nodeworker/go-webapp-sample'
                }
            }
            steps {
                script {
                    withEnv(
                        ['JENKINS_NODE_COOKIE=do_not_kill']) {
                            sh 'go run main.go &'
                        }
                }
            }
        }
        
    }
}
