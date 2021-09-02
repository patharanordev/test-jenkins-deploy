#!/usr/bin/env groovy
// jenkins pipeline

import java.text.SimpleDateFormat

def dateFormat = new SimpleDateFormat("yyyyMMddHHmm")
def date = new Date()
def timestamp = dateFormat.format(date)

pipeline {
  agent { label 'master' }

// variable set
  environment {
    def PROJECTNAME                 = "test-jenkins"
    def APPNAME                     = "${PROJECTNAME}-deploy"
    def WEBHOOKURL                  = "https://tesco.webhook.office.com/webhookb2/2662675d-daee-400e-bda2-e46b54d4f045@3928808b-8a46-426b-8f87-051a36bb2f91/JenkinsCI/a1b1612880654a2bb96ae2902893f358/5567e2dc-8008-4507-9dbc-fb6e2bdfd09f"
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
      // archiveArtifacts artifacts: "${WORKDIR}/result"
      office365ConnectorSend (
          status: "Pipeline Status",
          webhookUrl: "${WEBHOOKURL}",
          color: '00ff00',
          message: "Test Successful: <b>${JOB_NAME}</b> - ${BUILD_DISPLAY_NAME}<br>Pipeline duration: ${currentBuild.durationString}"
      )
      // publishHTML (target : [
      //     allowMissing: false,
      //     alwaysLinkToLastBuild: true,
      //     keepAll: true,
      //     reportDir: "tests/integration/result/jmeter-report-dashboard/jmeter-script",
      //     reportFiles: 'index.html',
      //     reportName: 'Integration Test',
      //     reportTitles: 'NewAG - Integration Test'
      // ])
    }

    failure {
      // office365ConnectorSend webhookUrl: "${WEBHOOKURL}",
      //     message: "<p style=\"color:red\">Fail</p>", 
      //     status:"FAIL"

      office365ConnectorSend (
          status: "Pipeline Status",
          webhookUrl: "${WEBHOOKURL}",
          color: 'ff0000',
          message: "Test Fail: <b>${JOB_NAME}</b> - ${BUILD_DISPLAY_NAME}<br>Pipeline duration: ${currentBuild.durationString}"
      )
    }
  }
}