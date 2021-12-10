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
  }

  stages {

// Validate checkout
    stage('Validate checkout') {
      steps {
        script {
          sh(returnStdout: true, script: "git tag --contains").trim()
        }
      }
    }

// Build artifact
    stage('Build artifact') {
      when {
        allOf {
          not { tag '*' }
          branch 'main'
        }
      }
      steps {
        script {
          // For variable name "BRANCH_NAME" and "TAG_NAME",
          // it requires to run "sh(returnStdout: true, script: "git tag --contains").trim()" first.
          sh"""
          echo "Built branch : $BRANCH_NAME"
          echo "Built artifact."
          """
        }
      }
    }

// waiting for tag
    stage('Build by tag') {
      when {
        tag 'v*'
      }
      steps {
        sh"""
        echo "Built branch : $BRANCH_NAME"
        echo "Built tag : $TAG_NAME"
        echo "Using artifact..."
        """
      }
    }
  }
}