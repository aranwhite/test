pipeline{
agent any
stages {
    stage('Checkout code') {
        steps {
            checkout scm
        }
    }
    stage('Build API in Live API Creator') {
        steps {
            sh 'curl -X POST -d @input.schema http://34.212.226.36:8080/pushToLac -H "Content-Type: application/json"'
        }
    }
    stage('Deploy to Portal - Test') {
        steps {
            sh 'curl -X POST -d @swagger.json http://34.212.226.36:8080/deployToPortal -H "Content-Type: application/json"'     
        }
    }
    stage('Build test for Blazemeter') {
        steps {
            sh 'curl -X POST -d @swagger.json -H "Content-Type: application/json" http://34.212.226.36:8080/startBlazeTest > file.json'     
        }
    }
    stage('Run Test in Blazemeter') {
        steps {
            sh 'bzt file.json .bzt-rc'     
        }
    }
}
}
