#!/usr/bin/env groovy
// jenkins pipeline

import java.text.SimpleDateFormat

def dateFormat = new SimpleDateFormat("yyyyMMddHHmm")
def date = new Date()
def timestamp = dateFormat.format(date)

pipeline {
  agent any

// variable set
  environment {
    def PROJECTNAME                 = "test-jenkins"
    def APPNAME                     = "${PROJECTNAME}-deploy"
    def WEBHOOKURL                  = ""
  }

  stages {

// Do something
    stage('do something') {
      steps {
        sh"""
        echo "do something"
        """
      }
    }
  }

  post {
    success {
      office365ConnectorSend (
          status: "Pipeline Status",
          webhookUrl: "${WEBHOOKURL}",
          color: '00ff00',
          message: "Test Successful: <b>${JOB_NAME}</b> - ${BUILD_DISPLAY_NAME}<br>Pipeline duration: ${currentBuild.durationString}"
      )
    }

    failure {
      office365ConnectorSend (
          status: "Pipeline Status",
          webhookUrl: "${WEBHOOKURL}",
          color: 'ff0000',
          message: "Test Fail: <b>${JOB_NAME}</b> - ${BUILD_DISPLAY_NAME}<br>Pipeline duration: ${currentBuild.durationString}"
      )
    }
  }
}