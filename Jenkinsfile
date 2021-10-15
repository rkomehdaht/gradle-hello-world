pipeline {
    agent slave1
    tools { 
        gradle 'gradle4'
    }
    stages {
      stage('checkout') {
        steps {
          checkout scm
        }
      }
      stage('build') {
        steps {
          sh "gradle build"
        }
      }
       stage('badge') {
        steps {
          addBadge(icon: 'completed.gif', text: 'OK'
        }
       }
    }
}
