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
      }
    }

// waiting for tag
    stage('build by tag') {
      when { 
        branch: 'master',
        tag:'v*'
      }
      steps {
        sh"""
        echo "build by tag"
        """
      }
    }
  }
}