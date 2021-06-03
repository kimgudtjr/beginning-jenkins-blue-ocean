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
        stash(name: 'build-test-artifacts', includes: 'Ch03/example-maven-project/**/target/surefire-reports/TEST-*.xml,target/*.jar')
      }
    }

    stage('Report & Publish') {
      agent {
        node {
          label 'docker'
        }

      }
      steps {
        unstash 'build-test-artifacts'
        junit 'Ch03/example-maven-project/**/target/surefire-reports/TEST-*.xml'
        archiveArtifacts(artifacts: 'Ch03/example-maven-project/target/*.jar', onlyIfSuccessful: true)
      }
    }

  }
}