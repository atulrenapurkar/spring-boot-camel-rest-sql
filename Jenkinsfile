#!/usr/bin/env groovy

@Library('github.com/fabric8io/fabric8-pipeline-library@master')
def setupScript = null

node('maven') {

    stage('Init') {
        echo 'Init'
        sh '''
                    echo "PATH = ${PATH}"
                    echo "M2_HOME = ${M2_HOME}"
                    echo "JAVA_HOME = ${JAVA_HOME}"                   
                '''
        sh "java -version"
        sh "mvn -version"

        sh "printenv"

        echo "\u2600 BUILD_URL=${env.BUILD_URL}"
        echo "\u2600 JENKINS_URL=${env.JENKINS_URL}"
        echo "\u2600 GIT_URL=${env.GIT_URL}"
        echo "\u2600 JOB_NAME=${env.JOB_NAME}"
        def workspace = pwd()
        echo "\u2600 workspace=${workspace}"

        tokens = "${env.JOB_NAME}".tokenize('/')
        org = tokens[0]
        repo = tokens[1]
        branch = tokens[2]
        echo 'account-org/repo/branch=' + org + '/' + repo + '/' + branch
    }

    stage('Checkout') {
        echo 'Checkout'
        checkout scm
    }

    stage('Prepare') {
        echo 'Prepare'
        sh "oc policy add-role-to-user view -z default"
        sh "oc policy add-role-to-user admin -z jenkins"
    }

    stage('Build') {
        echo 'Build'
        sh "mvn clean package -DskipTests"
    }

    stage('Unit Test') {
        echo 'Unit Test'
        sh "mvn test"
    }

    stage('Integration Test') {
        echo 'Integration Test'
        sh "mvn test"
    }

    stage('Deploy') {
        echo 'deploy'
        sh "mvn clean package fabric8:build -Popenshift -DskipTests"
    }
}
