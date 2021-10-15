pipeline{
    agent {
        label 'slave1'
    }
    tools {
        gradle 'gradle4'
    }
    stages{
		stage ('Checkout'){
            steps{
      			checkout scm  
            } 
   		}
   		stage ('build'){
            steps{
      	        sh "gradle build"
            }
   		}
        stage ('Unit-test'){
            steps{
                sh "gradle test"
                junit 'reports/*.xml'
                archiveArtifacts 'reports/*.xml'
            }
        }
        stage ('Func-test'){
            parallel{
                stage ('Test1'){
                    sh "test-data/int-test.shbuild/libs/oto-gradle-1.0.jar otoMato 'Hello Otomato!'"
                }
                stage ('Test2'){
                    sh "test-data/int-test.shbuild/libs/oto-gradle-1.0.jar ruslan 'Hello Ruslan!'"
                }
                stage ('Test3'){
                    sh "test-data/int-test.shbuild/libs/oto-gradle-1.0.jar piatrovich 'Hello Piatrovich!'"
                }
            }
        }

    }
    post{
        success {
            addBadge(icon: 'completed.gif', text: 'OK')
        }
        failure {
            addBadge(icon: 'error.gif', text: 'Error')
        }
    }
}
