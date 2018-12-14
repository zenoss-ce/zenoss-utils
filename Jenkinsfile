#!/usr/bin/env groovy

node {

  stage('Checkout') {
    checkout scm
  }

  docker.image('zenoss/build-tools:0.0.10').inside() { 
  stage('Build') {
    withMaven() {
      sh "mvn -B package"
    }
  }

  stage('Publish') {
    configFileProvider([configFile(fileId: 'bintray', variable: 'MAVEN_SETTINGS')]) {
      sh "mvn -s $MAVEN_SETTINGS -B deploy"
    }
  }
  }
}
