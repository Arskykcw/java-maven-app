@Library('jenkins-shared-library') _

pipeline {
    agent any
    tools {
        maven 'maven-3.9'
    }
    environment {
        DOCKER_IMAGE = 'azeshion21/demo-app:jma-3.0'
    }
    stages {
        stage("Initialize") {
            steps {
                script {
                    gv = load "script.groovy"
                }
            }
        }
        stage("Build JAR") {
            steps {
                script {
                    try {
                        gv.buildJar()
                    } catch (Exception e) {
                        echo "Error building JAR: ${e.message}"
                        throw e
                    }
                }
            }
        }
        stage("Build Docker Image") {
            steps {
                script {
                    try {
                        gv.buildImage(env.DOCKER_IMAGE)
                    } catch (Exception e) {
                        echo "Error building Docker image: ${e.message}"
                        throw e
                    }
                }
            }
        }
        stage("Deploy to Production") {
            steps {
                script {
                    try {
                        gv.deployApp()
                    } catch (Exception e) {
                        echo "Error deploying application: ${e.message}"
                        throw e
                    }
                }
            }
        }
    }
}
