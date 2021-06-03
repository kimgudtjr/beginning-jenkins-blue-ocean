pipeline {
  agent none
  stages {
    stage('Build & Test') {
      agent {
        node {
          label 'docker'
        }

      }
      steps {
        sh '''cd Ch03/example-maven-project/
mvn -Dmaven.test.failure.ignore clean package'''
        stash(name: 'build-test-artifacts', includes: '**/target/surefire-reports/TEST-*.xml,target/*.jar')
      }
    }

    stage('Report & Publish') {
      agent {
        node {
          label 'docker'
        }

      }
      steps {
        sh 'cd Ch03/example-maven-project/'
        unstash 'build-test-artifacts'
        junit '**/target/surefire-reports/TEST-*.xml'
        archiveArtifacts(artifacts: 'Ch03/example-maven-project/target/*.jar', onlyIfSuccessful: true)
        sh 'sleep 1000'
      }
    }

  }
}