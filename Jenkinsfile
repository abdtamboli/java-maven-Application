#!/usr/bin/env groovy
@Library('jenkins-shared-library')
def gv

pipeline {
    agent any
    tools{
        maven 'Maven'
    }
    stages {
        stage("init") {
            steps {
                script {
                    gv = load "script.groovy"
                }
            }
        }
        stage("build jar") {
            steps {
                script {
                   buildjar()
                }
            }
        }
        stage("build image and Push") {
            steps {
                script {
                    buildImage 'iamabhi1997/my-apps:jma-2.2'
                    dockerLogin()
                    dockerPush 'iamabhi1997/my-apps:jma-2.2'
                }
                
            }
        }
        stage("deploy") {
            steps {
                script {
                    echo "deploying...."
                    gv.deployApp()
                }
            }
        }
    }   
}
