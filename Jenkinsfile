pipeline {
    agent { docker {
        customWorkspace '/tmp/JenkinsWS/go_projects/'
        image 'golang:1.9.3' } }
    stages {
        stage ("Checkout"){
            steps {
                dir("/tmp/JenkinsWS/go_projects/") {
                    echo ("Checking out source code")
                    checkout([$class: 'TeamFoundationServerScm', credentialsConfigurer: [$class: 'AutomaticCredentialsConfigurer'], projectPath: 
'$/TechResearch/goChaincode', serverUrl: 'http://172.16.0.112:8080/tfs/DefaultCollection/', useOverwrite: true, useUpdate: true, workspaceName: 
'Hudson-${JOB_NAME}'])}
                }
            }
        stage('Running Build') {
            steps {
                dir("/tmp/JenkinsWS/go_projects/balance-transfer/artifacts/src/github.com/example_cc/go/go_projects/src") {
                    sh 'pwd'
                    sh 'ls'
                    sh 'go env'
                    sh 'cp -r vendor/* /go/src/'
                    sh 'go build main.go'
                }
            }
        }
                stage('Running Tests') {
            steps {
                
                  dir("/tmp/JenkinsWS/go_projects/balance-transfer/artifacts/src/github.com/example_cc/go/go_projects/src") {
                    sh 'go test'
                }
            }
        }
    }
    
}
