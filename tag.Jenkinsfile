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

// Do something
    stage('do something') {
      steps {
        sh"""
        echo "do something"
        """
        sh(returnStdout: true, script: "git tag --contains").trim()
      }
    }

// waiting for tag
    stage('build by tag') {
      when {
        tag 'v*'
      }
      steps {
        sh"""
        echo "Building $BRANCH_NAME"
        echo "Building $TAG_NAME"
        """
      }
    }
  }
}