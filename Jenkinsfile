pipeline {
  agent {
    node {
      label 'product'
    }
    
  }
  stages {
    stage('CollectDeviceInfo') {
      steps {
        sh 'ls'
      }
    }
    stage('UpdateEnv') {
      steps {
        svn 'http://127.0.0.1:2222'
      }
    }
    stage('UpGradeDevice') {
      steps {
        build(job: 'UpgradeDevice', wait: true)
      }
    }
    stage('RunTest') {
      steps {
        build(job: 'Run', wait: true)
      }
    }
    stage('MergeReport') {
      steps {
        sh 'pwd'
      }
    }
    stage('Retry') {
      steps {
        build(job: 'Retry', wait: true)
      }
    }
    stage('Archive') {
      steps {
        copyArtifacts 'Retry'
      }
    }
    stage('Notification') {
      steps {
        emailext(subject: 'done', body: 'done')
      }
    }
  }
}